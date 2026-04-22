# FPGA/SoC Device Family Comparison for Enclustra Product Selection

This document summarizes the key device family characteristics relevant to product selection. It is derived from the vendor datasheets in the `vendor/` folder and should be read before any product selection task. For device-specific pin counts, package options, or errata, consult the original datasheets.

**Source datasheets:**
- `vendor/amd/ds891-zynq-ultrascale-plus-overview.pdf` -- Zynq UltraScale+ MPSoC
- `vendor/amd/ds190-Zynq-7000-Overview.pdf` -- Zynq-7000 SoC
- `vendor/altera/a10_overview-683332-670810.pdf` -- Arria 10 SoC (SX variant)
- `vendor/altera/cv_5v2-683375-666995.pdf` -- Cyclone V SoC (SE/SX/ST variants)
- `vendor/microchip/Polarfire_SOC_Product_Overview.pdf` -- PolarFire SoC

**Extraction date:** 2026-04-22

---

## 1. Processor Subsystem Comparison

| Feature | Zynq UltraScale+ | Zynq-7000 | Cyclone V SoC | Arria 10 SoC | PolarFire SoC |
|---|---|---|---|---|---|
| Architecture | ARMv8-A (64-bit) | ARMv7-A (32-bit) | ARMv7-A (32-bit) | ARMv7-A (32-bit) | RISC-V RV64GC (64-bit) |
| Application cores | 2 or 4x Cortex-A53 | 2x Cortex-A9 (or 1x on 7000S) | 2x Cortex-A9 | 2x Cortex-A9 | 4x RV64GC (U54) |
| Max frequency | Up to 1.5 GHz | Up to 1.0 GHz (-3 speed) | Up to 925 MHz | Up to 1.5 GHz (1.2 GHz nominal) | Up to 667 MHz |
| Real-time cores | 2x Cortex-R5F (up to 600 MHz) | None | None | None | 1x RV64IMAC monitor (E51, 667 MHz) |
| FPU | Yes (per core) | Yes (NEON + VFP per core) | Yes (NEON + VFP per core) | Yes (NEON + VFP per core) | Yes (per U54 core) |
| L1 cache | 32K I + 32K D per core | 32K I + 32K D per core | 32K I + 32K D per core | 32K I + 32K D per core | 32K I + 32K D per U54 core |
| L2 cache | 1 MB shared (A53) | 512 KB shared | 512 KB shared | 512 KB shared | 2 MB flexible (cache/LIM/scratchpad) |
| On-chip RAM | 256 KB OCM (PS) | 256 KB OCM | 64 KB | 256 KB + 64 KB ROM | 128 KB eNVM boot + 2 MB L2 |
| GPU | Mali-400 MP2 (EG/EV only) | None | None | None | None |
| Video codec | H.264/H.265 (EV only) | None | None | None | None |
| TrustZone | Yes | Yes | Not mentioned | Yes | N/A (PMP/PUF-based security) |

### Processor I/O Peripherals

| Peripheral | Zynq UltraScale+ | Zynq-7000 | Cyclone V SoC | Arria 10 SoC | PolarFire SoC |
|---|---|---|---|---|---|
| GbE MAC | 4x (RGMII/SGMII) | 2x (RGMII/SGMII) | 2x (RGMII/SGMII) | 2x (RGMII) | 2x (SGMII) |
| USB | 2x USB 2.0/3.0 | 2x USB 2.0 OTG | 2x USB 2.0 OTG | 2x USB 2.0 OTG | 1x USB 2.0 OTG |
| CAN | 2x CAN 2.0B | 2x CAN 2.0B | 2x CAN 2.0B | 2x CAN 2.0B | 2x CAN 2.0 A/B |
| UART | 2x | 2x | 2x | 2x | 5x |
| SPI | 2x | 2x | 2x | 2x | 2x |
| I2C | 2x | 2x | 5x (I2C/SPI combined) | 5x (I2C/SPI combined) | 2x |
| SD/SDIO | 2x SD/eMMC4.51 | 2x SD/SDIO 2.0 | 1x SD/MMC | 1x SD/MMC | 1x MMC 5.1/SD/SDIO |
| GPIO (MIO) | Up to 78 MIO | Up to 54 MIO | Up to 62 HPS GPIO | Up to 62 HPS GPIO | GPIO available |
| PS-to-PL transceivers | 4x PS-GTR (6 Gbps) | None | None | None | None |
| PS-GTR protocols | PCIe Gen2, SATA 3.1, USB 3.0, DisplayPort 1.2a, SGMII | N/A | N/A | N/A | N/A |

