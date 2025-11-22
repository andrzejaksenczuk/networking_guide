# Networking Guide. CCNA in a Nutshell.

**Supplementary Materials & Lab Repository**

This repository contains all supporting materials for the book
**Networking Guide. CCNA in a Nutshell** — a practice-oriented introduction to computer networks designed for beginners and intermediate learners preparing for CCNA-level skills.
The repository includes ready-to-use Packet Tracer labs, solved exercises, cheat sheets, and infrastructure-as-code examples for deploying small teaching networks.

---

## About the Book

The book **Networking Guide. CCNA in a Nutshell.** provides a hands-on approach to networking with short theory chapters and practical exercises. Each lab is referenced in the book and can be run independently.
Topics include:

- Network fundamentals, OSI & TCP/IP models
- Switching, VLANs, STP, EtherChannel
- Routing basics (static & dynamic)
- IPv4/IPv6 addressing
- WLAN introduction
- IP services
- Security fundamentals (ACLs, DHCP Snooping, Port Security, VPN basics)
- Automation fundamentals

The GitHub repository extends the book with complete labs, answers, downloadable examples, and additional study materials.

---

## Repository Structure

`labs/packet_tracer directory` 

Contains all .pkt files referenced throughout the book:

* Initial files — used during exercises
* Final files — show the expected end-state configuration

Labs are named consistently and follow the order of chapters.

`appendix`

* A-answers.md – solutions to selected end-of-chapter problems
* Cheat Sheets – quick references for common commands, addressing rules, encapsulations, packet flow, and more

`ci`

The ansible project provides a minimal reproducible environment with core network services:

* DHCP
* DNS
* NTP
* Logging
* others

Useful for classroom setups or custom lab environments.

---

## How to Use These Materials

### Recommended workflow

1) Read the one-page concept in the book.
2) Open the related Packet Tracer lab from /labs/packet_tracer/.
3) Perform the configuration following the task description.
4) Compare your result with the final solution.
5) Check your understanding using the questions and answers.

### CLI & Formatting Conventions

* IOS comments use !
* User shell: #
* Global config mode: (config)#
* Submodes: (config-if)#, (config-vlan)#, etc.
* Some examples omit enable and configure terminal for brevity. If the device rejects a command, enter these first.

## Requirements

To use the materials you will need Cisco Packet Tracer (student or instructor version). Any text editor for reading Markdown (VSCode recommended) will also be useful. Optionally, a Linux host or VM if you want to run the ansible CI environment

---

## License & Attribution

* **License**: © [2026] Wrocław University of Science and Technology. All rights reserved.
This material is copyrighted by Wrocław University of Science and Technology. Permission is granted for educational and research use, provided that proper attribution is given.
* **Attribution format**: “© 2026 dr inż. Andrzej Aksenczuk, dr hab. inż. Michał Mazur”
* **Trademarks**: “Cisco, Packet Tracer and other marks are trademarks of their respective owners. Use of these names does not imply endorsement.”
