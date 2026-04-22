# Enclustra Product Summary for AI-Assisted Product Selection

This document contains summarized information from all Enclustra FPGA and SoC module user manuals. Its purpose is to enable an AI system to quickly identify candidate modules based on customer requirements, without needing to read every PDF. Once candidates are identified, the detailed PDFs should be consulted for pin-level, schematic, and known-issue information.

**Source repository:** `enc-product-docs`
**Extraction date:** 2026-04-22

---

## Module Families Overview

Enclustra modules come in three families, each with a distinct form factor and connector system. Modules within a family share base board compatibility.

| Family | Connector | Form Factor | Base Boards |
|---|---|---|---|
| Mars | 200-pin DDR2 SO-DIMM (1.8V) | 30 x 67.6 mm | EB1, PM3, ST3 |
| Mercury / Mercury+ | Hirose FX10 168-pin headers (2x or 3x) | 56x54 to 76x54 mm | PE1, PE3, ST1 |
| Andromeda | Samtec ADM6 240-pin headers (3x or 6x) | 68x52 to 80x64 mm | PE5 |

**Key constraint:** A module can only be used with base boards from its own family. Mars modules fit Mars base boards, Mercury modules fit Mercury base boards, Andromeda modules fit Andromeda base boards.

### Mercury Connector Sub-variants

Not all Mercury modules use the same number of Hirose connectors. This affects which PE1 base board variant is needed.

| Connector Count | Total Pins | Modules |
|---|---|---|
| 2x Hirose FX10 (336 pins) | Smaller modules | CA1, KX1, SA1, XU5, ZX1, ZX5 |
| 3x Hirose FX10 (504 pins) | Larger modules | AA1, KX2, MP1, SA2, XU1, XU6, XU61, XU7, XU8, XU9 |

---

## FPGA-Only Modules (No Hard Processor)

These modules have FPGA fabric only. No ARM or RISC-V cores. Use cases: pure logic, DSP, high-speed communication, protocol bridging, custom data processing.

### Mars AX3

- **FPGA:** AMD/Xilinx Artix-7 (28 nm), CSG324 package
- **Devices available:** XC7A35T, XC7A50T, XC7A100T
- **Family / Connector:** Mars / SO-DIMM 200-pin
- **Form factor:** 30 x 67.6 mm
- **User I/Os:** 108 (single-ended, differential, or analog), up to 3.3V
- **I/O banks:** 3 banks (14, 34, 35), 54 differential pairs
- **MGT transceivers:** None
- **PCIe:** None
- **DDR memory:** 256 MB DDR3 SDRAM
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** None (no eMMC, no NAND)
- **Ethernet:** 1x Gigabit Ethernet (on-module PHY)
- **USB:** None on module
- **Other interfaces:** I2C (EEPROM, RTC)
- **Clock:** 50 MHz oscillator
- **RTC:** Optional
- **Supply voltage:** Single 3.3V
- **Temperature:** Industrial (-40 to +85C) available
- **Tool support:** Vivado HL WebPACK (free)
- **Processor:** None
- **GPU / Video codec:** None
- **Base boards:** Mars EB1, Mars PM3, Mars ST3

### Mercury CA1

- **FPGA:** Intel/Altera Cyclone IV (60 nm), FBGA484 package
- **Devices available:** EP4CE30, EP4CE75, EP4CE115
- **Family / Connector:** Mercury / 2x Hirose FX10 (336 pins)
- **Form factor:** 56 x 54 mm
- **User I/Os:** Up to 168 (configurable: 25 diff pairs + 98 SE, or 146 SE, or 168 SE)
- **MGT transceivers:** None
- **PCIe:** None
- **DDR memory:** Up to 256 MB DDR2 SDRAM
- **Flash:** 16 MB SPI
- **Non-volatile storage:** None
- **Ethernet:** 1x Gigabit Ethernet
- **USB:** FTDI USB 2.0 device controller (on module)
- **Other interfaces:** I2C (RTC, power/current monitor)
- **Clock:** Not specified in features
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Temperature:** Commercial (0 to +70C) and Industrial (-40 to +85C) available
- **Tool support:** Intel Quartus
- **Processor:** None
- **GPU / Video codec:** None
- **Notable:** Power and current monitor on module. Oldest FPGA technology in portfolio (60 nm).
- **Base boards:** Mercury PE1 (PE1-200), Mercury ST1

### Mercury KX1

- **FPGA:** AMD/Xilinx Kintex-7 (28 nm), FFG676/FBG676 package
- **Devices available:** XC7K160T, XC7K325T
- **Family / Connector:** Mercury / 2x Hirose FX10 (336 pins)
- **Form factor:** 56 x 54 mm
- **User I/Os:** 178 total (158 FPGA I/Os + 20 MGT signals)
- **MGT transceivers:** 4 MGTs (FBG: 6.6 Gbit/s, FFG: 10.3125 Gbit/s) + 2 refclk pairs
- **PCIe:** Gen2 x4 (Xilinx integrated block)
- **DDR memory:** Up to 2 GB + 512 MB DDR3 SDRAM (two independent memory interfaces)
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** None
- **Ethernet:** 2x Gigabit Ethernet
- **USB:** Cypress EZ-USB FX3 USB 3.0 device controller (on module)
- **Other interfaces:** I2C (RTC)
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Temperature:** Commercial and Industrial available
- **Tool support:** Vivado (requires license for K325T)
- **Processor:** None
- **GPU / Video codec:** None
- **Notable:** High-power 16A core supply. Dual GbE. USB 3.0 on module. Two DDR3 banks.
- **Base boards:** Mercury PE1 (PE1-200), Mercury ST1

