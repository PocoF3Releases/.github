# Organization documentation rules

Scope: this repository contains the public organization profile and shared assets. Implementation and validation evidence belong in the relevant source repositories and the [project workhub](https://github.com/PocoF3Releases/Agents.md).

- `profile/README.md` owns the active Android 17 repository inventory. GitHub renders it on the organization page; do not create a competing root README inventory.
- `Legacy.md` owns Android 16 branch references. Keep one short link to it in the active profile rather than duplicating legacy tables.
- Verify repository URLs and branch existence before editing tables. Keep required GitLab camera prebuilts alongside the camera source integration.
- Use `aosp-17` for the primary kernel; `aosp-17-old_base` is historical. Preserve each repository's actual branch name (`cnb`, `aosp-17`, or `lineage-24.0`).
- Distinguish NXP HAL teardown from framework NFC shell compatibility. Neither patch replaces the other; remove custom patches only after checking upstream equivalence.
- Source availability, successful compilation, device tests and user confirmation are different evidence. Do not describe an inventory as a validated release manifest.
- Keep the profile concise, with relative links to local Markdown files. Do not add update dates, daily status logs, private workstation paths, credentials or personal details. Public proprietary-repository references are allowed.
- Check Markdown links, table consistency and `git diff --check` locally. Do not add GitHub Actions.
- Preserve attribution. Agent-assisted commits include `Co-authored-by: codex <noreply@openai.com>`.
