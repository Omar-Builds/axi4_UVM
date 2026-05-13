# UVM Verification Environment for AXI4 Memory-Mapped Slave

## Overview
This repository contains a robust, highly modular Universal Verification Methodology (UVM) testbench designed to verify an AXI4-compliant memory-mapped slave interface and an internal 4KB synchronous single-port RAM. The environment utilizes constrained random stimulus, Transaction Level Modeling (TLM), and comprehensive assertion checks to ensure strict adherence to the AMBA AXI4 protocol.

## Architecture & Methodology
The testbench is built from the ground up prioritizing scalability and layered separation:
* **UVM Component Separation:** Drivers, Monitors, Sequencers, and Scoreboards are strictly isolated to prevent layered mistakes and maximize component reusability.
* **Configuration Management:** Hierarchical configuration and resource sharing are managed dynamically using the `uvm_config_db`.
* **TLM Propagation:** Transaction Level Modeling (TLM) ports and exports handle the seamless propagation of AXI sequence items across the entire Test Environment (TE).

## Verification Strategy & Stress Testing
The master sequence is designed to push the Device Under Test (DUT) to its limits. Key verification strategies include:
* **Aggressive Bursting:** The master injects bursts of varying lengths (controlled via `AWLEN`/`ARLEN` and `AWSIZE`/`ARSIZE`) to stress the slave’s state machine and the memory's bandwidth capabilities.
* **Boundary & Alignment Enforcement:** The environment monitors and aggressively tests the 4KB boundary compliance rules and word-aligned (32-bit) memory access requirements, expecting `SLVERR` responses for illegal crossings.
* **Handshake Integrity:** Assertion-based monitors ensure the `VALID`/`READY` handshakes never violate AXI4 protocol rules across all five channels.

## Results & Bug Findings
Subjecting the DUT to high-stress, constrained-random AXI traffic exposed multiple edge-case failures. A total of **4 bugs** were successfully identified and isolated:
* **2 Bugs** in the Memory Module (addressing/storage logic).
* **2 Bugs** in the AXI4 Slave (control/handshake logic).

The environment tracks against rigorous sign-off metrics, targeting 100% Functional, Code, and Assertion coverage.

## Deliverables included
* Complete `.sv` design and testbench source files.
* Automation scripts (`run.do` file).
* Extensive coverage and assertion reports.
