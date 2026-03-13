# UART Protocol (Verilog)

A simple **Universal Asynchronous Receiver/Transmitter (UART)** implementation in Verilog.  
This project helped me understand serial communication at the RTL level and practice hardware design workflows including simulation and verification.

---

## Introduction

UART (Universal Asynchronous Receiver/Transmitter) is a commonly used **serial communication protocol** that allows two digital devices to exchange data asynchronously — meaning the transmitter and receiver do not share a common clock. In this project, I built a UART transmitter (TX) and receiver (RX) from scratch in Verilog, simulated their behavior with testbenches, and learned how timing and bit framing works in hardware.

---

## Description

UART is fundamental in many embedded systems and peripherals — it’s used everywhere from microcontrollers talking to sensors, to FPGA boards communicating with computers via USB‑UART bridges. UART transmits data **serially** (one bit at a time), adding a *start bit*, *data bits*, optional *parity*, and *stop bits* to each frame. 

While UART is simple in concept, implementing it in hardware deepened my understanding of:
- Asynchronous bit timing and baud rate generation  
- Shift registers and serial‑parallel conversion  
- Finite state machines for TX/RX control  
- Verilog module design and testbench creation  

This project was a hands‑on way for me to explore how communication protocols work **close to the hardware**, not just in software.

---

##  Design Overview

### What this project includes

- **Baud rate generator:** Divides the input clock to create the proper timing for serial data bits.
- **UART receiver (`uart_rx.v`):** Samples incoming bits and reassembles them into parallel data.
- **UART sender (`uart_sender.v`):** Takes 8‑bit parallel data and shifts it out serially with framing bits.
- **Top‑level module (`uart_top.v`):** Hooks RX, TX, and baud generator together.
- **Testbench (`tb.v`):** Verifies UART functionality in simulation.

This design focuses on demonstrating essential UART behavior rather than supporting all advanced features like parity checks, FIFOs, or hardware flow control.

---
## High‑Level Working Overview

1. **Baud Rate Generator:** Divides the main clock to generate a tick signal matching the desired baud rate (e.g., 9600 bps).  
2. **Transmitter (TX):** On a request to send data, it frames the byte with start and stop bits and shifts it out at the baud rate.  
3. **Receiver (RX):** Detects the start bit, samples each incoming bit in the middle of a bit period, and reconstructs the byte.  
4. **Testbench:** Stimulates TX, loops back TX to RX, and checks that sent and received bytes match (simulation). :contentReference[oaicite:3]{index=3}


## Learnings infered

Working on this UART protocol implementation taught me to:
- Translate communication protocol behavior into **RTL logic**
- Write structured Verilog with separation between control (FSM) and data flow
- Use simulation tools effectively for debug and verification
- Think about bit timing, start/stop framing, and asynchronous signaling

This project was a concrete way to practice digital design fundamentals and build confidence with Verilog and simulation workflows.
