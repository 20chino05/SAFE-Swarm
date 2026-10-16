# Open Herd – Draft Parts List (v0)

> **Day-0 draft (October 16, 2026).** Built from the team's brainstorm hardware list and voice memo.
> Only the STM32N6 board is reported as bought. Everything else is a need, not a choice. (Pay Samuel lol)
> Prices are left blank until someone looks them up.

**Status values:** **Bought** · **To buy** (need is clear, part not chosen) · **To research** · **Maybe**

## Phase 1: Dev board prototype (per node)

| Part | What it's for | Status | Options to research | Est. cost | Notes |
|---|---|---|---|---|---|
| STM32N6 development board (probably NUCLEO-N657X0-Q) | Runs the AI on the node | Bought (per the voice memo) | — | ~$75 was the estimate in the SAFE-Swarm proposal; actual price paid not recorded | Confirm the exact board and how many were bought. |
| Camera module | Captures video for the AI | To buy, with school funding (per the voice memo) | MIPI CSI-2 camera or parallel camera (to research) | TBD | The memo says both "it does have a camera" and "the camera we will buy"; confirm. |
| LoRa module | Sends small messages between nodes | To research | To research | TBD | Will likely need an antenna too. |
| Wi-Fi module | Maybe for sending a match image, which may be too big for LoRa | Maybe | To research | TBD | |
| Power | Runs the node | To research | USB power (bench and indoor) or a battery for off-grid use | TBD | A battery would also need charging and protection parts. |
| Enclosure | Protects the node | To research | To research | TBD | |

**How many nodes?** Not decided. A demo of nodes working together would need at least two.

## Phase 2: Custom PCB

The team's own board, replacing the dev board. Its goals are to be cheaper, mass-producible,
easier to tune, and probably smaller. Nothing is designed yet.

It would combine:

- The STM32N6 chip
- A camera connector (CSI-2 or parallel, matching Phase 1)
- The LoRa radio
- Power circuitry (USB and/or battery)
- Maybe Wi-Fi

The SAFE-Swarm plan used JLCPCB to make and assemble its custom board. The same or a similar
service could work here.

## Not needed anymore

The SAFE-Swarm drone parts (frame, motors, ESC, flight controller, ELRS radio) aren't part of
Open Herd. The team's notes only mention buying the STM32N6 board. Whether a node needs GPS is an
open question in the proposal.
The old parts lists are in [legacy/](../legacy/README.md).

## Budget

Not set. The voice memo says the camera would be bought with school funding.
