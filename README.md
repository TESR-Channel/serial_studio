# TESR Serial Studio

**Version 2.0.0** (19 Nov 2026)

A **web serial monitor** by Thai Embedded System and Robotics (TESR).
Runs 100% in the browser (no install, no backend) using the **Web Serial API**.

![theme](Logo_Red-No-Background.png)

## How the screen is organised

- **Top: connect.** Pick the port and baud rate, press **Connect**. Data bits,
  parity and stop bits sit behind the **8N1** button, since most devices never
  need them changed.
- **Middle: monitor.** Everything sent and received, shown as
  ASCII / HEX / DEC / BIN. Switching the format re-draws the whole log.
- **Bottom: send bar.** Type HEX or ASCII and press Enter.
- **Left: tools.** Each tool is a card with a switch. Leave them off for a plain
  serial monitor, switch on only what you need.

## Features

- **Connect to any serial port** — USB-UART, RS485 adapters, Arduino, STM32, ESP32…
- **Cross-platform**: Windows, Linux, macOS, Raspberry Pi (any Chromium-based browser)
- **4 display/edit modes**: ASCII / HEX / Decimal / Binary (Docklight style)
- **Send bar** with a line-ending picker for ASCII (none, LF, CR, CR+LF) and a
  one-click **CRC16** button when the Modbus tool is on
- **Tool: Send sequences** — named packets, per-sequence edit mode, optional auto
  CRC16 append, periodic repeat (polling)
- **Tool: Auto reply** (receive sequences) — pattern match on incoming data with
  highlight + automatic answer (slave simulation)
- **Tool: Modbus RTU** — frames split by silence gap, CRC16 verify,
  function-code names, register values, exception decoding
- **Remembers your setup** — sequences, rules and settings are kept in the browser
- **Save / Open project** as JSON (like Docklight `.ptp`) — sequences + port settings
- **Save log** to a text file
- **Light and dark themes** in TESR red and gold

## Deploy on GitHub Pages

1. Create a repository, e.g. `tesr-serial-studio`
2. Upload `index.html`, `Logo_Red-No-Background.png`, `README.md`
3. Repo **Settings → Pages → Source: Deploy from a branch → main / (root)**
4. Open [https://tesr-channel.github.io/serial_studio/](https://tesr-channel.github.io/serial_studio/)

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

- Switch on the **Modbus RTU** tool. Incoming bytes are grouped into
  frames using the **Frame gap** silence timeout (default 10 ms — raise it
  for slow baud rates, e.g. ~4 ms per character at 9600 baud).
- In a send sequence, enter only `ID FC DATA...` (e.g. `01 03 00 00 00 0A`) and
  switch on **Add a Modbus CRC16 checksum** — the CRC is calculated for you on
  every send. The send bar has the same option as the **+ CRC16** button.
- An Auto reply rule with an answer + CRC lets the page act as a simple
  **Modbus slave simulator**.

## Project files

**Save** (under Project, bottom left) downloads a JSON file containing port
settings, view mode, which tools are on, and all send sequences and auto reply
rules. **Open** restores everything — commit these JSON files to the repo to
share test packages with the team. Project files saved by v1.0 still open.

## Version history

The version number lives in one place, `APP_VERSION` near the top of the script
in `index.html`. It is shown next to the title; click it for the release notes.

### 2.0.0 — 19 Nov 2026

- New layout: connect at the top, monitor in the middle, send bar at the bottom
- Send sequences, Auto reply and Modbus RTU are separate tools you switch on
  only when you need them
- Data bits, parity and stop bits live behind one 8N1 button
- Switching ASCII / HEX / DEC / BIN now re-draws the whole log
- Line-ending picker for ASCII sends, and a CRC16 button when Modbus is on
- Light and dark themes
- Sequences and settings are remembered in this browser
- Fixed: sequence send buttons stayed disabled after connecting

### 1.0

- First release

---
© TESR — Thai Embedded System and Robotics / TESR Academy
