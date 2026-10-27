# Chase project context

Copy this file to the application repository as `.agents/chase-project.md`. Replace the guidance below with actual local facts and remove irrelevant sections. Keep shared Chase standards in Chase Workshop; this file holds project-specific details.

## Architecture and reuse

Name the layers, ownership boundaries, and canonical modules an implementation should inspect, including shared UI components and service packages used by multiple Lambdas or services when relevant. Link to maintained architecture guidance rather than repeating it.

## Contracts and vocabulary

Name shared schemas, domain terminology, public interfaces, compatibility requirements, and relevant error conventions.

For data access, identify canonical key builders, PK/SK or index conventions, expected queries, and intentional bounded scans when applicable. For security-sensitive work, identify ownership/tenant boundaries and where roles, resource policies, and trust relationships are defined. Record local constraints rather than inventing a universal schema or policy.

## Tests and verification

Provide exact commands from this repository for relevant unit, integration, end-to-end, lint, and type checks, using the actual configurations and flags. State required services and test-data isolation. Omit commands or test levels that do not exist.

### Optional app-verification recipe

For repeated user-flow or integration verification, record only the relevant parts:

- **Launch:** working directory, command, required services, and how to detect readiness before driving the app. Refer to credential setup without embedding secrets.
- **Preflight:** required configuration, isolated test data or account, dependency health checks, and how to recognize an unavailable environment.
- **Scenario:** entry point, inputs or fixture, actions, and the expected observable result. Where persistence matters, include independent read-back rather than relying only on a success message.
- **Evidence:** the assertions, output, screenshots, or read-back that demonstrate the result; where console, stderr, and server errors surface; and where non-sensitive evidence belongs.
- **Cleanup:** how to remove only the test data and processes created by this run, including after a failure. Leave pre-existing services and user data intact.

This recipe is optional project context, not a requirement to add a new verification framework or maintain a full navigation map.

## Review context

Describe branch-target conventions and generated artifacts. Record intentional local exceptions to the shared standards with their reasons. A branch convention helps scope resolution; explicit PR metadata still determines an existing PR's actual target.
