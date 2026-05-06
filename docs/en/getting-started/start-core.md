# Start Core

AutoLXB automation is provided by the on-device `lxb-core`. The app starts Core, manages configuration, and displays status; `lxb-core` performs the actual task execution.

## Root startup

Root startup is the shortest path for rooted devices.

1. Open the AutoLXB home page.
2. Tap **Root startup**.
3. Grant `su` permission in the system prompt.
4. Wait until the home page shows that Core is running.

## ADB startup

ADB startup is for non-root devices and requires one Wireless ADB pairing process.

1. Open Android **Developer Options**.
2. Enable **USB debugging** and **Wireless debugging**.
3. Return to AutoLXB and tap **ADB startup**.
4. Follow the guide to open the Wireless debugging pairing page.
5. Submit the pairing code from the notification and wait for pairing and startup to complete.

Full demo video: <https://www.bilibili.com/video/BV114RbBfEou>

## How to confirm startup succeeded

After a successful startup, you should see:

- The home page says Core is running.
- The task page can refresh runtime status.
- The log page shows Core trace events.

## Common issues

- **No pairing-code input in the notification shade**: check AutoLXB notification permission and allow notifications.
- **Core stops after closing the foreground app**: open Developer Options and confirm **USB debugging** is still enabled.
- **Root startup fails**: check whether your root manager denied or timed out the `su` request.
- **Other problems**: report them on GitHub Issues with device model, system version, startup method, and log screenshots.
