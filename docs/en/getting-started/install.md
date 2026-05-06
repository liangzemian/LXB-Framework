# Installation and Preparation

This page covers the required preparation before and after installing the APK, including device requirements, system switches, ROM compatibility settings, and battery policy.

## Supported devices

- A real Android device running **Android 11 (API 30)** or later.
- Non-root devices need Wireless debugging for Wireless ADB startup.
- Rooted devices need to grant `su` permission normally.

## Install the APK

1. Download the APK from GitHub Releases.
2. Install it on your phone.
3. Open AutoLXB for the first time and follow the in-app setup guidance.

## Required settings

Before starting Core, make sure:

- **Developer Options** are enabled.
- **USB debugging** is enabled.
- Non-root devices have **Wireless debugging** enabled.
- Your ROM-specific compatibility settings are handled:

| ROM | Suggested action |
| --- | --- |
| MIUI / HyperOS | Enable **USB debugging (Security settings)**. |
| ColorOS | Disable **Permission monitoring**. |
| Flyme | Disable **Flyme payment protection**. |

!!! warning "Keep USB debugging enabled"
    The on-device service depends on the debugging environment to stay alive. Even after pairing, keep USB debugging enabled. Otherwise, Core may need to be restarted after the foreground app is closed.

## Battery policy

Set AutoLXB battery usage to **Unrestricted** if possible. This reduces the chance that the system kills pairing, startup, or task execution in the background.
