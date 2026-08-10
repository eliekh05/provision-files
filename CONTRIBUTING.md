# Contributing to Provision Files

Thank you for helping grow Provision Files!

## Adding a Provisioning Profile

1. **Obtain** the provisioning profile from a macOS application.
2. **Verify** that the profile is valid and opens correctly on macOS.
3. **Rename** the file giving it a clear, application-based name.
   * *Examples:* `Google Chrome.provisionprofile`, `Discord.provisionprofile`, `Visual Studio Code.provisionprofile`
4. **Place** the file in the appropriate location under the `profiles/` directory.
5. **Commit** your changes.
6. **Open** a pull request.

## File Naming

Use the name of the bundle that directly contains the provisioning profile as the filename. 

The filename should describe the bundle the provisioning profile belongs to, rather than using the generic original filename found inside the application bundle. Always remove the bundle extension (e.g., `.app`, `.appex`) from the filename.

**Example:**
If an application contains `embedded.provisionprofile` and the main bundle containing it is `Google Chrome.app`, submit it as:
`Google Chrome.provisionprofile`

### Nested Bundles

Provisioning profiles can also exist inside nested bundles such as `.appex`, helper applications, plugins, widgets, and other components. In these cases, use the name of the **nested bundle** that directly contains the provisioning profile, *not* the name of the main application.

**Example 1: Widgets & Plugins**
```text
Pock.app
└── Contents
    └── PlugIns
        └── QLPockWidget.appex
            └── Contents
                └── embedded.provisionprofile

```

✅ The profile should be named: `QLPockWidget.provisionprofile`

❌ Not: `Pock.provisionprofile`

**Example 2: Helper Applications & Login Items**

```text
CleanMyMac_5.app
└── Contents
    └── Library
        └── LoginItems
            └── CleanMyMac_5_HealthMonitor.app
                └── Contents
                    └── embedded.provisionprofile

```

✅ The profile should be named: `CleanMyMac_5_HealthMonitor.provisionprofile`

❌ Not: `CleanMyMac_5.provisionprofile`

Example 3: Handling Generic Bundle Names to Avoid Conflicts

If the innermost bundle has a highly generic name (like XPCService.xpc) that could easily conflict with other applications, use the name of the most descriptive parent bundle instead.

Plaintext
SwiftPlantUMLApp.app
└── Contents
    └── PlugIns
        └── ActionExtension.appex
            └── Contents
                └── XPCServices
                    └── XPCService.xpc
                        └── Contents
                            └── embedded.provisionprofile
✅ The profile should be named: ActionExtension.provisionprofile

❌ Not: XPCService.provisionprofile (to avoid naming conflicts)

Example 4: Handling Generic Bundle Names (Hyphenated)

If the innermost bundle is generic and there is no descriptive intermediate bundle, combine the generic name with the main application name to prevent conflicts.

Plaintext
SwiftPlantUMLApp.app
└── Contents
    └── XPCServices
        └── XPCService.xpc
            └── Contents
                └── embedded.provisionprofile
✅ The profile should be named: XPCService-SwiftPlantUMLApp.provisionprofile

❌ Not: XPCService.provisionprofile

Example 5: Multiple Profiles in the Same Bundle

If multiple provisioning profiles exist inside the same bundle and have unique original names, combine the bundle name with the original filename's descriptor to prevent conflicts.

Plaintext
Apple Configurator.app
└── Contents
    └── Resources
        ├── distribution.provisionprofile
        └── UPP.provisionprofile
✅ The profiles should be named: Apple Configurator-distribution.provisionprofile and Apple Configurator-UPP.provisionprofile

❌ Not: Apple Configurator.provisionprofile

*Note: If multiple provisioning profiles exist inside different bundles of the same application, each profile should be treated as a separate profile and named after its respective containing bundle.*

## Pull Requests

Please keep pull requests focused on adding or updating provisioning profiles.

Before submitting a pull request, check that:

* The file is a valid provisioning profile.
* The filename clearly identifies the bundle that directly contains the profile.
* The profile is not already present in the repository.
* No unrelated files or changes are included.

*Note: Maintainers may modify the organization or filename of a submitted profile when necessary.*

## Issues

Use the repository’s Issues tab to:

* Request a provisioning profile.
* Report a missing or incorrect profile.
* Report a duplicate.
* Report a problem with a profile already in the repository.
* Report other repository-related problems.

When reporting a profile issue, please provide as much detail as possible, including the **application name, bundle name, application version**, and **distribution method**.

## Third-Party Content

Contributors should not assume that submitting a third-party provisioning profile transfers ownership or licensing rights to the repository.

The repository’s MIT License applies to the original repository content and does **not** automatically relicense third-party provisioning profiles.
