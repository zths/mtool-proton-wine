# MTool Proton Wine

This branch builds a Winlator-compatible ARM64EC Wine from Valve's `proton_11.0` branch.

## Base

- Valve Wine branch: `proton_11.0`
- Valve base commit: `81d78e4f3ea8ce868d775021fdc9f90122dc1a6b`
- Android/ARM64EC support adapted from AndreVto/proton-wine
- Android SDK 35 and 16 KiB page-size support

## MTool locale extension

Android Bionic does not provide the glibc locale archive expected by Wine. The launcher may set:

```text
WINLATOR_LOCALE=ja_JP.UTF-8
```

Wine consumes this value during ntdll locale initialization, before the process ACP/OEMCP tables are selected. For example, `ja_JP.UTF-8` selects Windows code page 932.

## Build

Follow `.github/workflows/build-proton-sdk35.yml`. For ARM64EC, run the `build-step0.sh` and `build-step-arm64ec.sh` stages in order. The `server_protocol.def.patch` must be applied before generated server protocol headers are produced.

## Binary release

The WCP archive is published through GitHub Releases rather than committed to Git.
