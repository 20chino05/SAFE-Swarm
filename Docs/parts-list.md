# Open Herd – Draft Parts List (v0)

> **Day-0 draft (October 16, 2026).** Built from the team's brainstorm hardware list and voice memo,
> plus a first round of online research. Only the STM32N6 board is reported as bought. (Pay Samuel lol)
> The options below are candidates to look at, not choices. Prices are from store and distributor
> listings seen on October 16, 2026; they change, so check them before ordering.

**Status values:** **Bought** · **To buy** (need is clear, part not chosen) · **To research** · **Maybe**

## Phase 1: Dev board prototype (per device)

| Part | What it's for | Status | Options found so far | Price seen | Notes |
|---|---|---|---|---|---|
| STM32N6 dev board (NUCLEO-N657X0-Q) | Runs the AI | Bought (per the voice memo) | — | ~$75 (ST store) | Confirm the exact board and how many were bought. |
| Camera module | Captures video | To buy, with school funding | ST-supported cameras that plug into the board: B-CAMS-IMX (5 MP color), STEVAL-66GYMAI1 (1.5 MP color), STEVAL-55G1MBI1 (0.56 MP black-and-white) | ~$57–84 depending on module and store | See "Camera" below. |
| LoRa radio module | Sends short messages between devices | To research | RAK3172 or Seeed Wio-E5 (simple text commands over a serial port); SX1262 modules as a backup | ~$7–10 | Needs a 915 MHz antenna too. |
| Wi-Fi module | Maybe, for sending a match photo | Maybe | ESP32-C3 board (e.g. Seeed XIAO ESP32C3) | ~$5 | LoRa is likely too slow for photos (see below). |
| Power | Runs the device | To research | USB-C wall power for the first prototype; battery + charger only if off-grid | Charger board seen at ~$20 | See "Power" below. |
| Case | Protects the device | To research | 3D-printed case indoors; sealed box outdoors | TBD | See "Case" below. |

**Rough Phase 1 cost per device:** about $145–170 for the board, camera, LoRa module, and Wi-Fi
module, before power parts, antenna, case, tax, and shipping. The board is already bought.

**How many devices?** Not decided. Showing devices working together would need at least two.

## Notes on each part

### Dev board
- The NUCLEO-N657X0-Q has a camera connector, but ST's documents suggest the camera does **not**
  come with it (the IMX335 camera comes with the pricier Discovery kit). This would explain the voice
  memo saying both "it does have a camera" and "the camera we will buy."
- It has a built-in programmer/debugger and is powered and programmed over USB-C.
- It has no screen. ST's examples show the camera and AI output on a laptop over USB.
- The STM32N6 chip has no built-in flash memory. Programs go into the board's external flash, set
  with two jumpers. This matters for the custom board too.

### Camera
- The board's camera connector uses MIPI CSI-2. ST's example projects already support the three
  modules listed above on this board, which is the fastest path to a working demo.
- A parallel camera (like the cheap OV2640 or OV5640) is possible with the chip, but ST has no
  example for it on this board, so it would take extra driver work.
- At least one store listed a very long lead time for the B-CAMS-IMX. Check stock before ordering.

### LoRa (and Wi-Fi)
- LoRa is made for short messages: alerts, counts, and status. At the fastest common settings, a
  small 10 KB photo would take about 17 seconds of airtime, and usually much longer. Sending a match
  photo will probably need Wi-Fi.
- Two ways to set up LoRa: devices talk directly to a receiver the team builds ("peer-to-peer"),
  or they use LoRaWAN, which needs a gateway (one listing: ~$234) and network software. Not decided.

### Power
- ST powers the board from USB-C in its examples, so wall power is the simplest start.
- ST measured about 0.27 W for the chip's core alone while running a small AI model. One common
  18650 battery cell (about 12 Wh) couldn't run even that for much more than two days. An off-grid
  device would likely need to sleep between checks, use a bigger battery, or add a small solar panel.
- A ready-made charger board that takes USB or solar input (for example, Adafruit's bq24074 board)
  avoids designing battery charging from scratch.
- The whole device (board + camera + radio) hasn't been measured yet. A USB-C power meter would do it.

### Case
- Indoors, a simple 3D-printed case is probably enough.
- Outdoors: look for an IP65 (dust-tight, handles water jets) or IP67 (survives brief dunking)
  rating, a clear UV-resistant window for the camera, a vent to stop fogging, and room for heat to escape.

## Phase 2: Custom board

The team's own board, replacing the dev board. Its goals are to be cheaper, mass-producible,
easier to tune, and probably smaller. Nothing is designed yet.

It would combine:

- The STM32N6 chip, plus external flash memory (the chip has none built in)
- A camera connector (CSI-2 or parallel, matching Phase 1)
- The LoRa radio
- Power circuitry (USB and/or battery). ST's application note AN6000 covers the chip's power supply options.
- Maybe Wi-Fi

The SAFE-Swarm plan used JLCPCB to make and assemble its custom board. The same or a similar
service could work here.

## Not needed anymore

The SAFE-Swarm drone parts (frame, motors, ESC, flight controller, ELRS radio) aren't part of
Open Herd. The team's notes only mention buying the STM32N6 board. Whether a device needs GPS is
an open question in the proposal.
The old parts lists are in [legacy/](../legacy/README.md).

## Budget

Not set. The voice memo says the camera would be bought with school funding.

## Sources

- Board, camera support, and setup: [STM32N6-GettingStarted-ObjectDetection](https://github.com/STMicroelectronics/STM32N6-GettingStarted-ObjectDetection), [ST's N6 deployment guide](https://github.com/STMicroelectronics/stm32ai-modelzoo-services/blob/main/object_detection/docs/README_DEPLOYMENT_STM32N6.md), [STM32CubeN6](https://github.com/STMicroelectronics/STM32CubeN6)
- Power measured by ST: [x-cube-n6-ai-power-measurement](https://github.com/STMicroelectronics/x-cube-n6-ai-power-measurement/blob/main/Utilities/pwr_scripts/README.md)
- LoRa modules: [RAK3172 datasheet](https://raw.githubusercontent.com/RAKWireless/rakwireless-docs/master/docs/Product-Categories/WisDuo/RAK3172-Module/Datasheet/README.md), [Seeed Wio-E5](https://raw.githubusercontent.com/Seeed-Studio/wiki-documents/docusaurus-version/sites/en/docs/Network/LoRa_Wio_Series/Wio-E5/LoRa-E5_STM32WLE5JC_Module.md)
- Wi-Fi: [Seeed XIAO ESP32C3 (RobotShop)](https://www.robotshop.com/products/seeedstudio-xiao-esp32c3-tiny-mcu-w-wi-fi-ble)
- Charger: [Adafruit bq24074 charger](https://www.adafruit.com/product/4755)
- Camera price example: [B-CAMS-IMX at Digi-Key](https://www.digikey.com/en/products/detail/stmicroelectronics/B-CAMS-IMX/24737934)
- Other prices: ST eStore, Future Electronics, Mouser, Rokland, and Jameco listings, checked October 16, 2026
