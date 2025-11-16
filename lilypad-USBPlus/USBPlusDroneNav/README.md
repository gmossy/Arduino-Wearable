# LilyPad USB Plus Drone Navigation Demo (USBPlusDroneNav)

This folder contains the **drone-focused** navigation light demo for the
**SparkFun LilyPad USB Plus**.

- Sketch: `USBPlusDroneNav.ino`
- Board: SparkFun LilyPad USB Plus (`SparkFun:avr:LilyPadProtoUSB`)
- Author: Glenn Mossy

Use this demo when you want to mount a LilyPad USB Plus on a small drone
and give it a simple, programmable RGB "nav light" for night flights and
visibility tests.

> **Note:** This pattern is for learning and experimentation. It does
> **not** claim to satisfy any official FAA/FCC or aviation lighting
> requirements. Always follow your local regulations and the drone
> manufacturer's safety guidance.

---

## What This Demo Does

`USBPlusDroneNav.ino` uses the **built-in RGB LED** on the LilyPad USB
Plus (pins `12`, `13`, `14`) to create a navigation-style effect:

- Continuous **low-level "position" glow**
  - A red/green mix (amber-ish) that slowly pulses brighter and dimmer.
  - Implemented as a triangle-wave brightness pattern.
- Periodic **bright white strobe**
  - A short, high-intensity flash layered on top of the glow.
  - Helps draw attention to the drone from a distance.

This makes the board easy to spot in low light while still keeping the
pattern visually appealing and simple to reason about in code.

---

## Device and Pin Info

- **Microcontroller**: ATmega32U4 with Arduino bootloader.
- **Built-in RGB LED pins**:
  - Red: `12`
  - Green: `13`
  - Blue: `14`
- **Power**:
  - Can be powered from USB or from a single-cell LiPo via the JST
    connector and on-board charger.

### Suggested mounting on a drone

- Attach the LilyPad USB Plus securely to the **top or rear** of the
  drone frame using Velcro, double-sided tape, or sewn into fabric
  wrapped around the frame.
- If using a LiPo battery:
  - Secure the battery so it cannot contact props or sharp edges.
  - Route wires away from motors and props.

---

## MacBook + Windsurf Workflow (Drone Demo)

This assumes you already have the repo checked out at
`/Users/gmossy/Arduino_Lillypad` and are using **Windsurf** on macOS.

### 1. Install Arduino CLI (if you haven't already)

```bash
brew update
brew install arduino-cli
```

Or see the official docs:

<https://arduino.github.io/arduino-cli/latest/installation/>

### 2. Configure Arduino CLI for LilyPad USB Plus

```bash
arduino-cli config init
arduino-cli config add board_manager.additional_urls \
  https://raw.githubusercontent.com/sparkfun/Arduino_Boards/master/IDE_Board_Manager/package_sparkfun_index.json
arduino-cli core update-index
arduino-cli core install SparkFun:avr

# Confirm the LilyPad USB Plus board definition exists
arduino-cli board listall | grep -i "lilypad usb plus"
```

### 3. Open the Drone Project in Windsurf

1. In Windsurf, open the folder `Arduino_Lillypad`.
2. Navigate to and open:
   - `lilypad-USBPlus/USBPlusDroneNav/USBPlusDroneNav.ino`
   - This `README.md` for reference.
3. Use the **integrated terminal** for all CLI commands.

### 4. Connect the LilyPad USB Plus to Your MacBook

1. Plug the LilyPad USB Plus into your MacBook with a **data-capable
   micro‑USB cable**.
2. Slide the **ON/OFF switch** to **ON**.
3. If the port does not appear, **double-tap RESET** on the board.
4. List attached boards:

```bash
arduino-cli board list
```

You should see a line similar to:

```text
/dev/cu.usbmodem1431301  serial  Serial Port (USB) LilyPad USB Plus SparkFun:avr:LilyPadProtoUSB SparkFun:avr
```

In this case, the port name is:

```text
/dev/cu.usbmodem1431301
```

---

## Build and Upload the Drone Nav Demo

From the repo root (`/Users/gmossy/Arduino_Lillypad`):

### 1. Compile the sketch

```bash
arduino-cli compile \
  --fqbn SparkFun:avr:LilyPadProtoUSB \
  lilypad-USBPlus/USBPlusDroneNav
```

You should see output showing program and memory usage with no errors.

### 2. Upload to the LilyPad USB Plus

```bash
arduino-cli upload \
  -p /dev/cu.usbmodem1431301 \
  --fqbn SparkFun:avr:LilyPadProtoUSB \
  lilypad-USBPlus/USBPlusDroneNav
```

If your Mac shows a different port, replace `/dev/cu.usbmodem1431301`
with the value from `arduino-cli board list`.

---

## What to Look For on the Drone

Once the sketch is running you should see:

1. A **soft pulsing amber glow** from the built-in RGB LED as the base
   "position" light.
2. A **brief bright white flash** every so often on top of that glow.

Mounted on a drone, this gives you:

- Better visual orientation when flying in low light.
- A simple starting point to discuss navigation lighting concepts and
  embedded timing patterns.

---

## Ideas for Extensions

- Change the colors or strobe timing to match your drone's main lights.
- Add additional external LEDs wired to the LilyPad sew tabs to create a
  front/back or left/right pattern.
- Add a serial protocol (over USB) to allow live configuration of pulse
  and strobe timing while the drone is on the bench.

---

Enjoy experimenting with the LilyPad USB Plus as a tiny, programmable
navigation light for your drone projects!