---

## 2. FPGA Fabric Resource Comparison

### 2.1 AMD Zynq UltraScale+ (16 nm)

Source: ds891, Tables 1/3/5 (CG/EG/EV). Fabric is identical across CG/EG/EV for the same device number.

| Device | Logic Cells | LUTs | Flip-Flops | Block RAM (Mb) | UltraRAM (Mb) | DSP Slices | Max HP I/O | Max HD I/O | GTH | GTY |
|---|---|---|---|---|---|---|---|---|---|---|
| ZU1 | 81,900 | 37,440 | 74,880 | 3.8 | 0 | 216 | 156 | 24 | 0 | 0 |
| ZU2 | 103,320 | 47,232 | 94,464 | 5.3 | 0 | 240 | 156 | 96 | 0 | 0 |
| ZU3 | 154,350 | 70,560 | 141,120 | 7.6 | 0 | 360 | 156 | 96 | 0 | 0 |
| ZU3T | 157,500 | 72,000 | 144,000 | 5.1 | 14.0 | 576 | 52 | 72 | 8 | 0 |
| ZU4 | 192,150 | 87,840 | 175,680 | 4.5 | 14.0 | 728 | 156 | 96 | 16 | 0 |
| ZU5 | 256,200 | 117,120 | 234,240 | 5.1 | 18.0 | 1,248 | 156 | 96 | 16 | 0 |
| ZU6 | 469,446 | 214,604 | 429,208 | 25.1 | 0 | 1,973 | 208 | 120 | 24 | 0 |
| ZU7 | 504,000 | 230,400 | 460,800 | 11.0 | 27.0 | 1,728 | 416 | 48 | 24 | 0 |
| ZU9 | 599,550 | 274,080 | 548,160 | 32.1 | 0 | 2,520 | 208 | 120 | 24 | 0 |
| ZU11 | 653,100 | 298,560 | 597,120 | 21.1 | 22.5 | 2,928 | 416 | 96 | 32 | 16 |
| ZU15 | 746,550 | 341,280 | 682,560 | 26.2 | 31.5 | 3,528 | 208 | 120 | 24 | 0 |
| ZU17 | 926,194 | 423,403 | 846,806 | 28.0 | 28.7 | 1,590 | 572 | 96 | 44 | 28 |
| ZU19 | 1,143,450 | 522,720 | 1,045,440 | 34.6 | 36.0 | 1,968 | 572 | 96 | 44 | 28 |

**Notes:**
- HP I/O: 1.0V to 1.8V, supports SLVS (native MIPI D-PHY), LVDS, SSTL, HSTL
- HD I/O: 1.2V to 3.3V, supports LVCMOS, LVTTL
- GTH max speed: package-dependent (12.5 Gbps in SFVC784, up to 16.375 Gbps in larger packages)
- DSP: 27x18 multiply, 48-bit accumulator, 27-bit pre-adder
- Device suffixes: CG = no GPU/VCU, dual A53; EG = GPU, quad A53; EV = GPU + H.264/H.265 VCU, quad A53

### 2.2 AMD Zynq-7000 (28 nm)

Source: ds190, Tables 1-3.

| Device | PL Equivalent | Logic Cells | LUTs | Flip-Flops | Block RAM (Mb) | DSP Slices | Max HR I/O | Max HP I/O | GTX (max) |
|---|---|---|---|---|---|---|---|---|---|
| Z-7007S | Artix-7 | 23K | 14,400 | 28,800 | 1.8 | 66 | 54 | 0 | 0 |
| Z-7010 | Artix-7 | 28K | 17,600 | 35,200 | 2.1 | 80 | 100 | 0 | 0 |
| Z-7012S | Artix-7 | 55K | 34,400 | 68,800 | 2.5 | 120 | 150 | 0 | 4 GTP |
| Z-7014S | Artix-7 | 65K | 40,600 | 81,200 | 3.8 | 170 | 200 | 0 | 0 |
| Z-7015 | Artix-7 | 74K | 46,200 | 92,400 | 3.3 | 160 | 150 | 0 | 4 GTP |
| Z-7020 | Artix-7 | 85K | 53,200 | 106,400 | 4.9 | 220 | 200 | 0 | 0 |
| Z-7030 | Kintex-7 | 125K | 78,600 | 157,200 | 9.3 | 400 | 100 | 150 | 4 GTX |
| Z-7035 | Kintex-7 | 275K | 171,900 | 343,800 | 17.6 | 900 | 212 | 150 | 8-16 GTX |
| Z-7045 | Kintex-7 | 350K | 218,600 | 437,200 | 19.2 | 900 | 212 | 150 | 8-16 GTX |
| Z-7100 | Kintex-7 | 444K | 277,400 | 554,800 | 26.5 | 2,020 | 250 | 150 | 16 GTX |

