## Versioning Flow

This project uses automated semantic versioning based on Git triggers and target branches, following a defined set of rules.

Versioning Configuration:
```JSON
{
    "scheme": "org_semantic",
    "versionFile": "./package.json",
    "files": ["./package-lock.json"],
    "rules": [
        {
        "trigger": "commit",
        "branch": "main",
        "suffix": "-beta"
        },
        {
        "trigger": "pull-request",
        "destBranch": "main",
        "suffix": "-beta",
        "bump": "build"
        },
        {
        "trigger": "pull-request",
        "destBranch": "release",
        "bump": "minor",
        "reset": "build"
        }
    ]
}

```

How it works:
 - When committing directly to the `main` branch:
    - The version includes a -beta suffix (e.g., 1.0.0 → 1.0.0-beta).
    - This suffix indicates a development or pre-release version.

When creating a pull request into the `main` branch:
 - The version is bumped at the build level (e.g., 1.0.0-beta → 1.0.1-beta).
 - The -beta suffix is maintained throughout the pull request lifecycle.

When creating a pull request into the `release` branch:
 - The version is bumped at the minor level (e.g., 1.0.1 → 1.1.0).
 - The build counter is reset, and the suffix is not applied (stable release).

This setup ensures consistent versioning for development, staging, and production, clearly distinguishing beta/pre-release builds from stable versions.