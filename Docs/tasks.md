# Tasks

Tasks, owners, and week numbers come from the [project proposal](EECS%20159%20-%20Project%20Proposal.pdf).
The proposal has no calendar dates; the October dates come from the earlier parts-list schedule.
The collaborator task, the simulator choice (ArduPilot SITL), the Week 4 evidence list, and every
Support and Status value come from planning discussion or this draft, not the proposal.

These are planning targets, not estimates checked against hours.
The planning assumption is about 6 hours per person per week.

**Owner** is the one responsible person the course template asks for.
**Support** is anyone who helps. Devin and Aaron collaborate on integration
work; the owner field doesn't change that.

**Status values:**

- **Planned**: scheduled for a later week.
- **Not started**: due now, no work yet.
- **In progress**: work has begun.
- **Done**: finished, with evidence linked (commit, file, screenshot, photo, or measurement).
- **Blocked**: waiting on something; say what.
- **Unknown**: not yet confirmed; ask at the next meeting.

Only mark a task Done when the evidence is linked.

## Week 3 (October 12–16)

| Task | Owner | Support | Status | Evidence / notes |
|---|---|---|---|---|
| Establish the software repository | Aaron | Devin | In progress | Repo created October 12. Proposal and parts lists uploaded. |
| Add Devin, Nader, and Samuel as repository collaborators | Aaron | | Not started | As of October 12, only the owner account (20chino05) is a collaborator, so only it can push. The repo is public, so anyone can view it. |
| Define communication messages and software interfaces | Aaron | Devin | In progress | First draft: [architecture.md](architecture.md). Not yet reviewed by the team. |
| Set up the AI development environment and select an initial human-detection model | Devin | Aaron | Unknown | |
| Complete the proposal | Nader or Samuel (pick one) | All | Unknown | See [Proposal cleanup](#proposal-cleanup) below. |
| Order the STM32N6 development board and camera | Nader or Samuel (pick one) | Devin | Unknown | Check which cameras ST's N6 example supports first (architecture.md, open question 2). |
| Finalize the BOM (bill of materials) for the IKEA-style drone | Nader or Samuel (pick one) | | Unknown | |

## Fall schedule

### Software

| Week | Task | Owner | Status |
|---|---|---|---|
| 4 | Prepare training and test images; run baseline human detection on a computer | Devin | Planned |
| 4 | Set up flight simulation and demonstrate a single-drone waypoint mission (planned tool, from discussion: ArduPilot SITL) | Aaron | Planned |
| 5 | Test camera input on the STM32 development board (depends on parts arriving) | Devin | Planned |
| 5 | Demonstrate command and telemetry exchange between communication modules (depends on parts arriving) | Aaron | Planned |
| 6 | Deploy an initial detection model to the STM32N6 board; record inference performance | Devin | Planned |
| 6 | Search-area division and waypoint assignment for two simulated drones | Aaron | Planned |
| 6 | User-entered search boundaries feeding the simulated search-area division | Aaron | Planned |
| 7 | Improve detection with representative images; document missed and incorrect detections | Devin | Planned |
| 7 | Mission-state tracking, connection monitoring, and communication-loss handling | Aaron | Planned |
| 8 | Detection messages with confidence scores and timestamps | Devin | Planned |
| 8 | Connect detection messages to mission logging; associate them with available drone-position data | Aaron | Planned |
| 9 | Test onboard detection with the prototype camera setup and identify integration issues | Devin | Planned |
| 9 | Test communication with the prototype flight controller; coordinated search in simulation | Aaron | Planned |
| 10 | Demonstrate onboard human detection on the development board or prototype; report measured accuracy and processing speed | Devin | Planned |
| 10 | Demonstrate two-agent search simulation, telemetry exchange, and detection logging | Aaron | Planned |
| 10 | AI documentation and remaining Winter tasks | Devin | Planned |
| 10 | Communication and mission-software documentation and remaining Winter tasks | Aaron | Planned |

Week 4 evidence for the simulation task: a saved waypoint mission file, a
screenshot or recording of the simulated flight, and short progress notes.

### Hardware

The proposal assigns these to Nader and Samuel together. The course template
asks for one owner per task, so pick one lead for each.

| Week | Task | Owner | Status |
|---|---|---|---|
| 5 | First schematic and layout of the custom drone PCBA, ready for review | TBD | Planned |
| 5 | Begin assembling the IKEA-style drone | TBD | Planned |
| 10 | Functioning IKEA-style drone (able to hover) | TBD | Planned |
| 10 | Initial custom drone | TBD | Planned |
| 10 | Trained AI model able to recognize humans in realistic test environments | TBD (listed under hardware in the proposal; overlaps Devin's Week 10 task) | Planned |

## Winter (from the proposal)

Winter deliverable: "An integrated search-and-rescue demonstration supported by measured performance, documented testing, and complete software documentation."

| Phase | Task | Owner |
|---|---|---|
| Early development | Integrate the AI model and camera pipeline onto the custom drone | Devin |
| Early development | Integrate mission commands, telemetry, and communication firmware with both drones | Aaron |
| System testing | Test human detection under representative lighting, viewing angles, and motion | Devin |
| System testing | Test coordinated search assignments, communication-loss behavior, and mission tracking | Aaron |
| Final demonstration | Validate onboard detection; document final performance | Devin |
| Final demonstration | Demonstrate two-drone search coordination and detection reporting, subject to flight readiness | Aaron |
| Final demonstration | Finalize AI source code, test results, and documentation | Devin |
| Final demonstration | Finalize communication and swarm source code, test results, and documentation | Aaron |
| Hardware | Integrate the AI stack with the custom drone | TBD (Nader or Samuel) |
| Hardware | "Fully tested" (the proposal does not say what scope) | TBD (Nader or Samuel) |

## Proposal cleanup

Checked against the proposal PDF uploaded October 12.

- [ ] Replace "Assumption is that both of us has the knowledge to do any of these things, but roles are assigned in case" with: "Devin and Aaron will collaborate, with initial responsibilities assigned below."
- [ ] Phase 2 lists "Package detection results with timestamps and associated drone position" as (Devin/Aaron). Week 8 already splits it: Devin produces detection messages with confidence scores and timestamps; Aaron connects them to mission logging and associates them with available drone-position data. Make Phase 2 match.
- [ ] Phase 2 also lists "Integrate camera input and human detection with the custom drone hardware" as (Devin/Aaron). The template says to split multi-person tasks into sub-tasks with one owner each.
- [ ] Budget: Phase 1 text says about $250 and Phase 2 says about $200, but the parts table says $279–319 per drone. The $75 NUCLEO-N657X0-Q is not in the table. The table lists a custom STM32F405 flight controller, while the Phase 1 IKEA-style drone is described as using PixHawk and ArduPilot and points to the table ("part breakdown below"). Separate shared development equipment from parts each drone carries.
- [ ] Hardware tasks list "(Nader and Samuel)". The template says "assign each task to 1 responsible member", so name one lead per task.
- [ ] Formatting: remove doubled bullets ("- -") and empty bullets in the timeline. Move "WINTER DELIVERABLE" out from between the software heading and Phase 1.
- [ ] Optional: the "Visual Representation" image shows three drones; the plan is two.
- [x] Search-area input appears in the Phase 1 list and in Week 6.
