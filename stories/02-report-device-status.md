# Story 02 — Report device status

**From:** Automation engineer

Our gateways forward a status message from each sensor — every few seconds up to every few minutes, depending on the device. We want the service to accept these messages and always know the **latest state** of every device.

A status message contains:

- **Serial number** of the device that sent it.
- **Timestamp** — when it was measured, in UTC.
- **Temperature** inside the device, in °C, between −40 and 125. Required.
- **Contamination** — how dirty the optics are, in %, between 0 and 100. Optional: only optical sensors send it.

Networks are messy, so:

- A message from a device that is **not registered** is refused, and nothing is stored. It must not create a device.
- A message with a timestamp **more than 60 seconds in the future** is refused (small clock differences are fine).
- The **same message twice** (same device, same timestamp) is accepted, but stored only once.
- A message **older than the latest one** we already have is accepted, but does not change the device's latest state.

The service receives one message per request.

**Out of scope:** batches of messages, history or trends.