### Mercury KX2

- **FPGA:** AMD/Xilinx Kintex-7 (28 nm), FFG676/FBG676 package
- **Devices available:** XC7K160T, XC7K325T, XC7K410T
- **Family / Connector:** Mercury / 3x Hirose FX10 (504 pins)
- **Form factor:** 56 x 54 mm (assumption based on Mercury family standard)
- **User I/Os:** 256 total (216 FPGA I/Os + 40 MGT signals)
- **MGT transceivers:** 8 MGTs (FBG: 6.6 Gbit/s, FFG: 10.3125 Gbit/s) + 4 refclk pairs
- **PCIe:** Gen2 x8 (Xilinx integrated block)
- **DDR memory:** Up to 2 GB DDR3 SDRAM
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** None
- **Ethernet:** 2x Gigabit Ethernet
- **USB:** FTDI USB 2.0 device controller (on module)
- **Other interfaces:** I2C
- **RTC:** Not mentioned in features
- **Supply voltage:** 5 to 15V
- **Temperature:** Commercial and Industrial available
- **Tool support:** Vivado (requires license for K325T, K410T)
- **Processor:** None
- **GPU / Video codec:** None
- **Notable:** High-power 20A core supply. Most I/Os and MGTs of any pure FPGA module. PCIe x8.
- **Base boards:** Mercury PE1 (PE1-300 or PE1-400), Mercury PE3, Mercury ST1

---

## SoC Modules with ARM Cortex-A9 (Older Generation)

Dual-core ARM Cortex-A9, suitable for Linux, moderate processing. Older but mature and cost-effective.

### Mars ZX2

- **SoC:** AMD/Xilinx Zynq-7010/7020 (28 nm), CLG400 package
- **Processor:** Dual ARM Cortex-A9 with NEON
- **Family / Connector:** Mars / SO-DIMM 200-pin
- **Form factor:** 30 x 67.6 mm
- **FPGA fabric:** Artix-7 class
- **User I/Os:** 108 (12 ARM peripheral + 96 FPGA), up to 3.3V
- **MGT transceivers:** None
- **PCIe:** None
- **DDR memory:** 512 MB DDR3L SDRAM
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** None (no eMMC, no NAND)
- **Ethernet:** 1x Gigabit Ethernet
- **USB:** 1x USB 2.0 OTG
- **Other peripherals (active via PS):** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** Single 3.3V
- **Temperature:** Commercial and Industrial available
- **Processor:** Dual ARM Cortex-A9
- **GPU / Video codec:** None
- **Notable:** Smallest Zynq SoC module. Good entry-level SoC. No MGTs.
- **Base boards:** Mars EB1, Mars PM3, Mars ST3

### Mars ZX3

- **SoC:** AMD/Xilinx Zynq-7020 (28 nm), CLG484 package
- **Processor:** Dual ARM Cortex-A9 with NEON
- **Family / Connector:** Mars / SO-DIMM 200-pin
- **Form factor:** 30 x 67.6 mm
- **FPGA fabric:** Artix-7 class
- **User I/Os:** 108 (12 ARM peripheral + 96 FPGA), up to 3.3V
- **MGT transceivers:** None
- **PCIe:** None
- **DDR memory:** Up to 1 GB DDR3 SDRAM
- **Flash:** 64 MB quad SPI + 512 MB NAND flash
- **Non-volatile storage:** 512 MB NAND flash
- **Ethernet:** 1x Gigabit Ethernet
- **USB:** 1x USB 2.0 OTG
- **Other peripherals (active via PS):** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** Single 3.3V
- **Temperature:** Commercial and Industrial available
- **Notable:** More DDR and NAND flash than ZX2. Same Zynq-7020 but larger package.
- **Base boards:** Mars EB1, Mars PM3, Mars ST3

### Mars MA3

- **SoC:** Intel/Altera Cyclone V SoC (28 nm) -- 5CSEBA5 or 5CSXFC6
- **Processor:** Dual ARM Cortex-A9
- **Family / Connector:** Mars / SO-DIMM 200-pin
- **Form factor:** 30 x 67.6 mm
- **FPGA fabric:** Cyclone V (28 nm)
- **User I/Os:** Up to 104 (16 ARM peripheral, 76 FPGA, 12 MGT for 5CSX)
- **I/O voltage:** Up to 3.3V
- **MGT transceivers:** 2 MGTs @ 3.125 Gbit/s (5CSX variants only) + 2 refclk pairs
- **PCIe:** Gen1 x2 (5CSX variants only, Altera hardened IP)
- **DDR memory:** 1 GB DDR3L SDRAM
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 1x Gigabit Ethernet + 1x Fast Ethernet
- **USB:** 1x USB 2.0 OTG
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** Single 3.3V
- **Temperature:** Commercial (0 to +70C) and Industrial (-40 to +85C)
- **Notable:** Only Intel/Altera SoC in the Mars family. Has eMMC. Dual Ethernet (1x GbE + 1x FE).
- **Base boards:** Mars EB1, Mars PM3, Mars ST3

### Mercury SA1

- **SoC:** Intel/Altera Cyclone V SoC (28 nm) -- 5CSXFC6
- **Processor:** Dual ARM Cortex-A9
- **Family / Connector:** Mercury / 2x Hirose FX10 (336 pins)
- **Form factor:** 56 x 54 mm
- **FPGA fabric:** Cyclone V (28 nm)
- **User I/Os:** 178 total (16 ARM peripheral + 134 FPGA + 28 MGT signals)
- **MGT transceivers:** 6 MGTs @ 3.125 Gbit/s + 2 refclk pairs
- **PCIe:** Gen1 x4 (Altera hardened IP)
- **DDR memory:** 1 GB DDR3L SDRAM
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** None
- **Ethernet:** 1x Gigabit Ethernet
- **USB:** 1x USB 2.0 OTG
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Temperature:** Commercial and Industrial available
- **Notable:** Mercury form factor Cyclone V SoC. More MGTs and I/Os than Mars MA3.
- **Base boards:** Mercury PE1 (PE1-200), Mercury ST1

