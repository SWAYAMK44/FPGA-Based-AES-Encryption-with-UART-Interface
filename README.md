# FPGA-Based AES-128 Encryption System with UART Interface

This project implements a hardware-based AES-128 encryption system on an FPGA.  
The system receives plaintext data through a UART interface, performs AES encryption in hardware, and transmits the encrypted ciphertext back via UART.

The design is implemented in **Verilog HDL** and synthesized using **Xilinx Vivado**.

The project explores two AES architectures:

• Baseline AES architecture  
• Pipelined AES architecture  

This allows comparison of **throughput, latency, and hardware utilization**.

---

# Project Overview

AES (Advanced Encryption Standard) is a symmetric encryption algorithm widely used in secure communication systems.

Software implementations of AES can be slow for high-speed or real-time applications. Hardware implementations using FPGAs allow:

• Faster encryption  
• Parallel processing  
• Low latency  
• Hardware-level security  

This project demonstrates a **complete FPGA encryption system with real-time communication** through UART.

---

# System Architecture

The overall system architecture is shown below.

The FPGA receives plaintext data from a host computer through UART, encrypts the data using AES-128, and sends the ciphertext back.

---

# Hardware Modules

The complete design is divided into several hardware modules.

### 1. UART Receiver (UART RX)

The UART RX module receives serial data from the host computer and converts it into parallel data that can be processed by the AES core.

Functions:

• Detect start and stop bits  
• Sample incoming serial data  
• Convert serial stream into 8-bit data  
• Signal when a byte has been received  

---

### 2. AES Encryption Core

The AES core performs the encryption process according to the AES-128 standard.

AES operates on a **128-bit block of data** and performs **10 rounds of transformations**.

Each round consists of several operations.

---

# AES Algorithm

AES encryption consists of the following transformations:

### 1. AddRoundKey

The input block is XORed with the round key derived from the key schedule.

---

### 2. SubBytes

Each byte in the state matrix is substituted using an S-box lookup table.

Purpose:

• Provides non-linearity  
• Protects against linear cryptanalysis

---

### 3. ShiftRows

Rows of the state matrix are cyclically shifted.

This spreads the byte influence across columns.

---

### 4. MixColumns

Columns of the state matrix are mixed using Galois Field arithmetic.

This step provides diffusion in the cipher.

---

### AES Encryption Flow

---

# Baseline AES Architecture

The baseline AES architecture performs each round sequentially.

Characteristics:

• Lower hardware resource usage  
• Simpler design  
• Higher latency  

Process:

Each round completes before the next round begins.

---

# Pipelined AES Architecture

The pipelined AES architecture improves throughput by executing multiple AES rounds simultaneously.

Pipeline concept:

Advantages:

• Higher throughput  
• Better performance for streaming data  

Trade-offs:

• Increased hardware usage  
• Slightly more complex design  

---

# UART Communication System

The FPGA communicates with a host computer through UART.

UART parameters typically used:

• Baud rate: 9600 or 115200  
• 8-bit data  
• No parity  
• 1 stop bit  

Data flow:

A Python script is used on the host side to send plaintext data and receive ciphertext.

---

# Verification and Testing

The system was verified using two stages:

### 1. Simulation

The Verilog design was simulated using **Vivado simulation tools**.

Simulation checks:

• Correct AES encryption  
• Correct UART transmission  
• Proper timing behavior  

Test vectors were used to validate AES outputs.

---

### 2. Hardware Testing

After simulation verification, the design was deployed onto the FPGA board.

Testing process:

1. FPGA programmed with generated bitstream  
2. Python script sends plaintext data through UART  
3. FPGA encrypts the data  
4. Encrypted ciphertext returned to PC  

Outputs were compared with expected AES results.

---

# Python Test Script

A Python script was used to interact with the FPGA via serial communication.

# Python libraries used

Pyserial

Typical operations:

• Send plaintext blocks  
• Receive encrypted ciphertext  
• Verify correctness  


---

# Performance Comparison

Two architectures were compared.

| Feature | Baseline AES | Pipelined AES |
|------|------|------|
| Latency | Higher | Lower |
| Throughput | Moderate | High |
| Hardware Usage | Lower | Higher |
| Complexity | Simple | More complex |

The pipelined architecture significantly improves throughput for continuous data encryption.

---

# Tools Used

Hardware Design

• Verilog HDL  
• Xilinx Vivado  

Testing

• Python  
• PySerial  

Concepts

• Digital System Design  
• Hardware Cryptography  
• FPGA Architecture  
• Serial Communication  

---

# Repository Structure

---

# Applications

Possible applications include:

• Secure communication systems  
• Hardware encryption modules  
• Network security hardware  
• Embedded cryptographic processors  
• IoT security systems  

---

# Future Improvements

Possible extensions to this project:

• Implement AES decryption  
• Add support for AES-256  
• Integrate DMA-based data transfer  
• Improve pipeline depth  
• Implement hardware countermeasures against side-channel attacks  

---

# Author

Swayam Kotecha  
Electronics and Communication Engineering  
IIIT Bangalore

GitHub  
https://github.com/SWAYAMK44
