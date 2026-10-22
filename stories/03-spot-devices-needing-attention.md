# Story 03 — Spot devices that need attention

**From:** Maintenance planner

Every morning I want one **overview** of the fleet: how many devices are fine, and which ones need attention and why — worst problems first. I also want to look at **a single device** and see exactly which rules it breaks.

The rules:

| Rule | Warning | Critical |
|---|---|---|
| Temperature | 70.0 °C or more | 85.0 °C or more |
| Contamination (only if the device sent a value) | 40 % or more | 70 % or more |
| Firmware older than the approved minimum for its kind of sensor | always a warning | — |

- A device is **offline** if it has never sent an accepted message, or if its latest accepted message is **more than 10 minutes** old.
- Firmware versions are compared as versions, not as text: `2.10.0` is newer than `2.9.3`, and a pre-release like `3.0.0-rc.2` is older than `3.0.0`. A kind of sensor without an approved minimum gets no firmware finding.

Each device gets one **status**:

- `OFFLINE` if it is offline. Its old temperature and contamination values are not judged any more, but outdated firmware is still reported.
- Otherwise its worst finding: `CRITICAL`, then `WARNING`, or `OK` if there is none.

The **overview** shows the number of devices per status, and lists every device that is not `OK`: first `CRITICAL`, then `OFFLINE`, then `WARNING`, and within each group by line, station and serial number.

For a **single device**, show its status and each finding with the rule, the measured value, and the limit.

"Now" comes from the server clock, but tests must be able to set it to a fixed time.
