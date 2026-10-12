# SAFE-Swarm System Architecture

**Stage:** concept. Nothing on this page has been built or tested yet.
**Last updated:** October 12, 2026
**Source:** [Project proposal](EECS%20159%20-%20Project%20Proposal.pdf) (uploaded October 12, 2026)

Every item is tagged with where it comes from:

- **Proposal**: stated in the current proposal.
- **Discussed**: suggested in planning, but not in the proposal yet. Confirm with the team.
- **Open**: not decided. Needs a team decision, an advisor answer, or a test.

## What the system must do

1. Accept a search area entered by a user. (Proposal)
2. Divide the area into one search route per drone. (Proposal)
3. Fly each route with a flight controller. (Proposal)
4. Detect people in camera images using AI running on the drone. (Proposal)
5. Exchange mission status and detection reports. (Proposal)
6. Demonstrate a coordinated two-drone search in a controlled setting. (Proposal)

## Aircraft

The proposal plans two drones: one "IKEA-style" drone and one custom drone.

| | Drone 1: IKEA-style (Phase 1) | Drone 2: Custom (Phase 2) |
|---|---|---|
| Goal | Fly early with off-the-shelf parts | Compact design on a custom circuit board (PCBA) |
| Flight controller | Pixhawk-type board running ArduPilot (Proposal). Exact model: Open | Custom STM32F405 board (Proposal parts table) |
| AI compute | NUCLEO-N657X0-Q development board for early vision work (Proposal). Whether it flies on Drone 1: Open | Built into the custom design (Proposal). Details: Open |
| Budget in proposal text | About $250 | About $200 |

Parts listed for each drone in the proposal's rough parts table (Proposal):
4-in-1 35 A ESC, four 2004/2000KV brushless motors, 5–6 inch propellers,
BN-880 GPS and compass, ESP32-CAM (OV2640), ESP32 communication module,
4S 3000mAh Li-ion battery, ELRS receiver, wiring, and a 3D-printed frame.
One ELRS transmitter is shared.

Terms:

- **ArduPilot**: open-source flight software. It stabilizes the aircraft and flies waypoint missions.
- **ELRS (ExpressLRS)**: a radio control link. A person holds the transmitter and can fly or disarm the drone by hand.
- **ESC**: electronic speed controller. It drives the motors.

## Data flow

This diagram shows what information moves where. It is **not** a wiring diagram.
Which boards physically connect to which is still Open.

```mermaid
flowchart LR
    subgraph D["Each drone (x2)"]
        CAM["Camera"] -->|images| AI["Onboard AI board"]
        GPS["GPS + compass"] --> FC["Flight controller (ArduPilot)"]
        RX["ELRS receiver"] -->|manual control| FC
        AI -->|"detection: confidence, timestamp"| COM["Communication module (ESP32)"]
        FC -->|"position, flight status"| COM
        COM -->|waypoint assignments| FC
    end
    COM <-->|"drone ID, status, telemetry, detections"| MC["Mission coordination (location Open)"]
    MC <--> UI["User interface: search-area input, status display"]
    TX["ELRS transmitter (safety pilot)"] -.->|radio| RX
```

## Interfaces

| From | To | Data | Status |
|---|---|---|---|
| Camera | AI board | Images | Open: how ESP32-CAM images reach the STM32N6 board (see Open questions) |
| AI board | Mission/communication software | Detection confidence and timestamp | Discuss |
| Flight controller | Mission/communication software | Position and flight status | Discuss |
| Mission software | Flight controller | Waypoint assignments | Discuss |
| Wireless link | Drones and mission coordination | Drone IDs, status, telemetry, detection reports | Discuss |
| ELRS transmitter | ELRS receiver | Manual control by a safety pilot | Proposal |

### Detection reports

A detection report says "drone N saw a person with this confidence at this time."
It can include where the **drone** was at that moment.
The drone's position is **not** the person's exact location on the ground.
Estimating the person's location would need camera angle, altitude, and lens
field of view, and is not in the current proposal.

Suggested split (Discussed; the proposal's Week 8 matches it, but Phase 2 still lists the task as joint):

- **Devin** produces each detection with its confidence and timestamp.
- **Aaron** attaches the drone's position at that time, logs the report, and sends it.
- Both collaborate on the interface between the two.

### Example messages (illustrative only)

These show the kind of fields involved. They are **not** the final format.

```json
{"type": "telemetry", "drone_id": 1, "mission_status": "searching", "latitude": 33.6405, "longitude": -117.8443}
```

```json
{"type": "detection", "drone_id": 1, "confidence": 0.87, "timestamp_ms": 123456}
```

Before these become real, the team needs to define:

- Units for every field (for example, degrees, meters, milliseconds).
- What a timestamp counts from (drone boot, GPS time, or another clock).
- Coordinate conventions (latitude/longitude, altitude reference).
- How often each message is sent.
- The transport (radio link) and its message size limit.

ArduPilot already sends and receives commands and telemetry using **MAVLink**, a
standard drone message protocol. The software talking to the flight controller
will need MAVLink. Whether drone-to-drone and detection messages also use MAVLink,
or a separate format, is Open.

## Open questions

| # | Question | Who decides |
|---|---|---|
| 1 | Where does mission coordination run: a ground laptop, or a board on each drone? | Devin, Aaron, with hardware |
| 2 | How do camera images reach the STM32N6? The ESP32-CAM's camera is wired to its own ESP32 chip, so images would have to be transferred to the N6 over a link the team builds. ST's N6 object-detection example reads from camera modules plugged into the board's camera connector instead. Check its README for supported boards and cameras. | Devin, with hardware |
| 3 | Which exact Pixhawk-type board for Drone 1? Confirm ArduPilot supports it. | Nader, Samuel |
| 4 | Can the custom STM32F405 board run ArduPilot? A new board needs a matching ArduPilot board definition; see the porting guide below. | Nader, Samuel |
| 5 | Which radio link carries mission messages (for example, ESP-NOW or Wi-Fi)? Do drones talk to each other directly, or only through mission coordination? | Aaron, with team |
| 6 | Does the NUCLEO-N657X0-Q fly on Drone 1 in Fall, or stay on the bench? | Team |
| 7 | Budget: the proposal text says about $250 and $200 per drone, but the parts table says $279–319 per drone. The $75 AI board and Drone 1's Pixhawk-type controller are not in the table. Which parts does each drone actually use? | Team |
| 8 | Flight authorization. With a 4S 3000mAh battery, each drone will very likely weigh more than 250 g, which brings FAA registration and Remote ID rules into play. Flights on campus also need UCI EH&S approval. The earlier parts-list documents list these steps; the current proposal does not. | Team, with advisor |

## Scope priorities (Discussed)

Core: flight controllers that ArduPilot supports, an existing lightweight detection
model, simple two-route coordination, telemetry and detection reporting, and
simulation before physical integration.

Stretch: a fully custom flight-controller board, more advanced autonomous behavior.

Targets such as 20-minute flight time or reliable detection from the air are goals,
not results, until they are measured.

## References

These show an implementation path. They do not confirm that the exact proposed hardware works together.

- [STM32N6 object detection getting started (ST)](https://github.com/STMicroelectronics/STM32N6-GettingStarted-ObjectDetection)
- [ArduPilot: porting to a new flight controller](https://ardupilot.org/dev/docs/porting.html)
- [ArduPilot: SITL simulator setup](https://ardupilot.org/dev/docs/SITL-setup-landingpage.html)
