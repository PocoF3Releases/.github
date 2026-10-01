<p align="center">
  <img src="https://raw.githubusercontent.com/PocoF3Releases/.github/main/profile/assets/pocof3releases-banner.webp" alt="PocoF3Releases — Android for alioth" width="100%" />
</p>

# Modern Android for POCO F3

Device sources and hardware integrations for **POCO F3 / Mi 11X (alioth)**, powered by Snapdragon 870. Active development targets **Evolution X / Android 17**.

> **Android 16 is no longer maintained.** Existing `aosp-16` branches are kept only as historical/legacy sources and may not receive fixes, compatibility updates, or security-related backports.

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
| [hardware_xiaomi](https://github.com/PocoF3Releases/hardware_xiaomi) | Shared Xiaomi hardware support and Dolby integration | `cnb` |

### Platform and hardware compatibility

| Repository | Purpose | Branch |
| --- | --- | --- |
| [frameworks_av](https://github.com/PocoF3Releases/frameworks_av) | Legacy Dolby DAP lifecycle and Xiaomi camera compatibility | `cnb` |
| [frameworks_base](https://github.com/PocoF3Releases/frameworks_base) | Android framework and SystemUI changes | `cnb` |
| [hardware_qcom-caf_sm8250_audio](https://github.com/PocoF3Releases/hardware_qcom-caf_sm8250_audio) | Qualcomm SM8250 audio HAL | `cnb` |
| [hardware_qcom-caf_sm8250_display](https://github.com/PocoF3Releases/hardware_qcom-caf_sm8250_display) | Qualcomm SM8250 display HAL | `cnb` |
| [hardware_qcom-caf_sm8250_media](https://github.com/PocoF3Releases/hardware_qcom-caf_sm8250_media) | Qualcomm SM8250 media components | `cnb` |
| [android_hardware_nxp_nfc](https://github.com/PocoF3Releases/android_hardware_nxp_nfc) | NXP NFC hardware support | `lineage-24.0` |
| [vendor_qcom_opensource_usb](https://github.com/PocoF3Releases/vendor_qcom_opensource_usb) | Qualcomm USB integration | `aosp-17` |

Android 17 uses Evolution X upstream for `system/core` and `system/memory/libmeminfo`; the required init and optional DMA-BUF fixes are included upstream. HBM and AC-4 support are also upstream, while the framework forks remain required for their other device-specific changes.

## Android 16 legacy branches

Android 16 development has ended. Existing `aosp-16` branches may remain available in individual repositories for reference, older builds, or comparison, but they are **not maintained or supported as the current device stack**.

For new builds and ongoing development, use the Android 17 branches above.

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

Use the **`user` build variant** for release builds. Follow your ROM's manifest for branch selection where upstream branch names differ.

## Get involved

Report problems with your build date, steps to reproduce and relevant logs in [Telegram support](https://t.me/PocoF3_Updates). For source changes, use the relevant repository so the implementation and discussion stay together.