### Mercury SA2

- **SoC:** Intel/Altera Cyclone V SoC (28 nm) -- 5CSTFD6D5
- **Processor:** Dual ARM Cortex-A9
- **Family / Connector:** Mercury / 3x Hirose FX10 (504 pins)
- **Form factor:** 56 x 54 mm (approx)
- **FPGA fabric:** Cyclone V (28 nm)
- **User I/Os:** 294 total (18 ARM peripheral + 202 FPGA + 32 FPGA shared with USB 3.0 + 42 MGT signals)
- **MGT transceivers:** 9 MGTs @ 6.144 Gbit/s + 3 refclk pairs
- **PCIe:** Gen2 x4 (Altera hardened IP)
- **DDR memory:** 2 GB DDR3L SDRAM
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** None
- **Ethernet:** 1x Gigabit Ethernet + 2x Fast Ethernet
- **USB:** Cypress EZ-USB FX3 USB 3.0 device controller + USB 2.0 host/device
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Temperature:** Industrial available
- **Notable:** Highest I/O count Cyclone V module. USB 3.0 on module. 3x Ethernet.
- **Base boards:** Mercury PE1 (PE1-300/PE1-400), Mercury PE3, Mercury ST1

### Mercury ZX1

- **SoC:** AMD/Xilinx Zynq-7030/7035/7045 (28 nm), FBG676/FFG676 package
- **Processor:** Dual ARM Cortex-A9 with NEON
- **Family / Connector:** Mercury / 2x Hirose FX10 (336 pins)
- **Form factor:** 56 x 54 mm (approx)
- **FPGA fabric:** Kintex-7 class
- **User I/Os:** 170-178 (varies by device: 12 ARM peripheral + 126-138 FPGA + 20-40 MGT signals)
- **MGT transceivers:**
  - Zynq-7030: 4 MGTs @ 6.6 Gbit/s + 2 refclk pairs
  - Zynq-7035: 8 MGTs @ 6.6 Gbit/s + 4 refclk pairs
  - Zynq-7045: 8 MGTs @ 10.3125 Gbit/s + 4 refclk pairs
- **PCIe:** Gen2 x4/x8 (AMD integrated block)
- **DDR memory:** 1 GB DDR3 (PS) + 256 MB DDR3 (PL) -- two independent interfaces
- **Flash:** 64 MB quad SPI + 512 MB NAND flash
- **Non-volatile storage:** 512 MB NAND
- **Ethernet:** 1x Gigabit Ethernet + 2x Fast Ethernet
- **USB:** 1x USB 2.0 OTG
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Temperature:** Commercial and Industrial available
- **Notable:** Zynq-7000 with Kintex-class fabric (higher performance than Artix-class in ZX2/ZX3). Dual DDR banks. NAND flash.
- **Base boards:** Mercury PE1 (PE1-200), Mercury ST1

### Mercury ZX5

- **SoC:** AMD/Xilinx Zynq-7015/7030 (28 nm), CLG485/SBG485 package
- **Processor:** Dual ARM Cortex-A9 with NEON
- **Family / Connector:** Mercury / 2x Hirose FX10 (336 pins)
- **Form factor:** 56 x 54 mm
- **FPGA fabric:** Artix-7 (7015) or Kintex-7 (7030) class
- **User I/Os:** 178 (12 ARM peripheral + 146 or 54+92 FPGA + 20 MGT signals)
- **MGT transceivers:**
  - Zynq-7015: 4 MGTs @ 6.25 Gbit/s
  - Zynq-7030: 4 MGTs @ 6.6 Gbit/s
  - 2 refclk pairs
- **PCIe:** Gen2 x4 (AMD integrated block)
- **DDR memory:** 1 GB DDR3L SDRAM
- **Flash:** 64 MB quad SPI + 512 MB NAND flash
- **Non-volatile storage:** 512 MB NAND
- **Ethernet:** 1x Gigabit Ethernet
- **USB:** 1x USB 2.0 OTG
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Temperature:** Commercial and Industrial available
- **Notable:** Compact Mercury Zynq-7000. NAND flash.
- **Base boards:** Mercury PE1 (PE1-200), Mercury ST1

### Mercury AA1

- **SoC:** Intel Arria 10 SoC (20 nm) -- 10AS027/10AS048
- **Processor:** Dual ARM Cortex-A9
- **Family / Connector:** Mercury / 3x Hirose FX10 (504 pins)
- **Form factor:** 56 x 54 mm (approx)
- **FPGA fabric:** Arria 10 (20 nm)
- **User I/Os:** 286 total (18 ARM peripheral + 168 FPGA + 44 FPGA shared with USB 3.0 + 56 MGT signals)
- **I/O voltage:** Up to 1.8V
- **MGT transceivers:** 12 MGTs (speedgrade 4: 10.3125 Gbit/s, others: 12.5 Gbit/s) + 4 refclk pairs
- **PCIe:** Gen3 x8 (Intel hardened IP)
- **DDR memory:** Up to 4 GB DDR4 SDRAM with ECC
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 1x Gigabit Ethernet
- **USB:** USB 2.0 host/device
- **Other peripherals:** UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Notable:** Highest-performance Intel SoC module. DDR4 with ECC. PCIe Gen3 x8. No CAN. I/Os limited to 1.8V max.
- **Base boards:** Mercury PE1 (PE1-300/PE1-400), Mercury PE3, Mercury ST1

