# 🛰️ Edge AI Safety Node

An embedded hardware architecture designed for real-time visual sensing, local edge processing, and automotive CAN Bus communication.

![Schematic Diagram]([<img width="2362" height="1672" alt="SCH_Schematic1_1-P1_2026-08-13" src="https://github.com/user-attachments/assets/616ceb25-2cbc-4753-a03e-f40095992bfb" />
](https://1drv.ms/i/c/e347dccb9c67e9f7/IQDZbSK93Jh2SoxXLgu51y4TAcOOEqeSA_pvKeaowyToPyA?e=xAFhqI)
---

## 📌 System Architecture

This project integrates three dedicated hardware modules into a unified edge computing safety node:

1. **Central MCU:** **STM32F401 (BlackPill)** — Handles main logic execution, system state monitoring, and communication bus routing.
2. **Vision Unit:** **ESP32-CAM** — Performs real-time frame capture and edge detection, communicating with the primary MCU over UART.
3. **Automotive Bus Interface:** **MCP2515 CAN Controller** — Connects the node to high-speed CAN networks (via onboard TJA1050 transceiver) using SPI.

---

## 🔌 Hardware Connections & Interfaces

### 1. ESP32-CAM ↔ STM32F401 (UART)
| ESP32-CAM Pin | STM32 Pin | Function |
| :--- | :--- | :--- |
| `U0T` (Pin 15) | `PA10` | USART1_RX (Transmit -> Receive) |
| `U0R` (Pin 14) | `PA9` | USART1_TX (Receive <- Transmit) |
| `5V` (Pin 8) | `5V` | Primary Power Rail |
| `GND` | `GND` | Common Ground |

### 2. MCP2515 CAN Module ↔ STM32F401 (SPI)
| MCP2515 Pin | STM32 Pin | Function |
| :--- | :--- | :--- |
| `SCK` | `PA5` | SPI1 Clock |
| `SO` (MISO) | `PA6` | SPI1 Master In Slave Out |
| `SI` (MOSI) | `PA7` | SPI1 Master Out Slave In |
| `CS` | `PB6` | Chip Select |
| `INT` | `PB0` | External Interrupt |
| `VCC` | `5V` | Transceiver Power (TJA1050) |
| `GND` | `GND` | Common Ground |

---

## 🛠️ Key Design Considerations

* **Power Plane Distribution:** The ESP32-CAM and MCP2515 transceiver require 5V power rails to prevent brownouts during frame capture and maintain standard CAN voltage differentials.
* **Bus Isolation & Integrity:** SPI signals are routed with dedicated interrupt lines (`PB0`) for event-driven packet reading rather than polling.
* **Common Ground:** All power domains share a low-impedance common ground reference across the system.

---

## 🚀 How to Open schematic Files

1. Open [EasyEDA Pro](https://pro.easyeda.com/).
2. Import the project file from the `/hardware` directory.
3. View or export the schematic and PCB footprints.
