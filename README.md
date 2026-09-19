# Sequence Detector Verification

A **SystemVerilog RTL and functional verification** project for a **11011 Mealy Sequence Detector**. The project demonstrates FSM design and a modular verification environment using transaction-based verification concepts such as constrained randomization, mailboxes, assertions, scoreboarding, and functional coverage.

## Overview

The design implements a **5-state Mealy FSM** that detects the binary sequence **11011**. The output `dout` is asserted for one clock cycle when the final `1` of the sequence is received. The RTL uses a reusable package (`fsm_pkg.sv`) for state definitions and separates sequential (`always_ff`) and combinational (`always_comb`) logic.

## Project Structure

```text
Sequence_Detector_Verification/
├── rtl/
│   ├── fsm_pkg.sv
│   └── sd11011_mealy_pure.sv
├── tb/
│   ├── generator.sv
│   ├── driver.sv
│   ├── monitor.sv
│   ├── scoreboard.sv
│   ├── transaction.sv
│   └── testbench_top.sv
├── outputs/
├── REPORT.pdf
└── README.md
```

## Verification Environment

The verification flow follows a layered architecture:

```text
Generator → Driver → DUT → Monitor → Scoreboard
```

Transactions are transferred between components using mailboxes (`gen2drv` and `mon2scb`), while the driver communicates with the DUT through a virtual interface.

## Verification Concepts Implemented

* **Constraint Randomization** – Generates randomized input bits (`din`) to exercise different input patterns.
* **Transaction Class** – Encapsulates stimulus as reusable transaction objects.
* **Mailbox Communication** – Enables synchronized communication between verification components.
* **Generator & Driver** – Generate and apply randomized stimulus to the DUT.
* **Parallel Execution** – Uses `fork...join` for concurrent execution.
* **Monitor** – Captures DUT activity and forwards transactions to the scoreboard.
* **Scoreboard & Reference Model** – Uses a 5-bit shift register to compare expected and actual outputs.
* **Assertions** – Includes immediate and concurrent assertions for functional correctness.
* **Functional Coverage** – Measures input coverage, sequence occurrences, detection events, and cross coverage.

## Documentation

A detailed explanation of the RTL implementation and verification methodology is available in **REPORT.pdf**.