---

## SoC Modules with ARM Cortex-A53 (AMD Zynq UltraScale+)

Quad-core or dual-core ARM Cortex-A53 (64-bit) + Cortex-R5 real-time cores. 16nm FinFET+ FPGA fabric. Supports Linux, RTOS, bare-metal. Current-generation AMD SoC platform.

**Device variant naming:**
- **CG** = No GPU, no video codec, dual-core A53
- **EG** = GPU (Mali-400 MP2), quad-core A53
- **EV** = GPU + H.264/H.265 video codec, quad-core A53

### Mars XU3

- **SoC:** AMD Zynq UltraScale+ (16 nm), SBVA484 package
- **Devices available:** XCZU2CG, XCZU2EG, XCZU3EG
- **Processor:** Dual/Quad-core ARM Cortex-A53 (up to 1.33 GHz) + Dual Cortex-R5 (533 MHz)
- **Family / Connector:** Mars / SO-DIMM 200-pin
- **Form factor:** 30 x 67.6 mm
- **User I/Os:** 108 (12 ARM peripheral + 76 FPGA: 52 HP up to 1.8V, 24 HD up to 3.3V)
- **MGT transceivers:** 4 GTR @ 5 Gbit/s + 2 refclk pairs
- **PCIe:** Gen2 x4 (AMD hard block via GTR)
- **DDR memory:** Up to 2 GB DDR4 SDRAM
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 1x Gigabit Ethernet
- **USB:** USB 2.0 OTG + USB 3.0 (via GTR)
- **RTC:** Yes
- **Supply voltage:** Not explicitly stated (Mars family, likely 3.3V or similar)
- **Temperature:** Available in industrial grades
- **Notable:** Smallest UltraScale+ module. Mars form factor. Good entry-level ZU+ with eMMC.
- **Base boards:** Mars EB1, Mars PM3, Mars ST3

### Mercury XU5

- **SoC:** AMD Zynq UltraScale+ (16 nm), SFVC784 package
- **Devices available:** XCZU2CG, XCZU2EG, XCZU3EG, XCZU4CG, XCZU4EV, XCZU5EV
- **Processor:** Dual/Quad-core ARM Cortex-A53 (up to 1.5 GHz) + Dual Cortex-R5 (600 MHz)
- **Family / Connector:** Mercury / 2x Hirose FX10 (336 pins)
- **Form factor:** 56 x 54 mm
- **User I/Os (ZU2/ZU3):** 146 FPGA (92 HP up to 1.8V, 54 HD up to 3.3V) + 12 ARM peripheral
- **User I/Os (ZU4/ZU5 standard):** 124 FPGA (72 HP, 52 HD) + 14 ARM peripheral
- **User I/Os (ZU4/ZU5 G1 alt routing):** 146 FPGA (92 HP, 54 HD) + 12 ARM peripheral
- **MGT transceivers:**
  - ZU2/ZU3: 4 GTR @ 6 Gbit/s + 2 refclk
  - ZU4/ZU5 standard: 4 GTH @ 12.5 Gbit/s + 4 GTR @ 6 Gbit/s + 4 refclk
  - ZU4/ZU5 G1: 4 GTH @ 12.5 Gbit/s + 2 refclk (no GTR on connector)
- **PCIe:**
  - ZU2/ZU3: Gen2 x4 (via GTR)
  - ZU4/ZU5: Gen3 x4 (via GTH) and/or Gen2 x4 (via GTR, standard routing only)
- **DDR memory:** Up to 8 GB DDR4 with ECC (PS) + up to 2 GB DDR4 (PL)
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 2x Gigabit Ethernet PHYs
- **USB:** 2x USB 2.0 PHYs + USB 3.0 (via GTR)
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Temperature:** Commercial and Industrial available
- **Notable:** Wide device range (ZU2 to ZU5). EV variants support video codec. Two DDR4 interfaces (PS+PL). Compact form factor. Assembly variant "G1" trades GTR lanes for more FPGA I/Os.
- **Base boards:** Mercury PE1 (PE1-200), Mercury ST1

### Mercury XU6

- **SoC:** AMD Zynq UltraScale+ (16 nm), SFVC784 package
- **Devices available:** XCZU2CG, XCZU2EG, XCZU3EG, XCZU4CG, XCZU4EV, XCZU5EV
- **Processor:** Dual/Quad-core ARM Cortex-A53 (up to 1.333 GHz) + Dual Cortex-R5 (533 MHz)
- **Family / Connector:** Mercury / 3x Hirose FX10 (504 pins)
- **Form factor:** 65 x 54 mm
- **User I/Os:** 240 FPGA (148 HP: 144 up to 1.8V + 4 up to 3.3V via level shifters; 92 HD up to 3.3V) + 14 ARM peripheral
- **MGT transceivers:**
  - ZU2/ZU3: 4 GTR @ 6 Gbit/s + 4 refclk
  - ZU4/ZU5: 4 GTH @ 12.5 Gbit/s + 4 GTR @ 6 Gbit/s + 6 refclk
- **PCIe:**
  - ZU4/ZU5: Gen3 x4 (GTH) + Gen2 x4 (GTR)
- **DDR memory:** Up to 8 GB DDR4 with ECC (PS)
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 1x Gigabit Ethernet PHY
- **USB:** 2x USB 2.0 PHYs (or 1x OTG) + USB 3.0 (via GTR)
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Notable:** Same devices as XU5 but with 3x connector and significantly more I/Os (240 vs 124-146). Only 1x GbE (vs 2x on XU5). Single DDR4 bank (PS only).
- **Base boards:** Mercury PE1 (PE1-300/PE1-400), Mercury PE3, Mercury ST1

