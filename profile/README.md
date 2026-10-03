<p align="center">
  <img src="https://raw.githubusercontent.com/PocoF3Releases/.github/main/profile/assets/pocof3releases-banner.webp" alt="PocoF3Releases — Android for alioth" width="100%" />
</p>

# Modern Android for POCO F3

Device sources and hardware integrations for **POCO F3 / Mi 11X (alioth)**, powered by Snapdragon 870. Active development targets **Evolution X / Android 17**.

**Android 17 is the active stack.** Older sources are listed separately in the [Android 16 legacy index](../Legacy.md).

**[Build updates and support on Telegram](https://t.me/PocoF3_Updates)** · **[Browse repositories](https://github.com/orgs/PocoF3Releases/repositories)**

## Find what you need

- **Building a ROM?** Start with the device, vendor and kernel trees below. Keep their revisions aligned with your ROM manifest.
- **Camera sources are required.** The device trees integrate MiuiCamera as the shipped camera replacement. Sync both `device/xiaomi/camera` and `vendor/xiaomi/camera`; follow the [camera integration guide](https://github.com/PocoF3Releases/device_xiaomi_camera#readme).
- **Looking for Xiaomi features?** XiaomiParts lives in the shared device tree; shared hardware and Dolby support live in `hardware_xiaomi`.
- **Investigating stock behavior?** Use `references_code` as research material, not as a ready-to-ship implementation.
- **Working with the project knowledge base?** See [Agents.md](https://github.com/PocoF3Releases/Agents.md) for maintained project context, validation notes and integration references.

## Android 17 repositories

The sources below are grouped by their role in the ROM. Branches shown are the current Android 17 integration branches. Required camera prebuilts are hosted on GitLab.

### Required device, camera and kernel sources

| Repository | Purpose | Branch |
| --- | --- | --- |
| [device_xiaomi_alioth](https://github.com/PocoF3Releases/device_xiaomi_alioth) | POCO F3 / Mi 11X device configuration | `aosp-17` |
| [device_xiaomi_sm8250-common](https://github.com/PocoF3Releases/device_xiaomi_sm8250-common) | Shared device configuration, XiaomiParts and services | `aosp-17` |
| [vendor_xiaomi_alioth](https://github.com/PocoF3Releases/vendor_xiaomi_alioth) | Device-specific proprietary files | `aosp-17` |
| [vendor_xiaomi_sm8250-common](https://github.com/PocoF3Releases/vendor_xiaomi_sm8250-common) | Shared proprietary files | `aosp-17` |
| [kernel_xiaomi_sm8250](https://github.com/PocoF3Releases/kernel_xiaomi_sm8250) | Redline kernel for alioth | `aosp-17` |
| [device_xiaomi_camera](https://github.com/PocoF3Releases/device_xiaomi_camera) | MiuiCamera integration, compatibility shims and extraction tools | `aosp-17` |
| [vendor_xiaomi_camera (GitLab)](https://gitlab.com/johnmart19/vendor_xiaomi_camera) | Required ready-to-use MiuiCamera APK and proprietary files | `aosp-17` |

### Shared Xiaomi features

| Repository | Purpose | Branch |
| --- | --- | --- |
| [hardware_xiaomi](https://github.com/PocoF3Releases/hardware_xiaomi) | Xiaomi interfaces, Dolby, sensors, fingerprint and stock-backed Alioth vibrator HAL | `cnb` |

### Platform and hardware compatibility

| Repository | Purpose | Branch |
| --- | --- | --- |
| [frameworks_av](https://github.com/PocoF3Releases/frameworks_av) | Legacy Dolby DAP lifecycle and Xiaomi camera compatibility | `cnb` |
| [frameworks_base](https://github.com/PocoF3Releases/frameworks_base) | High-refresh recording, independent recording blur control and NFC shell compatibility | `cnb` |
| [hardware_qcom-caf_sm8250_audio](https://github.com/PocoF3Releases/hardware_qcom-caf_sm8250_audio) | Qualcomm SM8250 audio HAL | `cnb` |
| [hardware_qcom-caf_sm8250_display](https://github.com/PocoF3Releases/hardware_qcom-caf_sm8250_display) | Qualcomm SM8250 display HAL | `cnb` |
| [hardware_qcom-caf_sm8250_media](https://github.com/PocoF3Releases/hardware_qcom-caf_sm8250_media) | Qualcomm SM8250 media components | `cnb` |
| [android_hardware_nxp_nfc](https://github.com/PocoF3Releases/android_hardware_nxp_nfc) | NXP NFC HAL shutdown queue fix | `lineage-24.0` |
| [external_tinycompress](https://github.com/PocoF3Releases/external_tinycompress) | Blocking compressed-capture reads expected by the legacy Qualcomm audio HAL | `lineage-24.0` |
| [vendor_qcom_opensource_usb](https://github.com/PocoF3Releases/vendor_qcom_opensource_usb) | Qualcomm USB integration | `aosp-17` |

Android 17 uses Evolution X upstream for `system/core` and `system/memory/libmeminfo`; the required init and optional DMA-BUF fixes are included upstream. HBM and AC-4 support are also upstream, while the framework forks remain required for their other device-specific changes.

## NFC: two independent fixes

- **NXP HAL:** preserves the client queue ID during teardown so the close-complete message can be consumed. This prevents the repeated `NFC client received bad message` loop while retaining the timer lifetime fix.
- **Framework `svc nfc`:** delegates enable/disable to the NFC service shell interface, avoiding hidden modular-framework APIs. This is command-line compatibility, not a HAL shutdown fix. Direct callers can use `cmd nfc enable-nfc` or `cmd nfc disable-nfc '[persist]'` on the integrated NFC module.

Keep both patches while their respective upstream bases lack equivalent fixes. Neither is a substitute for the other; verify equivalence before dropping either during a rebase. Tinycompress similarly fixes the compressed-capture read contract, not every possible messaging-app audio issue.

## Reference and organization

| Repository | Purpose | Branch |
| --- | --- | --- |
| [references_code](https://github.com/PocoF3Releases/references_code) | Stock-derived reference material for research and behavior comparison | `android13-miui14-cn_beta` |
| [Agents.md](https://github.com/PocoF3Releases/Agents.md) | Project knowledge base, integration notes, validation records and workflow documentation | `main` |
| [.github](https://github.com/PocoF3Releases/.github) | Organization profile and shared profile assets | `main` |

## Before integrating

- **Sync the complete device stack.** Device configuration, proprietary files, kernel and both camera repositories work together. The vendor camera repository supplies the ready-to-use APK; patch documentation belongs to the camera source tree.
- **Keep hardware ownership clear.** XiaomiParts is maintained in the common device tree. `hardware/xiaomi` remains a standalone dependency for shared Xiaomi features and Dolby integration.
- **Review compatibility options.** Read each repository's README and relevant commits before enabling device-specific behavior. Dolby and media integrations depend on the shipped components; Alioth's settings are not universal defaults for other devices.
- **Treat legacy branches as archival.** Android 16 branches are retained for reference only and should not be assumed to contain current fixes.

Use the **`user` build variant** for release builds. Follow your ROM's manifest for branch selection where upstream branch names differ. The tables are an integration inventory, not a pinned release manifest or proof of device validation. After `repo sync`, check that upstream checkouts still contain the required custom patches; preserve new upstream changes and omit patches already integrated there.

The primary kernel branch is `aosp-17`. `aosp-17-old_base` is historical and must not replace it in a current build.

## Get involved

Report problems with your build date, steps to reproduce and relevant logs in [Telegram support](https://t.me/PocoF3_Updates). For source changes, use the relevant repository so the implementation and discussion stay together.
