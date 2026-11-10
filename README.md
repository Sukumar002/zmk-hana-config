# Hana ZMK Configuration

Standalone firmware configuration for the Hana split keyboard and its central-dongle variants.

## Source of this migration

Migrated from:

- Repository: [Sukumar002/zmk-keyboards](https://github.com/Sukumar002/zmk-keyboards)
- Branch: `zmk-dongle-oled-enhancements`
- Source commit: `126fc6be8c04d748e4f6d97152ede5f7007e9ea7`

The migration copies Hana-specific firmware sources and the local modules required to build them. It does not modify or remove Hana from the source repository.

## Firmware targets

The GitHub Actions workflow builds all eight artifacts listed in [build-hana.yaml](build-hana.yaml):

| Artifact | Board | Purpose |
| --- | --- | --- |
| `hana_settings_reset_xiao` | `xiao_ble` | Reset settings on either Hana half |
| `hana_settings_reset_dongle` | `nice_nano` | Reset settings on the dongle |
| `hana_left_central` | `xiao_ble` | BLE mode, left half central |
| `hana_left_peripheral` | `xiao_ble` | Dongle-central mode, left peripheral |
| `hana_right_peripheral` | `xiao_ble` | Dongle-central mode, right peripheral |
| `hana_dongle_no_display` | `nice_nano` | Central dongle without OLED |
| `hana_dongle_central_128x32` | `nice_nano` | Central dongle with 128x32 OLED |
| `hana_dongle_central_128x64` | `nice_nano` | Central dongle with 128x64 OLED |

## Pinned dependencies

`config/west.yml` pins the exact dependency revisions used by the migration:

- Custom ZMK fork: `Sukumar002/zmk` at `88d03e9a30d0433375ded7c07c82e5a61f023fbb`
- Dongle display module: `Sukumar002/zmk-dongle-display` at `1c5efa9cb188f9b3c36a18fa8db0d6faba68457f`
- OLED adapter: `mctechnology17/zmk-oled-adapter` at `892c83d60b6a365c35334c06831d9c5b0f2ba9c0`

These are intentionally pinned rather than tracking moving branches.

## ZMK Studio

The central builds retain the `studio-rpc-usb-uart` snippet and `CONFIG_ZMK_STUDIO=y`. The keymap also retains the runtime layer slots, Studio unlock chord, and runtime-editable behaviors. Firmware-side compatibility is included here; the custom Studio web application remains a separate project.

## Build

Pushes and pull requests targeting `main` trigger the independent Hana build workflow. You can also start it manually from **Actions → Build Hana Firmware → Run workflow**.

## Validation status

This is the initial standalone migration snapshot, not yet a declared v2.3 release. GitHub Actions build results and physical hardware validation must be checked before replacing any known-good firmware or treating this snapshot as released.

See [the migration audit](docs/MIGRATION.md) for scope and dependency notes.
