# BitcoinMiner

A single BM1370 board that mines bitcoin

## Custom Features
- BM1370 ASIC miner
- ESP32-S3-WROOM-1/1u-N16R8 MCU for wifi
- 9x WS2812B status LEDs
- Fan controller
- TPS546D24 20A core regulator
- USB-C + TC2030 Tag-Connect

## PCB Design

The board is a 4 layer 100x75mm PCB with a dedicated ground inner layer

![PCB 3D / layout image](images/pcb-top-angle.png)

It is built around the BM1370 ASIC.
it is based on the proven Bitaxe Gamma reference design, and a buck 20A 1.2V core rail.
The ESP32-S3 module provides WiFi/BLE control. It can be programmed through the native USB-C port or the Tag-Connect debug header
The fan controller communicates to the ESP32 via i2C

## Firmware

The firmware is the open-source
see [firmware/](firmware/). 
To enter program mode:
1. Hold BOOT (SW2)
2. Press RESET (SW1)
3. Release BOOT
4. Start flashing

```
pip install bitaxetool
bitaxetool --config firmware/configs/config-bitcoinMiner.csv --firmware firmware/esp-miner-merged.bin
```

## BOM (Bill of Materials)

| Ref | Value | LCSC # | MPN | Manufacturer | Footprint | Qty | Unit $ | Ext $ | Link |
|-----|-------|--------|-----|--------------|-----------|-----|--------|-------|------|
| C1,C2,C4-C22,C58 | 1uF 16V X7R | C59782 | CL10B105KO8NNNC | Samsung | 0603 | 22 | — | — | [LCSC](https://www.lcsc.com/product-detail/C59782.html) |
| C3,C23-C28,C36,C37 | 0.1uF 16V X7R | C66501 | CL10B104KO8NNNC | Samsung | 0603 | 9 | — | — | [LCSC](https://www.lcsc.com/product-detail/C66501.html) |
| C29,C30,C31,C38,C42,C44 | 1uF 16V X5R | C2177690 | EMK105BJ105MV | Taiyo Yuden | 0402 | 6 | — | — | [LCSC](https://www.lcsc.com/product-detail/C2177690.html) |
| C32,C39 | 10uF 16V X5R | C1713 | CL21A106KOQNNNE | Samsung | 0805 | 2 | — | — | [LCSC](https://www.lcsc.com/product-detail/C1713.html) |
| C33,C45,C48,C59-C67 | 0.1uF 16V X5R | C159816 | CL05A104KO5NNNC | Samsung | 0402 | 12 | — | — | [LCSC](https://www.lcsc.com/product-detail/C159816.html) |
| C34 | 47uF 6.3V X5R | C140782 | GRM188R60J476ME15D | muRata | 0603 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C140782.html) |
| C35 | 470pF 50V C0G | C36252 | 0603CG471J500NT | FH | 0603 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C36252.html) |
| C40,C41 | 47uF 16V X5R | C2932477 | CL32A476KOJNNNE | Samsung | 1210 | 2 | — | — | [LCSC](https://www.lcsc.com/product-detail/C2932477.html) |
| C43 | 4700pF 50V X7R | C599603 | C0402C472K5RAC7867 | KEMET | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C599603.html) |
| C46 | 2200pF 50V X7R | C106861 | CC0402KRX7R9BB222 | YAGEO | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C106861.html) |
| C47 | 4.7uF 6.3V X5R | C82453 | GRM155R60J475ME47D | muRata | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C82453.html) |
| C49 | 1000pF 50V NP0 | C152850 | 0805N102J500CT | Walsin | 0805 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C152850.html) |
| C50 | 100pF 50V C0G | C597014 | 04025A101JAT2A | AVX | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C597014.html) |
| C51,C52,C53 | 22uF 10V X5R | C441864 | GRM21BR61A226ME44L | muRata | 0805 | 3 | — | — | [LCSC](https://www.lcsc.com/product-detail/C441864.html) |
| C54-C57 | 100uF 6.3V X5R | C15008 | CL31A107MQHNNNE | Samsung | 1206 | 4 | — | — | [LCSC](https://www.lcsc.com/product-detail/C15008.html) |
| D1,D2 | Green LED 0603 | C12624 | KT-0603G | Hubei KENTO | 0603 | 2 | — | — | [LCSC](https://www.lcsc.com/product-detail/C12624.html) |
| D3-D11 | WS2812B-2020 | C965555 | WS2812B-2020 | Worldsemi | PLCC4 2020 | 9 | — | — | [LCSC](https://www.lcsc.com/product-detail/C965555.html) |
| J1 | DC Barrel Jack 2.0x5.5mm | C431534 | 694106106102 | Wuerth | Through Hole | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C431534.html) |
| J4 | USB-C Receptacle 16P | C165948 | TYPE-C-31-M-12 | Korean Hroparts Elec | SMD | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C165948.html) |
| J6 | Pin Socket 1x4 2.54mm | C2718488 | 2.54-1\*4P | BOOMELE | Through Hole | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C2718488.html) |
| J7 | JST SH 4P 1mm | C160390 | BM04B-SRSS-TB(LF)(SN) | JST | SMD | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C160390.html) |
| L1 | 300nH Shielded Inductor | — | SLC1175-271MEC | Coilcraft | SMD 11x17mm | 1 | — | — | — |
| R1,R3 | 1K 1% | C22548 | RC0603FR-071KL | YAGEO | 0603 | 2 | — | — | [LCSC](https://www.lcsc.com/product-detail/C22548.html) |
| R13 | 14.7k 1% | C4021671 | CRCW040214K7FKTD | Vishay | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C4021671.html) |
| R14 | 0 ohm | C881153 | CR0402J0R00Q10Z | Ever Ohms | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C881153.html) |
| R16 | 3.74k 1% | C2085340 | CRCW04023K74FKED | Vishay | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C2085340.html) |
| R17 | 11.8k 1% | C324858 | RC-02K1182FT | FH | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C324858.html) |
| R18 | 68.1k 1% | C844116 | CRCW040268K1FKED | Vishay | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C844116.html) |
| R19 | 10 1% | C138066 | RC0402FR-0710RL | YAGEO | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C138066.html) |
| R20 | 1 ohm 0.1% sense | C2912606 | HoAR1206-1/4W-1R-0.1% | Milliohm | 1206 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C2912606.html) |
| R8,R21,R24,R25 | 10k 1% | C98220 | RC0603FR-0710KL | YAGEO | 0603 | 4 | — | — | [LCSC](https://www.lcsc.com/product-detail/C98220.html) |
| R22,R23 | 49.9 1% | C482189 | CRCW040249R9FKED | Vishay | 0402 | 2 | — | — | [LCSC](https://www.lcsc.com/product-detail/C482189.html) |
| R4 | 10k 1% | C60490 | RC0402FR-0710KL | YAGEO | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C60490.html) |
| R5,R6 | 100 1% | C100700 | CR0603FA1000G | LIZ | 0603 | 2 | — | — | [LCSC](https://www.lcsc.com/product-detail/C100700.html) |
| R7 | 5.6K 1% | C844799 | CRCW06035K60FKEA | Vishay | 0603 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C844799.html) |
| R9 | 8.25k 1% | C185389 | RC0402FR-078K25L | YAGEO | 0402 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C185389.html) |
| SW1,SW2 | Tactile Switch EVQPU | — | EVQPUM02K | PANASONIC | SMD | 2 | — | — | — |
| U10 | ESP32-S3-WROOM-1N16R8 | C2913202 | ESP32-S3-WROOM-1-N16R8 | ESPRESSIF | SMD WROOM | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C2913202.html) |
| U11 | EMC2101 | C626968 | EMC2101-R-ACZL-TR | Microchip | TSSOP-8 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C626968.html) |
| U12 | TPS546D24ARVFR | C507280 | TPS546D24ARVFR | TI | LQFN-40 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C507280.html) |
| U2 | 25MHz Crystal | C843258 | NX2016SA-25MHZ-STD-CZS-2 | NDK | 2016-4P | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C843258.html) |
| U3 | TLV75712PDBV | C1509296 | TLV75712PDBVR | TI | SOT-23-5 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C1509296.html) |
| U4 | MCP1824T-0802E | C625460 | MCP1824T-0802E/OT | Microchip | SOT-23-5 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C625460.html) |
| U5 | BM1370 | — | BM1370 | Bitmain | LQFP | 1 | — | — | — |
| U6,U7,U8 | SN74LVC1T45DBV | C7843 | SN74LVC1T45DBVR | TI | SOT-23-6 | 3 | — | — | [LCSC](https://www.lcsc.com/product-detail/C7843.html) |
| U9 | TLV75733PDBV | C485517 | TLV75733PDBVR | TI | SOT-23-5 | 1 | — | — | [LCSC](https://www.lcsc.com/product-detail/C485517.html) |
| **Total** | — | — | — | — | — | **116** | — | — | — |

Full CSVs: [LCSC BOM](BOM.csv)
[KiCad generated BOM](kicad/production/bom.csv)
[Pick and place](kicad/production/positions.csv)

## Production

Using JLCPCB
4-Layer
- HASL Lead Free
- 1.6mm thick board

## Credits

- [Bitaxe Gamma](https://github.com/bitaxeorg/BitaxeGamma) - reference schematic and BM1370 support circuitry
- [ESP-Miner](https://github.com/bitaxeorg/ESP-Miner) - firmware this board's target is based on
- [Hack Club](https://hackclub.com/) - funding through Forge