**Notes:**
- HR I/O: 1.2V to 3.3V
- HP I/O: 1.2V to 1.8V (available only on Kintex-class Z-7030 and above)
- GTP transceivers: up to 6.6 Gbps (CLG485/SBG485 packages)
- GTX transceivers: up to 12.5 Gbps (FFG676/FFG900 packages)
- DSP: 18x25 multiply, 48-bit accumulator, 25-bit pre-adder
- No native MIPI D-PHY I/O support (requires external resistor network, see XAPP894)
- PCIe: up to Gen2 x8 (Kintex-class devices only)

### 2.3 Intel Cyclone V SoC (28 nm)

Source: cv_5v2, Tables 2-1, 5-4, 5-5. The Cyclone V SoC comes in SE (no transceivers), SX (with transceivers), and ST (with transceivers + PCIe) variants.

| Variant | Member | Logic Elements (K) | ALMs | M10K RAM (Kb) | MLAB (Kb) | Total RAM (Kb) | DSP Blocks (18x18) | Transceivers | PCIe |
|---|---|---|---|---|---|---|---|---|---|
| SE | A2 | 25 | 9,840 | 1,400 | 138 | 1,538 | 36 | 0 | None |
| SE | A4 | 40 | 15,880 | 2,700 | 231 | 2,460 | 84 | 0 | None |
| SE | A5 | 85 | 32,070 | 3,970 | 480 | 4,450 | 87 | 0 | None |
| SE | A6 | 110 | 41,910 | 5,530 | 621 | 6,151 | 112 | 0 | None |
| SX | C2 | 25 | 9,840 | 1,400 | 138 | 1,538 | 36 | 2 (3.125 Gbps) | None |
| SX | C4 | 40 | 15,880 | 2,700 | 231 | 2,460 | 84 | 4 (3.125 Gbps) | None |
| SX | C5 | 85 | 32,070 | 3,970 | 480 | 4,450 | 87 | 6 (3.125 Gbps) | Gen1 |
| SX | C6 | 110 | 41,910 | 5,530 | 621 | 6,151 | 112 | 6 (3.125 Gbps) | Gen1 |
| ST | D5 | 85 | 32,070 | 3,970 | 480 | 4,450 | 87 | 9 (6.144 Gbps) | Gen2 |
| ST | D6 | 110 | 41,910 | 5,530 | 621 | 6,151 | 112 | 9 (6.144 Gbps) | Gen2 |

**Notes:**
- I/O: 1.2V to 3.3V (all banks are HR, no HP banks like Xilinx)
- DSP: 18x18 or 9x9 variable-precision multiply, accumulate
- No native MIPI D-PHY support (requires external resistor network, see Intel AN-754)
- LVDS SERDES: up to ~840 Mbps with passive network for MIPI compatibility
- HPS has its own DDR controller (shared with FPGA via bridges), separate from any FPGA DDR interface
- Enclustra modules using Cyclone V SoC: MA3 (5CSEBA5/5CSXFC6), SA1 (5CSXFC6), SA2 (5CSTFD6D5)

### 2.4 Intel Arria 10 SoC (20 nm)

Source: a10_overview, Table 12.

| Device | Logic Elements (K) | ALMs | M20K RAM (Kb) | MLAB (Kb) | DSP Blocks (var. precision) | 18x19 Multipliers | Transceivers (17.4 Gbps) | GPIO | PCIe Gen3 |
|---|---|---|---|---|---|---|---|---|---|
| SX 160 | 160 | 61,510 | 8,800 | 1,050 | 156 | 312 | 12 | 288 | 1 block |
| SX 220 | 220 | 80,330 | 11,740 | 1,690 | 192 | 384 | 12 | 288 | 1 block |
| SX 270 | 270 | 101,620 | 15,000 | 2,452 | 830 | 1,660 | 24 | 384 | 2 blocks |
| SX 320 | 320 | 119,900 | 17,820 | 2,727 | 985 | 1,970 | 24 | 384 | 2 blocks |
| SX 480 | 480 | 183,590 | 28,620 | 4,164 | 1,368 | 2,736 | 36 | 492 | 2 blocks |
| SX 570 | 570 | 217,080 | 36,000 | 5,096 | 1,523 | 3,046 | 48 | 696 | 2 blocks |
| SX 660 | 660 | 251,680 | 42,620 | 5,788 | 1,687 | 3,374 | 48 | 696 | 2 blocks |

