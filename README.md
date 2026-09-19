# Sequence Detector Verification

A **SystemVerilog RTL and functional verification** project for a **11011 Mealy Sequence Detector**. The project demonstrates finite state machine (FSM) design and a modular verification environment using transaction-based verification techniques, assertions, scoreboarding, and functional coverage.

## Overview

The design implements a **5-state Mealy FSM** that detects the binary sequence **11011**. The output `dout` is asserted for one clock cycle when the final `1` of the sequence is received. The RTL uses a reusable package (`fsm_pkg.sv`) for state definitions and separates sequential (`always_ff`) and combinational (`always_comb`) logic for a clean and synthesizable implementation.

## Project Structure

```text
Sequence_Detector_Verification/
├── rtl/
│   ├── fsm_pkg.sv
│   └── sd11011_mealy_pure.sv
├── tb/
│   ├── testbench_top.sv
│   ├── test.sv
│   ├── env.sv
│   ├── agent.sv
│   ├── generator.sv
│   ├── driver.sv
│   ├── monitor.sv
│   ├── scoreboard.sv
│   └── transaction.sv
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

The verification environment incorporates the following SystemVerilog verification concepts:

1. **Constraint Randomization** – Generates randomized `din` values to exercise diverse input scenarios.
2. **Transaction Class** – Encapsulates stimulus and expected response into reusable transaction objects.
3. **Mailbox Communication** – Uses `gen2drv` and `mon2scb` mailboxes for synchronized communication between components.
4. **Generator** – Creates randomized transactions and forwards them to the driver.
5. **Driver with Virtual Interface** – Applies transactions to the DUT through a virtual interface on clock edges.
6. **Parallel Execution (`fork...join`)** – Executes verification components concurrently.
7. **Monitor** – Passively observes DUT signals and converts them into transactions.
8. **Scoreboard** – Compares DUT outputs against expected outputs from the reference model.
9. **Reference Model** – Uses a 5-bit shift-register model to predict the expected detection output.
10. **Immediate & Concurrent Assertions** – Verifies both procedural and temporal correctness during simulation.
11. **Functional Coverage** – Measures coverage of input patterns, sequence occurrences, and detection events.
12. **Covergroups** – Collects functional coverage during simulation.
13. **Coverpoints** – Tracks important signals such as `din` and `detect`.
14. **Cross Coverage** – Analyzes combinations of `din` and `detect` to ensure meaningful input-output scenarios are exercised.

## Documentation

A detailed explanation of the RTL implementation, verification environment, assertions, and coverage methodology is available in `REPORT.pdf`.