### Mercury XU61

- **SoC:** AMD Zynq UltraScale+ **Low-Power Grade** (16 nm), SFVC784 package
- **Devices available:** XCZU2CG, XCZU2EG, XCZU4CG, XCZU5CG
- **Processor:** Dual/Quad-core ARM Cortex-A53 (up to 1.333 GHz) + Dual Cortex-R5 (533 MHz)
- **Family / Connector:** Mercury / 3x Hirose FX10 (504 pins)
- **Form factor:** 65 x 54 mm
- **User I/Os:** 240 FPGA (148 HP: 144 up to 1.8V + 4 up to 3.3V via level shifters; 92 HD up to 3.3V) + 14 ARM peripheral
- **MGT transceivers:**
  - ZU2: 4 GTR @ 6 Gbit/s + 4 refclk
  - ZU4/ZU5: 4 GTH @ 12.5 Gbit/s + 4 GTR @ 6 Gbit/s + 6 refclk
- **PCIe:**
  - ZU4/ZU5: Gen3 x4 (GTH) + Gen2 x4 (GTR)
- **DDR memory:** Up to 2 GB LPDDR4 SDRAM
- **Flash:** 64 MB QSPI
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 1x Gigabit Ethernet PHY
- **USB:** Up to 2x USB 2.0 PHYs (or 1x OTG) + USB 3.0 (via GTR)
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **TPM:** Yes
- **User EEPROM:** Yes
- **Supply voltage:** 5 to 13.2V
- **Notable:** **Low-power variant** of XU6. Uses LPDDR4 (max 2 GB vs 8 GB). Has TPM and user EEPROM. Only CG devices (no EV/EG with video codec or GPU). Designed for power-constrained applications.
- **Base boards:** Mercury PE1 (PE1-300/PE1-400), Mercury PE3, Mercury ST1

### Mercury XU1

- **SoC:** AMD Zynq UltraScale+ (16 nm), FFVC900 package
- **Devices available:** XCZU6CG, XCZU6EG, XCZU9EG, XCZU15EG
- **Processor:** Dual/Quad-core ARM Cortex-A53 (up to 1.5 GHz) + Dual Cortex-R5 (600 MHz)
- **Family / Connector:** Mercury / 3x Hirose FX10 (504 pins)
- **Form factor:** 76 x 54 mm
- **User I/Os:** 200 FPGA (152 HP: 148 up to 1.8V + 4 up to 3.3V via level shifters; 48 HD up to 3.3V) + 14 ARM peripheral
- **MGT transceivers:** Up to 20 total
  - 12 GTH (speed grade 1: 12.5 Gbit/s, others: 16.375 Gbit/s)
  - 4 GTR @ 6 Gbit/s
  - Up to 12 refclk inputs (6 GTH + 4 GTR)
- **PCIe:** Gen2 x4 (via GTR)
- **DDR memory:** Up to 4 GB DDR4 with ECC
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 2x Gigabit Ethernet PHYs (one shared with USB)
- **USB:** 2x USB 2.0 PHYs + USB 3.0 (via GTR)
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Notable:** Mid-to-high-end ZU+ module. Larger FPGA devices (ZU6 to ZU15). 12 GTH transceivers for high-speed links. One GbE PHY shared with USB PHY.
- **Base boards:** Mercury PE1 (PE1-300/PE1-400), Mercury PE3, Mercury ST1

### Mercury XU7

- **SoC:** AMD Zynq UltraScale+ (16 nm), FFVC900 package
- **Devices available:** XCZU6EG, XCZU9EG, XCZU15EG
- **Processor:** Quad-core ARM Cortex-A53 (up to 1.333 GHz) + Dual Cortex-R5 (533 MHz)
- **Family / Connector:** Mercury / 3x Hirose FX10 (504 pins)
- **Form factor:** 74 x 54 mm
- **User I/Os:** 122 FPGA (74 HP: 50 up to 1.8V + 20 at 1.2V fixed + 4 up to 3.3V via level shifters; 48 HD up to 3.3V) + 14 ARM peripheral
- **MGT transceivers:** 20 total
  - 16 GTH (speed grade 1: 12.5 Gbit/s, others: 16.375 Gbit/s)
  - 4 GTR @ 6 Gbit/s
  - 10 refclk inputs (8 GTH + 2 GTR)
- **PCIe:** Gen2 x4 (via GTR)
- **DDR memory:** Up to 4 GB DDR4 with ECC (PS) + up to 2 GB DDR4 (PL)
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 2x Gigabit Ethernet PHYs (one shared with USB)
- **USB:** 2x USB 2.0 PHYs (or 1x OTG) + USB 3.0 (via GTR)
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Notable:** Optimized for MGT-heavy applications (16 GTH). Fewer FPGA I/Os than XU1 (122 vs 200) but 4 more GTH (16 vs 12). Dual DDR4 (PS+PL). Only EG devices (all have GPU). 20 I/Os at fixed 1.2V.
- **Base boards:** Mercury PE1 (PE1-300/PE1-400), Mercury PE3, Mercury ST1

### Mercury XU8

