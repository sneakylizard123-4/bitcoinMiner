# BitcoinMiner

A Bitcoin mining board based on the BM1370 ASIC with WiFi capabilities using the onboard ESP32

---

## Key Features

- BM1370 ASIC
- ESP32-S3 Controller
- TLV75733 1A 3.3v bus
- TLT75712 1A 1.2v bus
- MCP1824T-0802E 0.8v bus
- SN74LVC1T45DBV Logic Translator
- EMC2101 Fan Controller
- TPS546D24ARVFR 20A 1.2v ASIC Power

---

## Bill of Materials

### ICs

| Ref | Value | Description |
|-----|-------|-------------|
| U5 | BM1370 | SHA-256 ASIC miner |
| U10 | ESP32-S3-WROOM-1 | WiFi/BLE controller module |
| U12 | TPS546D24ARVFR | 20A 1.2V DC/DC for ASIC |
| U3 | TLV75712PDBV | 1A 1.2V LDO |
| U9 | TLV75733PDBV | 1A 3.3V LDO |
| U4 | MCP1824T-0802E | 0.8V LDO |
| U6, U7, U8 | SN74LVC1T45DBV | Logic level translator (x3) |
| U11 | EMC2101 | Fan controller w/ temp sensing |
| U13 | DP83848I | Ethernet PHY |
| U2 | 25MHz | ASIC oscillator |

### Passives

| Ref | Value | Qty |
|-----|-------|-----|
| C1-C28, C29-C31, C38, C42, C44, C58 (bm1370) | 1uF | 28 |
| C3, C23-C28, C33, C36, C37, C45, C48, C60-C71 | 0.1uF | 24 |
| C54-C57 | 100uF | 4 |
| C34, C40, C41 | 47uF | 3 |
| C51-C53 | 22uF | 3 |
| C32, C39 | 10uF | 2 |
| C58, C59 (ethernet) | 14pF | 2 |
| C35, C43, C46, C47, C49, C50, C72 | misc | 7 |
| R1, R2, R3 | 1K | 3 |
| R22, R23, R26-R29 | 49.9 | 6 |
| R4, R8, R21, R25 | 10K/10k | 4 |
| R5, R6 | 100 | 2 |
| R33, R34 | 330 | 2 |
| R30, R31 | 2.2K | 2 |
| R7, R10, R12, R13, R17, R18, R19, R20, R24, R32 | misc (5.6K, 3.74k, 8.25k, 14.7k, 11.8k, 68.1k, 10, 1, 1.5K, 4.87K 1%) | 10 |
| R11, R14, R15 | net-tie | 3 |
| L1 | 300nH SLC1175-271MEC_COC | 1 |

### Connectors

| Ref | Value | Description |
|-----|-------|-------------|
| J1 | 54-00164 | DC Barrel Jack, 2.0x5.5mm |
| J4 | USB-C 14P | USB 2.0 receptacle |
| J8 | RJ45 Bel SI-60062-F | Ethernet |
| J2 | TC2030-IDC | Tag-Connect debug header |
| J3 | 1x06 | Pin header |
| J5, J6, J7 | 1x04 | Pin headers (x3) |

### Other

| Ref | Value | Description |
|-----|-------|-------------|
| SW1, SW2 | SW_Push | Push buttons (boot/reset) |
| Y1 | 25MHz | Crystal |

---

## Usage

1. Populate the board per the Bill of Materials and assembly data.
2. Power the board via the DC barrel jack (J1).
3. Connect to the serial debug header (J2) or USB-C to flash the ESP32-S3.
4. Connect a WiFi Network for pool communication via ESP32-S3 Module.
5. Attach a cooling fan to the EMC2101 fan header (J7).

---

## Images

> Add renders here: `images/pcb-layout.png`, `images/schematic.png`, `images/3d-model.png`

### PCB Layout

![PCB Layout](images/pcb-layout.png)

### Schematic

![Schematic](images/schematic.png)

### 3D Model

![3D Model](images/3d-model.png)

---
