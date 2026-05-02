# About Tab

**Runtime Atlas v1.2.0**

---

## Purpose

Displays the current package version, publisher information, and a brief tool description. Used to verify the installed version after import or upgrade.

---

## Displayed Information

| Field | Value |
|-------|-------|
| **Tool Name** | Runtime Atlas |
| **Publisher** | Tools Studio |
| **Version** | Version 1.2.0 |
| **Description** | Brief tool summary |
| **Documentation** | Reference to the Documentation folder |

---

## Version Verification

After import or upgrade, open this tab and confirm the version string matches the expected version. If it shows an unexpected version, the import may be incomplete or a stale compiled assembly may be cached. Delete `Library/` and reopen the project to force a clean recompile.
