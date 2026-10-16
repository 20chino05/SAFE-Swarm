# Open Herd

Privacy-first camera nodes with onboard AI

UCI EECS 159 Senior Design | Fall 2026 – Winter 2027

> **Day-0 draft (October 16, 2026).** The team just switched from SAFE-Swarm to Open Herd.
> Everything here is a starting point for discussion. Nothing is agreed yet.

## Overview

Open Herd is a proposed standalone camera device ("node") that runs AI on the device itself.
Several nodes could work together as a group.

The main idea is privacy: video would be processed on the node and then discarded.
No footage would be stored or sent anywhere. Only small results would leave the node,
such as an alert when something matches or a count of people or cars.
The plan is to make it open source.

The same hardware could run different software for different uses. Ideas so far:

- A privacy-first security alert, as an alternative to networked police cameras such as Flock
- Crowd safety at venues such as games and concerts
- Counting foot or vehicle traffic

Which one becomes the demo hasn't been decided.

## Current Status

Day 0 of the switch. According to the team's notes, one STM32N6 development board has been
bought. Everything else is still being planned.

## Team

Roles are carried over from SAFE-Swarm and may change.

- Nader Guirguis — Hardware
- Samuel Malak — Hardware
- Devin Mccaw — Software
- Aaron Torres — Software

Faculty Advisor: Boris Vaisband

## Documents

- [Draft proposal](Docs/proposal.md): the idea, use cases, phases, and open questions
- [Draft parts list](Docs/parts-list.md): what's bought, what's needed, and options to research
- [Meeting notes](Docs/meeting-notes.md)
- [Legacy: SAFE-Swarm](legacy/README.md): the original drone project, archived October 16, 2026
