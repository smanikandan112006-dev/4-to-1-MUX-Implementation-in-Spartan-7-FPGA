# 4:1 Multiplexer Implementation in Spartan-7 FPGA

## Aim
To design, synthesize, and implement a 4:1 Multiplexer using Verilog HDL on a Spartan-7 FPGA using Xilinx Vivado Design Suite.

---

## Apparatus Required
| S.No | Apparatus / Software | Specification / Description |
|------|----------------------|-----------------------------|
| 1 | FPGA Board | Xilinx Spartan-7 development board  |
| 2 | Software | Xilinx Vivado Design Suite  |
| 3 | Cable | USB Programming Cable (JTAG/USB-JTAG) |

---

## Theory
A **4:1 multiplexer** selects one of four data inputs (i0..i3) and routes it to a single output y, based on two select lines sel[1:0].

**Truth table**

| S1 | S0 | Y   |
|----|----|-----|
| 0  | 0  | D0  |
| 0  | 1  | D1  |
| 1  | 0  | D2  |
| 1  | 1  | D3  |

**Logic Diagram:**
<img width="463" height="368" alt="image" src="https://github.com/user-attachments/assets/7e2b9a82-5482-4265-8007-4c3761706314" />

---

## Procedure (Vivado Design Suite)

1. **Create Project**
   - Open Vivado → *Create New Project*.
   - Name project `MUX_4to1_Spartan7`. Select *RTL Project*, enable *Do not specify sources at this time* (or add immediately).
   - Choose the correct Spartan-7 device/board for your hardware.

2. **Create Design Source**
   - Flow Navigator → *Add Sources* → *Add or Create Design Sources*.
   - Create file `mux4to1.v` and type the Verilog code.

3.  **Add Constraints**
   - Add XDC file `mux4to1.xdc` and map inputs/outputs to board pins.

4.  **Synthesize & Implement**
   - Run *Synthesis* → inspect warnings/errors.
   - Run *Implementation* → review timing and utilization.

5. **Generate Bitstream & Program**
   - Generate Bitstream.
   - Open *Hardware Manager* → connect to target → Program device with `.bit` file.
   - Verify outputs on LEDs/scope.
---
## Verilog Program (`mux4to1.v`)

```verilog
`timescale 1ns / 1ps

module mux4(I,S,y);
input [3:0]I;
input [1:0]S;
output y;
wire [4:1]W;
and g1(W[1],(~S[0]),(~S[1]),I[0]);
and g2(W[2],(~S[0]),S[1],I[1]);
and g3(W[3],S[0],(~S[1]),I[2]);
and g4(W[4],S[0],S[1],I[3]);
or g5(y,W[1],W[2],W[3],W[4]);
endmodule

```
## Constraint file for Seven-Segment Display
```
set_property -dict {PACKAGE_PIN V2 IOSTANDARD LVCMOS33} [get_ports {I[0]}]
set_property -dict {PACKAGE_PIN U2 IOSTANDARD LVCMOS33} [get_ports {I[1]}]
set_property -dict {PACKAGE_PIN U1 IOSTANDARD LVCMOS33} [get_ports {I[2]}]
set_property -dict {PACKAGE_PIN T2 IOSTANDARD LVCMOS33} [get_ports {I[3]}]
set_property -dict {PACKAGE_PIN K2 IOSTANDARD LVCMOS33} [get_ports {sel[0]}]
set_property -dict {PACKAGE_PIN K1 IOSTANDARD LVCMOS33} [get_ports {sel[1]}]
set_property -dict {PACKAGE_PIN G1 IOSTANDARD LVCMOS33} [get_ports {y}]
```
## FPGA Implementation Output

![WhatsApp Image 2025-11-18 at 22 51 49_5cea61d2](https://github.com/user-attachments/assets/0eb73dfe-63c6-47d9-86c9-7d4255847ce8)


---

## Conclusion

The 4:1 multiplexer was successfully designed,synthesized, and implemented (bitstream generated) in the Spartan-7 FPGA. The output matches the expected truth table.