- **SoC:** AMD Zynq UltraScale+ (16 nm), FBVB900 package
- **Devices available:** XCZU4CG, XCZU5EV, XCZU7EV, XCZU7EG
- **Processor:** Dual/Quad-core ARM Cortex-A53 (up to 1.5 GHz) + Dual Cortex-R5 (533 MHz)
- **Family / Connector:** Mercury / 3x Hirose FX10 (504 pins)
- **Form factor:** 74 x 54 mm
- **User I/Os:** 122 FPGA (74 HP: 50 up to 1.8V + 20 at 1.2V fixed + 4 up to 3.3V via level shifters; 48 HD up to 3.3V) + 14 ARM peripheral
- **MGT transceivers:** 20 total
  - 16 GTH (speed grade 1: 12.5 Gbit/s, others: 15 Gbit/s)
  - 4 GTR @ 6 Gbit/s
  - 12 refclk inputs (8 GTH + 4 GTR)
- **PCIe:** Gen3 x16 (via GTH) + Gen2 x4 (via GTR)
- **DDR memory:** Up to 4 GB DDR4 with ECC (PS) + up to 2 GB DDR4 (PL)
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 2x Gigabit Ethernet PHYs (one shared with USB)
- **USB:** 2x USB 2.0 PHYs + USB 3.0 (via GTR)
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Notable:** Has **PCIe Gen3 x16** capability (unique among Mercury ZU+ modules). EV variants have H.264/H.265 video codec. Similar I/O layout to XU7 but different FPGA package (FBVB900 vs FFVC900) and PCIe Gen3 x16 vs Gen2 x4. ZU7EV is the highest-performance EV device in Mercury.
- **Base boards:** Mercury PE1 (PE1-300/PE1-400), Mercury PE3, Mercury ST1

### Mercury XU9

- **SoC:** AMD Zynq UltraScale+ (16 nm), FBVB900 package
- **Devices available:** XCZU4CG, XCZU4EV, XCZU5EV, XCZU7EV
- **Processor:** Dual/Quad-core ARM Cortex-A53 (up to 1.333 GHz) + Dual Cortex-R5 (533 MHz)
- **Family / Connector:** Mercury / 3x Hirose FX10 (504 pins)
- **Form factor:** 74 x 54 mm
- **User I/Os:** 78 FPGA (30 HP: 26 at 1.2V fixed + 4 up to 3.3V via level shifters; 48 HD up to 3.3V) + 14 ARM peripheral
- **MGT transceivers:** 20 total
  - 16 GTH (speed grade 1: 12.5 Gbit/s, others: 16.375 Gbit/s)
  - 4 GTR @ 6 Gbit/s
  - 10 refclk inputs (8 GTH + 2 GTR)
- **PCIe:** Gen3 x16 (via GTH) + Gen2 x4 (via GTR)
- **DDR memory:** Up to 4 GB DDR4 with ECC (PS) + up to 2 GB DDR4 (PL)
- **Flash:** 64 MB quad SPI
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 2x Gigabit Ethernet PHYs (one shared with USB)
- **USB:** 2x USB 2.0 PHYs + USB 3.0 (via GTR)
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** 5 to 15V
- **Notable:** **Fewest FPGA I/Os** of any Mercury ZU+ module (78 total, 26 at fixed 1.2V). Optimized for maximum MGT throughput, not general-purpose I/O. PCIe Gen3 x16. EV variants available. Same physical layout as XU8.
- **Base boards:** Mercury PE1 (PE1-300/PE1-400), Mercury PE3, Mercury ST1

---

## SoC Modules with RISC-V (Microchip PolarFire SoC)

### Mercury MP1

- **SoC:** Microchip PolarFire SoC (28 nm, non-volatile FPGA fabric)
- **Devices available:** MPFS250T, MPFS460T
- **Processor:** 4x RV64GC application cores (up to 625 MHz) + 1x RV64IMAC monitor core (625 MHz)
- **Family / Connector:** Mercury / 3x Hirose FX10 (504 pins)
- **Form factor:** Not explicitly stated (Mercury family)
- **User I/Os (MPFS250T):** 215 total (208 I/Os up to 3.3V + 9 MSS I/Os up to 3.3V)
- **User I/Os (MPFS460T):** 195 total (188 I/Os up to 3.3V + 9 MSS I/Os)
- **MGT transceivers:**
  - MPFS250T: 20 XCVRs @ 12.7 Gbit/s + 10 refclk
  - MPFS460T: 16 XCVRs @ 10.3125 Gbit/s + 8 refclk
- **PCIe:** Gen2 x4
- **DDR memory:** Up to 4 GB DDR4 with ECC (MSS) + up to 8 GB DDR4 (FPGA side)
- **Flash:** 64 MB quad SPI + 64 MB SPI
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** Up to 2x Gigabit Ethernet PHYs (SGMII on MSS)
- **USB:** OTG USB 2.0
- **Other peripherals:** UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **TPM:** Yes
- **Supply voltage:** 5 to 13.2V
- **Notable:** **Only RISC-V module** in the portfolio. **Non-volatile FPGA** (no bitstream loading needed, instant-on). TPM for security. Dual DDR4 interfaces. Non-AMD/non-Intel vendor.
- **Base boards:** Mercury PE1 (PE1-300/PE1-400), Mercury PE3, Mercury ST1

---

## High-End SoC Modules (Andromeda Family)

Largest FPGA resources, most MGTs, highest bandwidth. For demanding applications like radar, 5G, high-performance computing, video processing at scale.

### Andromeda XZU65

