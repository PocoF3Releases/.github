<p align="center">
  <img src="https://raw.githubusercontent.com/PocoF3Releases/.github/main/profile/assets/pocof3releases-banner.webp" alt="PocoF3Releases — Android for alioth" width="100%" />
</p>

# Modern Android for POCO F3

Device sources and hardware integrations for **POCO F3 / Mi 11X (alioth)**, powered by Snapdragon 870. Current ROM work targets **Evolution X / Android 17**.

**[Build updates and support on Telegram](https://t.me/PocoF3_Updates)** · **[Browse repositories](https://github.com/orgs/PocoF3Releases/repositories)**

## Find what you need

- **Building a ROM?** Start with the device, vendor and kernel trees below. Keep their revisions aligned with your ROM manifest.
- **Camera sources are required.** Our device trees include MiuiCamera as the shipped camera replacement. Sync both `device/xiaomi/camera` and `vendor/xiaomi/camera`; follow the [camera integration guide](https://github.com/PocoF3Releases/device_xiaomi_camera#readme).
- **Looking for Xiaomi features?** XiaomiParts lives in the shared device tree; shared hardware and Dolby support live in `hardware_xiaomi`.
- **Investigating stock behavior?** Use `references_code` as research material, not as a ready-to-ship implementation.

## Repository directory

The sources are grouped by their role in the ROM. Branches below are repository defaults; use your ROM manifest to select compatible revisions. Required camera prebuilts are hosted on GitLab.

### Required device, camera and kernel sources

| Repository | Purpose | Default branch |
| --- | --- | --- |
| [device_xiaomi_alioth](https://github.com/PocoF3Releases/device_xiaomi_alioth) | POCO F3 / Mi 11X device configuration | `aosp-17` |
| [device_xiaomi_sm8250-common](https://github.com/PocoF3Releases/device_xiaomi_sm8250-common) | Shared device configuration, XiaomiParts and services | `aosp-17` |
| [vendor_xiaomi_alioth](https://github.com/PocoF3Releases/vendor_xiaomi_alioth) | Device-specific proprietary files | `aosp-17` |
| [vendor_xiaomi_sm8250-common](https://github.com/PocoF3Releases/vendor_xiaomi_sm8250-common) | Shared proprietary files | `aosp-17` |
| [kernel_xiaomi_sm8250](https://github.com/PocoF3Releases/kernel_xiaomi_sm8250) | Redline kernel for alioth | `aosp-17` |
| [device_xiaomi_camera](https://github.com/PocoF3Releases/device_xiaomi_camera) | MiuiCamera integration, compatibility shims and extraction tools | `aosp-17` |
| [vendor_xiaomi_camera (GitLab)](https://gitlab.com/johnmart19/vendor_xiaomi_camera) | Required ready-to-use MiuiCamera APK and proprietary files | `aosp-17` |

### Shared Xiaomi features

| Repository | Purpose | Default branch |
| --- | --- | --- |
| [hardware_xiaomi](https://github.com/PocoF3Releases/hardware_xiaomi) | Shared Xiaomi hardware support and Dolby integration | `cnb` |

### Platform and hardware compatibility

| Repository | Purpose | Default branch |
| --- | --- | --- |
| [frameworks_av](https://github.com/PocoF3Releases/frameworks_av) | Audio and media compatibility, including opt-in Dolby AC-4 support | `cnb` |
| [frameworks_base](https://github.com/PocoF3Releases/frameworks_base) | Android framework and SystemUI changes | `cnb` |
| [hardware_qcom-caf_sm8250_audio](https://github.com/PocoF3Releases/hardware_qcom-caf_sm8250_audio) | Qualcomm SM8250 audio HAL | `cnb` |
| [hardware_qcom-caf_sm8250_display](https://github.com/PocoF3Releases/hardware_qcom-caf_sm8250_display) | Qualcomm SM8250 display HAL | `cnb` |
| [hardware_qcom-caf_sm8250_media](https://github.com/PocoF3Releases/hardware_qcom-caf_sm8250_media) | Qualcomm SM8250 media components | `cnb` |
| [android_hardware_nxp_nfc](https://github.com/PocoF3Releases/android_hardware_nxp_nfc) | NXP NFC hardware support | `lineage-24.0` |
| [system_core](https://github.com/PocoF3Releases/system_core) | Core Android system components | `aosp-17` |
| [vendor_qcom_opensource_usb](https://github.com/PocoF3Releases/vendor_qcom_opensource_usb) | Qualcomm USB integration | `aosp-17` |
| [system_memory_libmeminfo](https://github.com/PocoF3Releases/system_memory_libmeminfo) | DMA-BUF memory accounting compatibility | `cnb` |

### Reference and organization

| Repository | Purpose | Default branch |
| --- | --- | --- |
| [references_code](https://github.com/PocoF3Releases/references_code) | Stock-derived reference material for research | `android13-miui14-cn_beta` |
| [.github](https://github.com/PocoF3Releases/.github) | This organization profile and its assets | `main` |

## Before integrating

- **Sync the complete device stack.** Device configuration, proprietary files, kernel and both camera repositories work together. The vendor camera repository supplies the ready-to-use APK; patch documentation belongs to the camera source tree.
- **Keep hardware ownership clear.** XiaomiParts is maintained in the common device tree. `hardware/xiaomi` remains a standalone dependency for shared Xiaomi features and Dolby integration.
- **Review compatibility options.** Read each repository's README and relevant commits before enabling device-specific behavior. Dolby and media integrations depend on the shipped components; Alioth's settings are not universal defaults for other devices.

Use the **`user` build variant** for release builds. Follow your ROM's manifest for branch selection, especially where default branch names differ from the Android version.

## Get involved

Report problems with your build date, steps to reproduce and relevant logs in [Telegram support](https://t.me/PocoF3_Updates). For source changes, use the relevant repository so the implementation and discussion stay together.
