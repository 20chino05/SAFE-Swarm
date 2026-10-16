# Legacy: SAFE-Swarm

> **Archived October 16, 2026.** The team switched from SAFE-Swarm (a two-drone
> search-and-rescue swarm) to Open Herd. This folder keeps the SAFE-Swarm files
> as they were on that date, for reference. Nothing here describes Open Herd.
> See the [repository README](../README.md) for the current project.

## Documents

> **First draft.** The team first meets on October 12, 2026, so nothing here has been agreed yet. The proposal is a hypothetical draft, and its hardware parts are researched candidates, not final choices.

| File | What it is | Status |
|---|---|---|
| [EECS 159 - Project Proposal.pdf](EECS%20159%20-%20Project%20Proposal.pdf) | Fall Project Proposal #1 | **Latest draft.** Proposes scope, roles, a timeline, and a rough per-drone parts estimate (table on pages 3–4). |
| [architecture.md](architecture.md) | Proposed components, data flow, interfaces, and open questions | Draft |
| [tasks.md](tasks.md) | Weekly tasks, proposed owners, and status | Draft |
| [meeting-notes.md](meeting-notes.md) | Meeting notes and decisions | First meeting: October 12, 2026 |
| [Parts List - Original.pdf](Parts%20List%20-%20Original.pdf) | Execution plan and parts list dated October 7, 2026 | **Earlier concept.** Differs from the draft proposal. |
| [Parts List (Revised Oct 10, 2026).pdf](Parts%20List%20%28Revised%20Oct%2010%2C%202026%29.pdf) | Revision of the October 7 plan | **Earlier concept.** Differs from the draft proposal. |

## About the earlier parts lists

Both describe an earlier three-drone concept: one ArduPilot "mother" drone, two
small ESP32 "worker" drones, AI running on a ground laptop, a $300 budget, and a
local LLM. The draft proposal instead describes two drones with onboard AI.

Don't treat these files as the latest parts list. The team may still choose to
reuse parts of them, such as the flight-authorization steps or communication notes.

## Original project README

The repository's front page as it was before the switch.

### SAFE-Swarm
Search and FInd Emergency Swarm

UCI EECS 159 Senior Design | Fall 2026 – Winter 2027

> **First draft.** The team first meets on October 12, 2026, so nothing here has been agreed yet. The proposal is a hypothetical draft, and its hardware parts are researched candidates, not final choices.

#### Overview
SAFE-Swarm is a proposed two-drone search-and-rescue system.
Users would specify a search area, and the drones would coordinate
search routes, detect humans using onboard AI, and report detections.

#### Current Status
Concept development and initial setup. Hardware selection,
software interfaces, and implementation details are still to be decided.

#### Team
- Nader Guirguis — Hardware
- Samuel Malak — Hardware
- Devin Mccaw — Software
- Aaron Torres — Software

Faculty Advisor: Boris Vaisband

#### Proposed System
- Flight controllers for stabilization and waypoint navigation
- Onboard AI processing for camera-based human detection
- Wireless communication for commands, telemetry, and detection reports
- Mission software for search-area input and coordinated route assignment

Exact components and connections remain subject to validation.

#### Development Plan
In the draft proposal, Fall quarter would focus on prototype
development, AI evaluation, communication testing, and simulated
navigation.

Winter quarter would focus on hardware/software integration,
coordinated search testing, and the final demonstration.

#### Documentation
- [Draft project proposal](EECS%20159%20-%20Project%20Proposal.pdf): proposed scope, roles, timeline, and rough parts estimate
- [System architecture](architecture.md): proposed components, interfaces, and open questions
- [Tasks](tasks.md): weekly tasks, proposed owners, and status
- [Meeting notes](meeting-notes.md)
- [All documents](#documents): also lists two earlier parts lists, which describe a three-drone concept that differs from the draft proposal

#### Initial Tasks
- Establish the shared repository
- Document system architecture and communication interfaces
- Evaluate human-detection models
- Set up single-drone flight simulation
- Finalize component selection and budget

Proposed owners and status are tracked in [tasks.md](tasks.md). Some owners, including the hardware tasks and the parts list and budget, are still to be chosen.