- **SoC:** AMD Zynq UltraScale+ (16 nm), FFVC1156 package
- **Devices available:** XCZU7EG, XCZU7EV, XCZU11EG
- **Processor:** Quad-core ARM Cortex-A53 (up to 1.333 GHz) + Dual Cortex-R5 (533 MHz)
- **GPU:** Mali-400 MP2 (up to 667 MHz)
- **Video codec:** H.264/H.265 (EV models only)
- **Family / Connector:** Andromeda / 3x Samtec ADM6 240-pin (720 pins total)
- **Form factor:** 68 x 52 mm
- **User I/Os:** 180 FPGA (156 HP 1.0-1.8V + 24 HD 1.8-3.3V) + 22 ARM peripheral
- **MGT transceivers:** 24 total
  - 20 GTH @ 16.375 Gbit/s
  - 4 GTR @ 6 Gbit/s
  - 12 refclk inputs (10 GTH + 2 GTR)
- **PCIe:** Gen3 x16 (GTH) + Gen2 x4 (GTR)
- **DDR memory:** Up to 8 GB DDR4 ECC (PS) + up to 8 GB DDR4 (PL)
- **Flash:** 128 MB QSPI (dual parallel)
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 2x Gigabit Ethernet (PS and PL)
- **USB:** USB 2.0 host/device + USB 3.0 (via GTR)
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** 12V single supply
- **Notable:** High-end module with 24 MGTs. Up to 16 GB DDR4 total (PS+PL). 128 MB dual QSPI. ZU11EG has largest FPGA fabric in this module.
- **Base boards:** Andromeda PE5

### Andromeda XZU90

- **SoC:** AMD Zynq UltraScale+ (16 nm), FFVD1760 package
- **Devices available:** XCZU17EG, XCZU19EG
- **Processor:** Quad-core ARM Cortex-A53 (up to 1.333 GHz) + Dual Cortex-R5 (533 MHz)
- **GPU:** Mali-400 MP2
- **Video codec:** None (EG devices only, no EV)
- **Family / Connector:** Andromeda / 6x Samtec ADM6 240-pin (1440 pins total)
- **Form factor:** 80 x 64 mm
- **User I/Os:** 284 FPGA (260 HP 1.0-1.8V + 24 HD 1.8-3.3V) + 22 ARM peripheral
- **MGT transceivers:** 76 total
  - 28 GTY (speed grade 1: 25.785 Gbit/s, speed grade 2: 28.21 Gbit/s)
  - 44 GTH (speed grade 1: 12.5 Gbit/s, speed grade 2: 16.375 Gbit/s)
  - 4 GTR @ 6 Gbit/s
  - 38 refclk inputs (14 GTY + 22 GTH + 2 GTR)
- **PCIe:** Up to 3x Gen3 x16 (via GTH/GTY) + Gen2 x4 (via GTR)
- **DDR memory:** 4 GB DDR4 ECC (PS)
- **Flash:** 128 MB QSPI (dual parallel)
- **Non-volatile storage:** 16 GB eMMC
- **Ethernet:** 2x Gigabit Ethernet (PS and PL)
- **USB:** USB 2.0 host/device + USB 3.0 (via GTR)
- **Other peripherals:** CAN, UART, SPI, I2C, SDIO/MMC
- **RTC:** Yes
- **Supply voltage:** 12V single supply
- **Notable:** **Largest module in the entire portfolio.** 76 MGT transceivers including 28 GTY (up to 28.21 Gbit/s). Up to 3x PCIe Gen3 x16. ZU19EG has the largest FPGA fabric available. 284 FPGA I/Os. For extreme bandwidth applications.
- **Base boards:** Andromeda PE5

---

## Base Boards Summary

### Mars Base Boards (SO-DIMM)

| Board | Form Factor | Key Features |
|---|---|---|
| Mars EB1 | 120 x 80 mm | System controller, USB 2.0 host/device, GbE, HDMI 1.3, 2x Camera Link, 40-pin Anios, 3x 12-pin (2x Pmod), microSD, 12V or USB-powered |
| Mars PM3 | 100 x 72 mm (pico-ITX) | FMC LPC (72 I/Os), Cypress FX3 USB 3.0, USB 2.0 host, GbE, mini HDMI, microSD, battery holder for RTC, 12V or USB-powered |
| Mars ST3 | 100 x 80 mm | USB 3.0 host, GbE, MIPI D-PHY (CSI), Mini DisplayPort, HDMI 1.4b, 2x 40-pin Anios, 2x 12-pin IO, microSD, 12V |

### Mercury Base Boards (Hirose FX10)

| Board | Form Factor | Key Features |
|---|---|---|
| Mercury PE1 | 160 x 111.15 mm | Available in PE1-200 (2-conn), PE1-300 (3-conn), PE1-400 (3-conn) variants. System controller, JTAG, system monitor |
| Mercury PE3 | 171 x 112.4 mm | 3x connector, PCIe x8 edge, QSFP+, 4x SFP+ (model dependent), HDMI 2.0a, USB Type-C, USB 3.0, flexible MGT routing, low-jitter clock generator, microSD |
| Mercury ST1 | 120 x 100 mm | 2x USB 3.0 (host+device), 2x GbE, Mini DisplayPort, SFP+, FMC HPC, 2x MIPI D-PHY, HDMI 2.0, 2x 40-pin Anios, 3x 12-pin IO, microSD, 12V |

### Andromeda Base Boards (Samtec ADM6)

| Board | Form Factor | Key Features |
|---|---|---|
| Andromeda PE5 | 170 x 111.15 mm | 6x Samtec connectors, PCIe edge card, 3x low-jitter clock generators, fan controller, microSD, system monitor, JTAG/UART/I2C via FTDI |

---

## Quick Selection Guide

### By Processor Architecture

| Need | Options |
|---|---|
| No processor (pure FPGA) | AX3, CA1, KX1, KX2 |
| ARM Cortex-A9 (32-bit, Linux) | ZX2, ZX3, MA3, SA1, SA2, ZX1, ZX5, AA1 |
| ARM Cortex-A53 (64-bit, Linux) | XU3, XU5, XU6, XU61, XU1, XU7, XU8, XU9, XZU65, XZU90 |
| RISC-V | MP1 |

