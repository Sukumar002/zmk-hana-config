# Hana standalone migration audit

## Source snapshot

- Source repository: `Sukumar002/zmk-keyboards`
- Source branch: `zmk-dongle-oled-enhancements`
- Source commit: `126fc6be8c04d748e4f6d97152ede5f7007e9ea7`
- Destination: `Sukumar002/zmk-hana-config`

## Included

- Hana shield definitions, matrix, keymap, and all central/peripheral/dongle variants.
- Shared Studio feature, runtime-layer, and unlock-combo includes used by Hana.
- Custom layout-shift behavior implementation and devicetree bindings.
- OLED brightness/toggle, base-view toggle, and timeout-cycle behaviors and bindings.
- 128x32 and 128x64 OLED snippets.
- ZMK module metadata, root CMake/Kconfig, and the Hana build matrix.
- An independent GitHub Actions workflow that runs on pushes and pull requests to `main`, plus manual dispatch.

## Pinned external dependencies

The copied `config/west.yml` preserves the source snapshot's exact revisions:

| Project | Revision |
| --- | --- |
| `Sukumar002/zmk` | `88d03e9a30d0433375ded7c07c82e5a61f023fbb` |
| `Sukumar002/zmk-dongle-display` | `1c5efa9cb188f9b3c36a18fa8db0d6faba68457f` |
| `mctechnology17/zmk-oled-adapter` | `892c83d60b6a365c35334c06831d9c5b0f2ba9c0` |

The display module provides Hana charging-state telemetry (`CONFIG_HANA_CHARGE_STATUS`) and the dongle display implementation. The pinned custom ZMK fork provides the Studio unlock behavior and custom Studio support used by this configuration.

## Deliberately excluded

- Chocofi, Sweep, Sofle, Corne, and all other shield configurations.
- Multi-board/unified-dongle orchestration and unrelated build-console tooling.
- `dts/peripherals/cirque.dtsi`: no Hana shield/keymap include references it in this source snapshot.

## Important validation caveat

The source snapshot's own Hana workflow did not include `zmk-dongle-oled-enhancements` in its push branch allowlist. This standalone workflow deliberately fixes that operational gap by building from `main` on every push and pull request.

The migration preserves the source build matrix; it does not assert that the new repository has already completed a successful build or that hardware has been tested. Check the first Actions run for compile-time dependency or devicetree issues before flashing.
