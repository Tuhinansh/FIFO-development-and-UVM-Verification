# FIFO-development-and-UVM-Verification
This is a Constrained-Random UVM Verification of a Synchronous FIFO with Scoreboard, Coverage &amp; Assertions


A FIFO (First-In First-Out) buffer ensures that data is read in the same order it is written.
This project verifies FIFO behavior using a full UVM environment and SystemVerilog Assertions.

FIFO Features

8-bit data width

4-entry depth

Write/Read enable logic

Full & Empty flag generation

Pointer & count-based control

Verified Scenarios

Random read/write sequences

Overflow condition (write when full)

Underflow condition (read when empty)

Reset functionality

Data integrity (order maintained)

Coverage and scoreboard checks


                          ┌───────────────────┐
                          │   test.sv         │
                          │ Starts UVM test   │
                          └─────────┬─────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │     env.sv          │
                         │Builds all UVM comps │
                         └───────┬─────────────┘
                                 │
     ┌───────────────────────────┼────────────────────────────┐
     ▼                           ▼                            ▼
┌───────────┐           ┌────────────────┐          ┌─────────────────┐
│ sequencer │           │    driver      │          │    monitor      │
│ Sends     │──────────▶│Drives FIFO DUT │──writes──│Observes signals │
│ seq_items │           │ via interface  │          │Creates analysis │
└─────┬─────┘           └────────────────┘          └─────────┬───────┘
      │                                                       │
      │                                                       ▼
      │                                          ┌─────────────────────┐
      │                                          │   scoreboard        │
      │                                          │Checks DUT vs model  │
      │                                          └─────────┬───────────┘
      │                                                    │
      │                                                    ▼
      │                                          ┌─────────────────────┐
      │                                          │      coverage        │
      │                                          │Tracks scenarios      │
      │                                          └─────────────────────┘
      │
      ▼
┌──────────────┐
│ sequence.sv  │
│ generates    │
│ read/write   │
│ patterns     │
└──────────────┘

                     ┌────────────────────────┐
                     │ fifo_assertions.sv     │
                     │ (no write when full,   │
                     │  no read when empty)   │
                     └────────────────────────┘
