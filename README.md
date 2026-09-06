# BitcoinMiner

A single-BM1370 Bitcoin mining board with onboard ESP32-S3 for wifi and active fan cooling. No external controller board needed!
il add more bm1370s soon trust

![PCB Top](images/pcb-top-angle.png)

![PCB Isometric](images/pcb-iso-right.png)

![PCB Bottom](images/pcb-bottom.png)

---

## Why I Built This

I wanted a single board that handles everything for mining: the ASIC, the controller, networking, and power. The BM1370 is one of the most efficient SHA-256 ASIC right now at ~25 J/TH, and pairing it with an ESP32-S3 gives WiFi, BLE, and enough processing power for mining firmware all in one compact package (in theorey).
Also i dont want to make my gpu suffer, its busy doing even less important stuff

---

## Schematic

![Schematic](images/bitcoinMiner.png)

### Sub-sheets

| Sheet | File | Purpose |
|-------|------|---------|
| Main | `bitcoinMiner.kicad_sch` | Top-level, mounting holes, logo, barrel jack |
| BM1370 | `bm1370.kicad_sch` | ASIC, oscillator, decoupling, level translators |
| Power | `power.kicad_sch` | TPS546D24 20A buck, LDOs, power filtering |
| ESP32 | `esp32.kicad_sch` | ESP32-S3, USB-C, boot/reset, debug header |
| Ethernet | `ethernet.kicad_sch` | DP83848I PHY, RJ45, crystal |
| Fan | `fan.kicad_sch` | EMC2101 fan controller, temperature sensing |

---

## How to Assemble

### Tools Needed
- Soldering iron of course
- Solder paste + reflow oven/hot plate, unless you like small parts hand soldering
- Flux, solder wick, tweezers
- Multimeter for when it doesnt work

### Step-by-step

1. **Paste** - use the stencil to spread solder paste on the board

2. **Place parts** - start with small stuff, then go bigger

3. **Reflow** - Use hot plate or hot air, or maybe even hand solder????

4. **Cool** - Wait until it isnt hot anymore

5. **Power** - Power via the barrel jack, maybe use CC if you have a bench power supply just to make sure nothing explodes

6. **Program** - Flash the bitaxe firmware onto the esp32

7. **Configure** - configure the esp32 so that it can connect to wifi

8. **Test** - test the whole board, make sure it hashes

9. **Heatsink and Fan** - to keep it cool, maybe use thermal paste?

10. **Inspect** - Observe the miner hash

---

## How to Flash

Flash via USB-C (J4) or TC2030 debug header (J2):

1. Install [esptool](https://github.com/espressif/esptool): `pip install esptool`
2. Connect the board via USB-C.
3. Hold **SW1** (boot) and press **SW2** (reset) to enter download mode.
4. Flash: `esptool.py --chip esp32s3 --port /dev/ttyACM0 write_flash 0x0 firmware.bin` make sure to choose correct port!
5. Press **SW2** (reset) to boot.

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
| C58, C59 | 14pF | 2 |
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
| Y1 | 25MHz | Crystal (Ethernet PHY) |

---

## Known Issues

- **Missing 3D models** - ESP32-S3-WROOM-1U, WS2812B LEDs, and HRO USB-C connector footprints don't have STEP models assigned. Won't show in 3D renders or PnP files.

---

## Credits

- [Bitaxe Gamma](https://github.com/bitaxeorg/BitaxeGamma) - reference schematic and BM1370 support circuitry
- [Hack Club](https://hackclub.com/) - funding through Forge
- KiCad - PCB design tool
- Texas Instruments - TPS546D24 datasheet and app notes
