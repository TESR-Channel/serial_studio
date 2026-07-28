# TESR Serial Studio

A **web serial monitor** by Thai Embedded System and Robotics (TESR).
Runs 100% in the browser (no install, no backend) using the **Web Serial API**.

![theme](Logo_Red-No-Background.png)

## Features

- **Connect to any serial port** — USB-UART, RS485 adapters, Arduino, STM32, ESP32…
- **Cross-platform**: Windows, Linux, macOS, Raspberry Pi (any Chromium-based browser)
- **4 display/edit modes**: ASCII / HEX / Decimal / Binary (Docklight style)
- **Modbus RTU decode mode**: frames split by silence gap, CRC16 verify,
  function-code names, register values, exception decoding
- **Send Sequences**: named packets, per-sequence edit mode, optional auto
  CRC16 append, periodic repeat (polling)
- **Receive Sequences**: pattern match on incoming data with highlight +
  automatic answer (slave simulation)
- **Quick Send** bar with one-click Modbus CRC
- **Save / Load project** as JSON (like Docklight `.ptp`) — sequences + port settings
- **Save log** to a text file
- Dark TESR theme (dark red / gold)

## Deploy on GitHub Pages

1. Create a repository, e.g. `tesr-serial-studio`
2. Upload `index.html`, `Logo_Red-No-Background.png`, `README.md`
3. Repo **Settings → Pages → Source: Deploy from a branch → main / (root)**
4. Open https://tesr-channel.github.io//tesr-serial-studio

> Web Serial requires a **secure context** — GitHub Pages (HTTPS) or
> `http://localhost` both work. Opening the file directly (`file://`) also works
> in Chrome for local testing.

## Browser support

| Platform | Browser | Works |
|---|---|---|
| Windows / macOS / Linux | Chrome, Edge, Opera, Brave | ✅ |
| Raspberry Pi OS | Chromium (pre-installed) | ✅ |
| Any | Firefox / Safari | ❌ (no Web Serial API) |

On Linux / Raspberry Pi, add your user to the `dialout` group if the port is not listed:

```bash
sudo usermod -aG dialout $USER   # then log out / in
```

## Modbus RTU tips

- Turn on **Modbus RTU decode** in the toolbar. Incoming bytes are grouped into
  frames using the **Frame gap (ms)** silence timeout (default 10 ms — raise it
  for slow baud rates, e.g. ~4 ms per character at 9600 baud).
- In a Send Sequence, enter only `ID FC DATA...` (e.g. `01 03 00 00 00 0A`) and
  tick **Append Modbus CRC16** — the CRC is calculated for you on every send.
- A Receive Sequence with an answer + CRC lets the page act as a simple
  **Modbus slave simulator**.

## Project files

`Save project` downloads a JSON file containing port settings, view mode, and
all send/receive sequences. `Load project` restores everything — commit these
JSON files to the repo to share test packages with the team.

---
© TESR — Thai Embedded System and Robotics / TESR Academy
