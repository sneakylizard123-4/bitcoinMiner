# bitcoinMiner Firmware

ESP32-S3 mining firmware for the bitcoinMiner board, based on the open-source
[bitaxe ESP-Miner](https://github.com/bitaxeorg/ESP-Miner) firmware (GPL-3.0,
ESP-IDF v6.0.x). The entire upstream tree is vendored under `firmware/` with a
custom **BitcoinMiner** board target added, so the board tunnels a single
BitMiner BM1370 ASIC at ~525 MHz / 1.15 V core like a Bitaxe Gamma.

## Board target

Added to the upstream ESP-Miner:

| File | Change |
|------|--------|
| `main/device_pins.h` / `main/device_pins.c` | `BITCOINMINER_I2C_PINS` (SDA=48, SCL=47) |
| `main/device_config.h` | `BITCOINMINER` family + `board_version = "bitcoinMiner"` config |
| `configs/config-bitcoinMiner.csv` | NVS config flashed with `bitaxetool` |

Board version string: **`bitcoinMiner`**

### How the board is selected

`device_config_init()` (in `device_config.c`) looks up `boardversion` from NVS
against `default_configs[]`. The `bitcoinMiner` entry selects:

- Family `BitcoinMiner`: 1x BM1370, default 525 MHz, 1150 mV, 128 cores, 4 hash domains
- `BITCOINMINER_PINS`: I2C SDA=GPIO48, SCL=GPIO47 (EMC2101 at 0x4C, TPS546D24 at 0x24 on PMBus)
- `EMC2101` fan/temp controller enabled (ideality 0x24, beta 0x00)
- `TPS546` PMBus core regulator enabled (VOUT 1.2 V core rail)
- No BAP, no display (`.bap = NULL, .i80 = NULL`)
- `asic_enable = false`, `plug_sense = false` (core power is always on via TPS546; barrel jack has no sense pin)

## ESP32 pin map

| Signal | ESP32-S3 GPIO | Notes |
|--------|---------------|-------|
| ASIC serial TX (→U7→BM1370 CI) | GPIO17 | UART1, hardcoded in `components/asic/serial.c` |
| ASIC serial RX (←U8←BM1370 RO) | GPIO18 | UART1 |
| ASIC reset (→U6→BM1370 NRSTI) | GPIO1 | `CONFIG_GPIO_ASIC_RESET`, default already 1 |
| I2C SDA (EMC2101, TPS546D24) | GPIO48 | `BITCOINMINER_I2C_PINS` |
| I2C SCL | GPIO47 | |
| WS2812B LED chain (D3–D11) | GPIO38 | Not driven by ESP-Miner (no RGB LED support); reserved |
| Boot button (SW2) | GPIO0 | default boot button |
| USB D− / D+ | GPIO19 / GPIO20 | USB-C flashing |
| UART0 console (J2 TC2030) | GPIO43 (RX) / GPIO44 (TX) | debug |
| Board LED D2 | GPIO21 | not used by firmware |
| TPS546 Power Good (PGD) | GPIO11 | not used by firmware |
| TPS546 SMB_ALERT | GPIO13 | not used by firmware |

GPIO2 is tied to the 1.2 V ASIC core rail on the PCB — do not configure it as an output.

## Build

Requires ESP-IDF v6.0.x for ESP32-S3 and Node.js ≥ 22 (the AxeOS web UI is
compiled into the binary). See upstream `AGENTS.md` / `readme.md` for the exact
SDK and the official devcontainer if you don't want to install the toolchain.

```
cd firmware
git clone ... # upstream expects the libsecp256k1 component vendored here already
. $HOME/esp/v6.0.2/esp-idf/export.sh
idf.py set-target esp32s3
idf.py build
./merge_bin.sh ./esp-miner-merged.bin
```

## Flash

Install [bitaxetool](https://pypi.org/project/bitaxetool/):

```
pip install bitaxetool
bitaxetool --config ./configs/config-bitcoinMiner.csv --firmware ./esp-miner-merged.bin
```

Or flash over USB-C (J4) / TC2030 (J2):

1. Hold **SW1** (boot) and press **SW2** (reset) to enter download mode.
2. `esptool.py --chip esp32s3 --port /dev/ttyACM0 write_flash 0x0 esp-miner-merged.bin`
3. Press **SW2** (reset) to boot, then configure WiFi/pool from the AxeOS UI
   (captive portal AP `bitcoinminer`).

## What's not wired up

- **WS2812B status LEDs (GPIO38)**: upstream ESP-Miner has no RGB/LED-strip
  support, so the LED chain stays dark. Wiring it to the firmware would need a
  new feature (e.g. led_strip + status colors) that doesn't exist upstream.
- **Board LED D2 (GPIO21)** and TPS546 PGD/SMB_ALERT (GPIO11/13) are reserved
  but unused by the firmware.