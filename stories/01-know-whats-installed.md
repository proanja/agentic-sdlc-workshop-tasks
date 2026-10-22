# Story 01 — Know what's installed

**From:** Maintenance team lead

As a maintenance engineer I want to see which sensors are installed on our lines, so that I know what I am responsible for and can find a device quickly when something goes wrong. Today this lives in a spreadsheet that is always out of date.

We need to **register** a device when it is installed, **look up** one device by its serial number, and **list** all devices — optionally filtered by line, by kind of sensor, or both.

For each device we store:

- **Serial number** — upper-case letters, digits and hyphens, 3 to 32 characters. It identifies the device, so it must be unique: registering the same serial number twice is refused.
- **Kind of sensor** — one of `PHOTOELECTRIC`, `DISTANCE`, `LIDAR_2D`, `ENCODER`. Anything else is refused.
- **Firmware version** — a version like `2.10.0`, optionally with a pre-release suffix like `3.0.0-rc.2`.
- **Line** and **station** — where it is mounted, free text, 1 to 64 characters.

All fields are required. Looking up a serial number that does not exist says so clearly.

**Out of scope:** changing or deleting devices, login.