**Notes:**
- I/O: supports 3.0V, 2.5V, 1.8V, 1.5V, 1.2V (via configurable I/O banks)
- DSP: variable-precision, supports 18x19 or 27x27 multiply, floating point capable
- Transceiver speed: up to 17.4 Gbps
- HPS: dual Cortex-A9 @ 1.2 GHz (1.5 GHz overdrive), hard DDR4/DDR3 controller (up to 2400 Mbps)
- No native MIPI D-PHY support
- PCIe: Gen3 x8 hard IP
- Enclustra modules: AA1 (10AS027/10AS048)

### 2.5 Microchip PolarFire SoC (28 nm, non-volatile)

Source: Polarfire_SOC_Product_Overview, Table 2-1.

| Device | Logic Elements (K) | Math Blocks (18x18) | LSRAM Blocks (20 Kb) | uSRAM Blocks (64x12) | Total RAM (Mb) | SERDES Lanes (up to 12.7 Gbps) | PCIe Gen2 EP/RP | Total FPGA I/O (HSIO+GPIO) | MSS I/O |
|---|---|---|---|---|---|---|---|---|---|
| MPFS025T | 23 | 68 | 84 | 204 | 1.8 | 4 | 2 | 108 | 136 |
| MPFS095T | 93 | 292 | 308 | 876 | 6.7 | 4 | 2 | 276 | 136 |
| MPFS160T | 161 | 498 | 520 | 1,494 | 11.3 | 8 | 2 | 312 | 136 |
| MPFS250T | 254 | 784 | 520 | 2,352 | 17.6 | 16 | 2 | 372 | 136 |
| MPFS460T | 461 | 1,420 | 1,460 | 4,260 | 31.6 | 20 | 2 | 468 | 136 |

**Notes:**
- Non-volatile FPGA fabric (flash-based, no bitstream loading needed, instant-on)
- HSIO: supports DDR4 up to 1600 Mbps, LPDDR4, DDR3L (1.8V-1.2V)
- GPIO: supports 3.3V to 1.2V, SGMII, LVDS up to 1.6 Gbps
- No native MIPI D-PHY I/O support (external companion PHY chip required)
- SERDES: multi-protocol (PCIe, SGMII, 10G Ethernet), up to 12.7 Gbps per lane
- PCIe: Gen2 x4 (two independent endpoints/root ports)
- MSS DDR: integrated 36-bit controller, supports DDR4/DDR3/LPDDR4/LPDDR3 with ECC
- DSP: 18x18 multiply with pre-adder, 48-bit accumulator, optional 16-deep coefficient ROM
- Enclustra modules: MP1 (MPFS250T/MPFS460T)

---

## 3. Key Differentiating Features for Product Selection

### 3.1 MIPI D-PHY Support

| Family | Native D-PHY I/O | Vendor MIPI IP | Max Lane Rate | LP Mode Support | Notes |
|---|---|---|---|---|---|
| Zynq UltraScale+ | **Yes** (SLVS in HP banks) | MIPI D-PHY Controller (PG202), CSI-2 RX/TX Subsystem | 1.5+ Gbps | Full (HS + LP natively) | Enclustra verified pinout for XU6, XU61, XU7, XU8, XU9 |
| Zynq-7000 | No | Manual D-PHY config only | ~800 Mbps (with resistor network) | Partial (D0 only for LP) | Requires XAPP894 resistor network. Not tested by Enclustra. |
| Cyclone V | No | No (AN-754 passive network) | ~840 Mbps (with resistor network) | Limited | AN-754 documents approach. No Intel IP available in current Quartus. |
| Arria 10 | No | No | Similar to Cyclone V | Limited | Same resistor-network approach. Intel MIPI D-PHY IP is for Agilex 5/3 only. |
| PolarFire SoC | No (IOD-based) | CSI-2 TX/RX IP (uses IOD blocks) | Depends on IOD config | Via IOD | Functional but requires external D-PHY companion chip for full compliance. Microchip provides CSI-2 IP. |

