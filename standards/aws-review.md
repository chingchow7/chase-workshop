# AWS review notes

Read only when the change touches DynamoDB access or IAM/Lambda permissions. Establish the project's schema, existing shared libraries, infrastructure, and execution paths before proposing remedies.

## DynamoDB

- Trace the access pattern to existing table/index definitions and canonical key builders. Preserve actual PK/SK formats, tenant keys, projections, and write/read contracts; do not guess a new index or key shape from one call site.
- A `Query` needs a partition-key value and can narrow by sort-key conditions. Verify that a proposed replacement for `Scan` is supported by an existing access path, or identify the index/migration decision it needs. Filters are applied after reading for both operations, so adding a filter is not a read-capacity optimization. [Query API](https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_Query.html), [Scan behavior](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Scan.html)
- Check pagination against `LastEvaluatedKey`, including empty filtered pages with more data. Check consistency needs before using a GSI, which supports eventual consistency. Preserve tenant authorization in any replacement path. [Query API](https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_Query.html)
- Evaluate scans by workload and purpose. A tenant-facing request that repeatedly walks a growing table needs scrutiny; a controlled maintenance/export scan may be justified. State the growth or capacity concern and the known access-path alternative. [Query and scan best practices](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/bp-query-scan.html)

## IAM and Lambda

- Map changed API calls to the principal, actions, resources, and conditions they need. Inspect the execution role as well as invocation/resource policies and trust relationships where relevant. Shared libraries do not justify granting every Lambda the union of every consumer's permissions. [IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html), [Lambda permissions](https://docs.aws.amazon.com/lambda/latest/dg/security_iam_service-with-iam.html)
- Verify which actions support resource-level scoping and condition keys. Some actions require `Resource: "*"`; report unnecessary privilege with the supported narrower policy, not an indiscriminate wildcard ban. Check permission changes against the application's actual resource and index use. [Lambda IAM support](https://docs.aws.amazon.com/lambda/latest/dg/security_iam_service-with-iam.html)
- Passing static checks is not proof of deployed effective permissions. Note unavailable policy layers or account context and distinguish missing evidence from a demonstrated excess grant. [IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