### By FPGA Vendor

| Vendor | Modules |
|---|---|
| AMD/Xilinx | AX3, KX1, KX2, ZX2, ZX3, ZX1, ZX5, XU3, XU5, XU6, XU61, XU1, XU7, XU8, XU9, XZU65, XZU90 |
| Intel/Altera | CA1, MA3, SA1, SA2, AA1 |
| Microchip | MP1 |

### By PCIe Generation

| PCIe | Modules |
|---|---|
| None | AX3, CA1, ZX2, ZX3 |
| Gen1 | MA3 (x2), SA1 (x4) |
| Gen2 | KX1 (x4), KX2 (x8), SA2 (x4), ZX1 (x4/x8), ZX5 (x4), XU3 (x4), XU5 (x4 via GTR), XU1 (x4), XU7 (x4), MP1 (x4) |
| Gen3 | AA1 (x8), XU5 (x4 via GTH, ZU4/5 only), XU6 (x4), XU61 (x4), XU8 (x16), XU9 (x16), XZU65 (x16), XZU90 (up to 3x x16) |

### By MGT Count

| MGTs | Modules |
|---|---|
| 0 | AX3, CA1, ZX2, ZX3 |
| 2-4 | MA3, XU3, XU5 (ZU2/3) |
| 4-6 | KX1, SA1, ZX5 |
| 8-9 | KX2 (FBG), SA2, ZX1 (7035/7045), XU5 (ZU4/5) |
| 12 | AA1, KX2 (FFG) |
| 16-20 | XU1, XU6 (ZU4/5), XU7, XU8, XU9, MP1 |
| 24 | XZU65 |
| 76 | XZU90 |

### By DDR Memory Capacity

| Max DDR | Modules |
|---|---|
| 256 MB | AX3, CA1 |
| 512 MB | ZX2 |
| 1 GB | ZX3, MA3, SA1, ZX5 |
| 1.25 GB (dual bank) | ZX1 (1 GB PS + 256 MB PL) |
| 2 GB | XU3, SA2, XU61 (LPDDR4) |
| 2.5 GB (dual bank) | KX1 (2 GB + 512 MB) |
| 2 GB + 2 GB (dual bank) | KX2 |
| 4 GB | AA1, XU1 |
| 4+2 GB (PS+PL) | XU7, XU8, XU9 |
| 8 GB (PS) | XU6 |
| 8+2 GB (PS+PL) | XU5 |
| 4+8 GB (MSS+FPGA) | MP1 |
| 8+8 GB (PS+PL) | XZU65 |
| 4 GB (PS only) | XZU90 |

### By Video Codec (H.264/H.265)

Only EV device variants support the video codec:
- Mercury XU5 (ZU4EV, ZU5EV)
- Mercury XU6 (ZU4EV, ZU5EV)
- Mercury XU8 (ZU5EV, ZU7EV)
- Mercury XU9 (ZU4EV, ZU5EV, ZU7EV)
- Andromeda XZU65 (ZU7EV)

### By Non-Volatile Storage (eMMC / NAND)

| Storage | Modules |
|---|---|
| None | AX3, CA1, KX1, KX2, ZX2, SA1, SA2, ZX5 |
| 512 MB NAND | ZX3, ZX1 |
| 16 GB eMMC | MA3, XU3, XU5, XU6, XU61, XU1, XU7, XU8, XU9, AA1, MP1, XZU65, XZU90 |

### By Temperature Range

| Range | Availability |
|---|---|
| Industrial (-40 to +85C) | Available for most modules. Check specific device variants. |
| Commercial (0 to +70C) | Default for many configurations. |

### By Special Features

| Feature | Modules |
|---|---|
| TPM (security) | XU61, MP1 |
| Non-volatile FPGA (instant-on) | MP1 |
| Low-power grade devices | XU61 |
| USB 3.0 on module | KX1, SA2, and all ZU+ modules (via GTR) |
| Dual Gigabit Ethernet on module | KX1, KX2, XU5, XU1, XU7, XU8, XU9, XZU65, XZU90 |
| FMC connector on base board | Mars PM3 (LPC), Mercury ST1 (HPC) |
| SFP+ on base board | Mercury PE3, Mercury ST1 |
| QSFP+ on base board | Mercury PE3 |
| MIPI CSI on base board | Mars ST3, Mercury ST1 |

---

## Decision Tree for AI Product Selection

When a customer describes their application, evaluate in this order:

1. **Processor requirement?** Pure FPGA vs SoC. If SoC: ARM A9 (older/cheaper), ARM A53 (current gen), or RISC-V?
2. **FPGA vendor preference?** AMD/Xilinx, Intel/Altera, or Microchip?
3. **High-speed serial links (MGTs)?** How many? What speed? PCIe generation?
4. **FPGA I/O count and voltage?** How many general-purpose I/Os? Need 3.3V or 1.8V only?
5. **Memory requirements?** DDR size, ECC needed, dual-bank (PS+PL)?
6. **Non-volatile storage?** eMMC, NAND, or QSPI-only sufficient?
7. **Connectivity?** Ethernet count, USB version, CAN, specific interfaces?
8. **Video processing?** Need H.264/H.265 codec? GPU?
9. **Form factor / family?** Size constraints? Existing base board?
10. **Special requirements?** Industrial temp, TPM, low power, instant-on, specific base board features (FMC, SFP+, MIPI)?

After narrowing to 1-3 candidates, consult the full PDF user manuals for detailed pinout, schematics, known issues, and power consumption data.