### 3.2 Video Processing Capabilities

| Family | Hardware Video Codec | GPU | DisplayPort (PS) | Notes |
|---|---|---|---|---|
| Zynq UltraScale+ (EV) | H.264/H.265 encode + decode | Mali-400 MP2 | Yes (DP 1.2a via PS-GTR) | EV variants only. Simultaneous encode/decode. |
| Zynq UltraScale+ (EG) | None | Mali-400 MP2 | Yes (DP 1.2a via PS-GTR) | GPU but no video codec. |
| Zynq UltraScale+ (CG) | None | None | Yes (DP 1.2a via PS-GTR) | Minimal -- no GPU, no codec. |
| Zynq-7000 | None | None | None | All video must be implemented in PL. |
| Cyclone V | None | None | None | All video must be implemented in PL. |
| Arria 10 | None | None | None | All video must be implemented in PL. |
| PolarFire SoC | None | None | None | All video must be implemented in PL. |

### 3.3 External Memory Support

| Family | PS DDR Standard | Max Width | ECC | Max Address Space | PL DDR | Notes |
|---|---|---|---|---|---|---|
| Zynq UltraScale+ | DDR4, DDR3, DDR3L, LPDDR4, LPDDR3 | 64-bit | Yes (64b and 32b) | 32 GB | Yes (via PL MIG) | Most advanced memory subsystem. |
| Zynq-7000 | DDR3, DDR3L, DDR2, LPDDR2 | 32-bit | Yes (16b only) | 1 GB | No (PL has no hard memory controller) | No DDR4 support. 1 GB address limit. |
| Cyclone V | DDR3, DDR3L, LPDDR2 | 32-bit | Yes | 4 GB | Yes (hard FPGA DDR controller) | HPS and FPGA have separate hard DDR controllers. |
| Arria 10 | DDR4, DDR3 | 40-bit (32+ECC) | Yes | Larger | Yes (hard FPGA DDR controller) | DDR4 up to 2400 Mbps. |
| PolarFire SoC | DDR4, DDR3, LPDDR4, LPDDR3 | 36-bit (32+ECC) | Yes | 8 GB | Yes (via FPGA I/O) | MSS DDR controller is 36-bit with ECC. |

### 3.4 PCIe Support

| Family | Max PCIe Gen | Max Lanes | Hard IP | Via | Notes |
|---|---|---|---|---|---|
| Zynq UltraScale+ | Gen2 (PS-GTR), Gen3 (PL GTH) | x4 (PS), x16 (PL) | Yes | PS-GTR or PL transceivers | Gen3 requires GTH in PL, device-dependent. |
| Zynq-7000 | Gen2 | x8 | Yes | PL GTX | Kintex-class devices only (Z-7030 and above). |
| Cyclone V SE | None | N/A | N/A | N/A | SE variants have no transceivers. |
| Cyclone V SX | Gen1 | x4 | Yes | Transceivers | Limited to Gen1. |
| Cyclone V ST | Gen2 | x4 | Yes | Transceivers | |
| Arria 10 SX | Gen3 | x8 | Yes | Transceivers | Hard IP. |
| PolarFire SoC | Gen2 | x4 | Yes (dual) | SERDES | Two independent EP/RP. |

### 3.5 Power and Technology

| Family | Process Node | FPGA Config Type | Typical Core Voltage | Key Power Characteristic |
|---|---|---|---|---|
| Zynq UltraScale+ | 16 nm FinFET+ | SRAM (volatile) | 0.85V | Moderate power. PS and PL on separate power domains. |
| Zynq-7000 | 28 nm | SRAM (volatile) | 1.0V | Lower absolute power (smaller devices), higher per-LUT power than 16nm. |
| Cyclone V | 28 nm | SRAM (volatile) | 1.1V | Low-cost, low-power focus. |
| Arria 10 | 20 nm | SRAM (volatile) | 0.9V (or 0.82V SmartVID) | Up to 40% lower power than previous gen. |
| PolarFire SoC | 28 nm | Flash (non-volatile) | 1.0V / 1.05V | **Lowest power in class.** Non-volatile = no config time, no external config flash. SEU-immune fabric. |

### 3.6 Tool and Ecosystem

