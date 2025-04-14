# OS Process Scheduling Simulator 

This project simulates process scheduling in an operating system using a multi-level feedback queue (MLFQ) scheduler, shared memory, and message queues.

## Overview

- **OSS (Scheduler):**
  - Manages a simulated system clock using shared memory.
  - Maintains a process table (PCB) with scheduling details.
  - Launches worker processes at random simulated intervals.
  - Dispatches processes using an MLFQ with three levels:
    - Level 0: Base time quantum (10 ms)
    - Level 1: 2 × base quantum
    - Level 2: 4 × base quantum
  - Logs detailed scheduling events to a log file and outputs periodic snapshots of the process table and queues.

- **Worker Processes:**
  - Wait for a scheduling message from OSS.
  - Simulate execution by choosing one of three outcomes:
    - Run for full quantum
    - Use part of the quantum (simulate I/O block)
    - Terminate early
  - Respond back to OSS through a message queue.

## Build and Run

1. **Build the Project:**

   ```bash
   make
   ```

2. **Run OSS:**

   ```bash
   ./oss -n 100 -s 18 -i 100 -f oss.log
   ```

   OSS will launch up to 100 processes (with an 18-process concurrency limit) and log the scheduling events to `oss.log`.

## Cleanup

All IPC resources (shared memory and message queues) are cleaned up upon termination, ensuring no leftover resources.