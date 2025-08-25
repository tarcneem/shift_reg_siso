# 4-bit Serial-In Serial-Out (SISO) Shift Register

This project implements a simple **4-bit Serial-In Serial-Out shift register** in Verilog, along with a self-checking testbench.

---

## 🔹 The Model (`shift_reg_siso.v`)

- **Reset**: Active-low (`reset_n=0`) clears the register to `0000`.
- **Shift operation**:  
  - On every rising edge of `clk`, all bits shift left.  
  - The input bit `sdi` enters at the rightmost position.  
  - The leftmost bit (`siso[3]`) comes out as `sdo`.

➡️ In simple words: a bit pushed into `sdi` will travel across the 4 positions until it pops out at `sdo` after 4 clocks.

---

## 🔹 The Testbench (`tb_shift_reg_siso.v`)

- Generates a **1 MHz clock**.
- Applies **reset** to clear the register.
- Drives test bits on `sdi` (like injecting beads into a pipe).
- Uses a **reference model** inside the testbench that shifts the same way as the DUT.
- Compares the DUT against the reference **on every clock edge**:
  - If they match → continues.
  - If they don’t match → prints an **ERROR**.
- `$monitor` shows the state of DUT and reference so you can **see the bit moving** through the register.

➡️ In simple words: instead of manually checking the output, the testbench works like a **scoreboard** that automatically verifies the DUT.

---

## 🔹 How to Run

### EDA Playground
1. Create a new Verilog playground.
2. Paste both `shift_reg_siso.v` and `tb_shift_reg_siso.v`.
3. Select Icarus/Verilator and run.  
   - View console for `$monitor` output.  
   - Use EPWave (if enabled) to see waveforms.