| Family | Design Tool | License for Small Devices | OS/SW Ecosystem Maturity | Notes |
|---|---|---|---|---|
| Zynq UltraScale+ | Vivado / Vitis | Free for some devices (check WebPACK) | Mature (PetaLinux, Yocto, Ubuntu) | Largest IP ecosystem for video/image. |
| Zynq-7000 | Vivado / Vitis | Free (WebPACK covers most devices) | Mature but aging (32-bit ARM) | Good community support, many legacy designs. |
| Cyclone V | Quartus Prime | Free (Lite edition) | Moderate (Yocto, Angstrom) | Intel SoC EDS for HPS development. |
| Arria 10 | Quartus Prime | Requires paid license | Moderate | Quartus Pro required for some features. |
| PolarFire SoC | Libero SoC | Free (Silver license) | Growing (Yocto, Buildroot via Mi-V) | RISC-V ecosystem is younger. Renode simulation available. |

---

## 4. Enclustra Module Mapping

Which Enclustra modules use which device family:

| Device Family | Enclustra Modules | Module Family | Connector |
|---|---|---|---|
| Zynq UltraScale+ | XU3 | Mars | SO-DIMM 200-pin |
| Zynq UltraScale+ | XU5 | Mercury | 2x Hirose FX10 |
| Zynq UltraScale+ | XU6, XU61, XU1, XU7, XU8, XU9 | Mercury | 3x Hirose FX10 |
| Zynq UltraScale+ | XZU65, XZU90 | Andromeda | 3x/6x Samtec ADM6 |
| Zynq-7000 | ZX2, ZX3 | Mars | SO-DIMM 200-pin |
| Zynq-7000 | ZX1, ZX5 | Mercury | 2x Hirose FX10 |
| Cyclone V SoC | MA3 | Mars | SO-DIMM 200-pin |
| Cyclone V SoC | SA1 | Mercury | 2x Hirose FX10 |
| Cyclone V SoC | SA2 | Mercury | 3x Hirose FX10 |
| Arria 10 SoC | AA1 | Mercury | 3x Hirose FX10 |
| PolarFire SoC | MP1 | Mercury | 3x Hirose FX10 |

---

## 5. Quick Decision Matrix

Use this matrix to quickly narrow down the device family based on the customer's primary requirement:

| Primary Requirement | Best Family | Rationale |
|---|---|---|
| MIPI CSI/DSI camera interface | Zynq UltraScale+ | Only family with native D-PHY I/O. Enclustra-verified pinouts available. |
| Hardware H.264/H.265 video codec | Zynq UltraScale+ (EV) | Only family with integrated VCU. |
| GPU for graphics/display compositing | Zynq UltraScale+ (EG/EV) | Only family with integrated GPU (Mali-400 MP2). |
| Lowest cost / simplest design | Zynq-7000 or Cyclone V | Mature, cheap, free tools. Good for designs without MIPI or advanced video. |
| Intel/Altera vendor preference | Cyclone V (low-end) or Arria 10 (mid/high) | Only Intel options in portfolio. |
| Highest transceiver count | Zynq UltraScale+ (XZU90) | 76 transceivers (28 GTY + 44 GTH + 4 GTR). |
| PCIe Gen3 | Zynq UltraScale+ or Arria 10 | Both support Gen3. Arria 10 up to x8, ZU+ up to x16. |
| Non-volatile FPGA (instant-on) | PolarFire SoC | Only non-volatile FPGA in portfolio. Flash-based, SEU-immune. |
| RISC-V processor | PolarFire SoC | Only RISC-V option. |
| Lowest power consumption | PolarFire SoC | Non-volatile fabric + low-power design. Lowest static power. |
| Maximum FPGA fabric size | Zynq UltraScale+ (ZU19EG) | 522K LUTs, 1M+ flip-flops, 34.6 Mb BRAM, 36 Mb UltraRAM. |
| Security (TPM) | XU61 or MP1 | Only modules with on-board TPM. |
| Industrial temperature | Most families | Available across most modules. Check specific device variants. |
| USB 3.0 from processor | Zynq UltraScale+ | Only family with USB 3.0 via PS-GTR. Others are USB 2.0 only. |
| DDR4 memory | Zynq UltraScale+, Arria 10, or PolarFire SoC | Zynq-7000 and Cyclone V do not support DDR4. |
| Dual independent DDR interfaces | Zynq UltraScale+ (some modules), PolarFire SoC (MP1) | PS DDR + PL DDR on ZU+. MSS DDR + FPGA DDR on PolarFire. |
