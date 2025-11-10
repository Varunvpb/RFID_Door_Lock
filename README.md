# RFID_Door_Lock
ESD 
# PassTa – Dual Authentication Access Control System

A secure RFID + Password-based access control system developed on the **LPC1768 ARM Cortex-M3** platform. PassTa combines contactless RFID authentication with PIN-based keypad entry for enhanced physical security.

---

## Overview

PassTa introduces **two-factor authentication** to prevent unauthorized entry. The system verifies a **registered RFID tag** along with a **user-entered 4-digit PIN** before granting access. A 16×2 LCD provides real-time feedback, while LEDs visually indicate authentication results.

This project demonstrates essential embedded systems concepts including GPIO interfacing, keypad scanning, SPI communication, and secure authentication logic.

---

## Features

-  Dual security: RFID + Password authentication  
-  LCD feedback for user guidance  
-  LED status indication for access granted/denied  
-  Real-time keypad scanning with masked input  
-  Auto reset after each authentication attempt  
-  Secure PIN comparison stored in MCU memory  

---

## Hardware Components

| Component | Description |
|----------|-------------|
| LPC1768 Microcontroller | ARM Cortex-M3 core, handles all logic |
| MFRC522 RFID Reader | Reads card UID via SPI |
| RFID Tags/Cards | Contactless authentication input |
| 4×4 Matrix Keypad | PIN entry |
| 16×2 LCD Display | Displays messages & prompts |
| LED Array (8 LEDs) | Visual access indication |
| Connecting Wires + Power Supply | Hardware interfacing |

---

## Pin Configuration

### MFRC522 → LPC1768

| RFID Pin | Function | Connected to |
|---------|----------|--------------|
| SDA/SS | SPI Chip Select | P0.6 |
| SCK | SPI Clock | P0.7 |
| MOSI | Data MCU → RFID | P0.9 |
| MISO | Data RFID → MCU | P0.8 |
| RST | Reset | 3.3V|
| GND | Ground | GND |
| VCC | Power | 3.3V |

### Keypad → LPC1768

| Keypad Pin | Direction | LPC Pin |
|------------|-----------|---------|
| Row1–4 | Output | P2.10 – P2.13 |
| Col1–4 | Input (pull-ups) | P1.23 – P1.26 |

### LCD 16×2 → LPC1768 (4-bit)

| LCD Pin | LPC Pin |
|---------|---------|
| RS | P0.27 |
| EN | P0.28 |
| D4–D7 | P0.23–P0.26 |
| RW | GND |

---

## System Architecture

### Authentication Workflow

1️ Scan RFID tag → UID validation  
2️ Prompt & accept 4-digit PIN input  
3️ If both match → Access Granted  
4️ Else → Access Denied  

### LED Patterns

- Success → LEDs run sequential pattern  
- Failure → All LEDs blink together  

---

## Software Functions

| Function | Purpose |
|---------|---------|
| `RFID_Init()` | Initialize MFRC522 reader |
| `read_RFID_UID()` | Request and read RFID UID |
| `scan_keypad()` | Detect keypad key presses |
| `verify_password()` | Compare PIN with stored value |
| `lcd_print()` | Display messages on LCD |

Source code is written in embedded C using LPC17xx drivers.

---

## Usage Instructions

1️) Power ON → LCD shows *Enter Card*  
2️) Scan RFID card  
3️) If valid → LCD prompts *Enter PIN*  
4️) Enter 4 digits (shown as `****`)  
5️) Feedback:
-  Access Granted → LCD + LED success pattern  
-  Access Denied → LCD + LED failure pattern  

After each attempt, system resets automatically.

---


## Technical Specifications

| Parameter | Value |
|----------|------|
| Operating Voltage | 3.3V |
| RFID Frequency | 13.56 MHz |
| Processing Time | <100 ms |
| Max Read Range | 3–5 cm |

---

## Author

Project developed as part of **Embedded System Laboratory** coursework (ICT 3143), Manipal Institute of Technology.


---

##  References

- NXP LPC1768 Datasheet  
- MFRC522 RFID Reader Technical Manual  
- ARM Cortex-M3 Architecture Guide  

---
