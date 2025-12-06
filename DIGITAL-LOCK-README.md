# Simple 3-bit Digital Lock (Logisim)

Description
-----------
This is a simple logic-based digital lock that takes three 1-bit inputs A, B, and C and lights an "UNLOCKED" LED only when the correct 3-bit password is entered.

Default password used in this design: binary 101
- A = 1
- B = 0
- C = 1

Boolean logic
-------------
We want UNLOCKED = 1 only for input (A,B,C) = (1,0,1).

A straightforward Boolean expression for that single minterm is:
UNLOCKED = A AND (NOT B) AND C

Using logical operators:
UNLOCKED = A & ~B & C

Truth table
-----------
A B C | UNLOCKED
0 0 0 | 0
0 0 1 | 0
0 1 0 | 0
0 1 1 | 0
1 0 0 | 0
1 0 1 | 1  <-- the only unlocked combination
1 1 0 | 0
1 1 1 | 0

How to build this in Logisim-evolution
--------------------------------------
1. Open Logisim-evolution and create a new circuit (File → New).

2. Add three input pins:
   - From the wiring toolbar pick "Pin".
   - Place three pins and label them "A", "B", and "C".
   - Set each pin's bit width to 1 (default) and set labels so you can identify them.

3. Add an inverter (NOT) for B:
   - From the Gates toolbar choose "NOT".
   - Connect input B to the NOT gate input.
   - The output of this gate is ~B.

4. Add a 3-input AND gate:
   - From the Gates toolbar choose "AND".
   - If Logisim's AND gate defaults to 2 inputs, either:
     - Change the AND gate's "Inputs" attribute to 3 (select the AND, then modify "Data" → "Inputs" to 3), or
     - Use two 2-input AND gates: first AND A and ~B, then AND the result with C.
   - Connect A, ~B, and C to the inputs of the 3-input AND.

5. Add an LED (Output):
   - From the Input/Output toolbar choose "LED".
   - Connect the AND output to the LED.
   - Optionally add a label "UNLOCKED" next to the LED.

6. (Optional) Add a constant 1 and constant 0 or show pin labels:
   - For testing you can use the pin toggle or place "Constant" components to force desired inputs.

7. Test the circuit:
   - With the poke tool, toggle A, B, and C to verify only the combination A=1, B=0, C=1 lights the LED.

Schematic (logical)
-------------------
Inputs: A, B, C

      A ----\
            \
             AND ---- UNLOCKED LED
      ~B ---/  \
               \
      C --------/

Where ~B is the output of NOT(B).

Variations / enhancements
-------------------------
- Multiple valid passwords: OR together multiple minterms. For example, to allow 101 or 011: UNLOCKED = (A & ~B & C) OR (~A & B & C).
- Use a 3-bit comparator: If you want to compare (A,B,C) to some constant password P2P1P0, you can use XNOR gates per bit and AND their outputs: UNLOCKED = XNOR(A,P2) & XNOR(B,P1) & XNOR(C,P0).
- Add a latch or memory to keep the unlocked state until reset.
- Add debounce or edge detection if inputs come from mechanical switches.

If you want me to change the password, the file path, or add extra features (like multiple passwords, a reset, or a stored latch), tell me which changes you'd like.
