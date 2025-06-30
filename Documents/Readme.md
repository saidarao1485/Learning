### ARM Processor:

* ➤ It is a processor.
* ➤ Designed by ARM Limited or ARM Holding
  *(Latest name of ARM Limited)* 

### Block Diagram:

```
         +----------------+
         | ARM Processor  |
         +----------------+
                 |
         +----------------+
         |    Memory      |
         +----------------+
                 |
   +--------+    +------+    +--------+
   |  UART  |    | ADC  |    | Timer  |
   +--------+    +------+    +--------+
``` 
### ARM-based SoC:

* SoC → *System on Chip* 
### SoC Manufacturers:

1. Qualcomm
2. Samsung
3. Broadcom
4. NXP Semiconductors
5. Atmel



### 🔸 SoC’s (System on Chips):

1. Snapdragon *(by Qualcomm)*
2. BCM2708 *(by Broadcom)*
3. LPC2148 *(by NXP Semiconductors)*

   *(Used in Vectors board)*
4. AM335x *(by Sitara)* 

### 🔸 ARM Applications:

1. Camera
2. Router
3. SIM card
4. Pointing device
5. Mobile phone 

### 🔸 Embedded Linux Boards (Single Board Computers):

1. Raspberry Pi *(BCM2708)*
2. BeagleBone Black *(AM335x)*

   * OR
     BeagleBone White *(AM335x)*
3. Cubieboard
4. FriendlyARM
5. etc.

* ARM processor is a RISC type processor.
* RISC type CPU uses fixed-length instructions.
* In RISC, mostly single clock cycle instructions are available. 

### ⭐ 4 Rules of Designing RISC-Based CPU:

1. Instruction Set
2. Registers
3. Pipelining
4. Load & Store Architecture 

### 🔹 Notes:

* More number of registers are used because register access is faster compared to memory.
* To speed up execution, pipelined architecture is used. 
### ❓ Question: Pipelining – How does it speed up execution?

* Pipelining speeds up execution by fetching the next instruction while the previous ones are being decoded or executed. 
### 📊 Example Table: Instruction Pipeline

| Cycle   | Fetch | Decode | Execute |
| ------- | ----- | ------ | ------- |
| Cycle 1 | ADD   |        |         |
| Cycle 2 | SUB   | ADD    |         |
| Cycle 3 | CMP   | SUB    | ADD     |

#### Instruction Clock Cycle Table:

| Instruction | Opcode |
| ----------- | ------ |
| CMP         | 0x03   |
| SUB         | 0x02   |
| ADD         | 0x01   |
| MUL         | 0x0A   | 

### 🕒 ARM instructions take 1 clock cycle to execute.

* ➤ Only the first instruction needs 3 clock cycles to execute.
* ➤ The rest follow with only 1 clock cycle each. 

### ⚙️ Instruction Queue and Pipelining

* Some processors use an instruction queue to speed up execution
  → Example: 8086 Intel
* Some processors use pipeline architecture for execution speedup.
* All RISC-based µP (microprocessors) → use pipeline architecture. 

### ❌ Pipelining – When It Fails

#### ❗ Failure Case: During loop execution

##### Code Example:

```c
while (condition) {
    1st
    2nd
    3rd
    4th
}
```

##### Pipeline Table:

| Cycle  | Fetch | Decode | Execute |
| ------ | ----- | ------ | ------- |
| Cycle1 | Cmd^m |        |         |
| Cycle2 | 1st   | Cmd^m  |         |
| Cycle3 | 2nd   | 1st    | Cmd^m   |
| Cycle4 | 3rd   | 2nd    | 1st     |

> `Cmd^m` = Command from loop condition. 

### ❗ Exceptions When Pipeline Will Be Flushed:

1. Looping condition
2. Interrupt occurs
3. ISA is called
4. If–else statement 
### 🧠 RISC Load and Store Characteristics:

* In RISC, only Load & Store instructions can access memory, reducing memory access time.
* In RISC, a separate set of Load/Store instructions interact with memory. 

### 🏗️ Load and Store Architecture:

* Only Load and Store instructions access memory.
* ➤ This reduces memory access time.
* ➤ Since the microprocessor interacts primarily with registers,
  RISC-based processing is also called:
  👉 "Register Intensive Processing" 

### ➕ Coming Up Next:

### 🟣 ARM7 Architecture Features

1. ✅ Low power, high performance processor
   *(Works on 3.3V)*

2. ✅ ARM working frequency is 60 MHz

3. ✅ 1 machine cycle = 1 instruction execution

4. ✅ ARM7 core uses RISC Architecture & Von Neumann type bus architecture

5. ✅ ARM7 is a 32-bit processor core (CPU)

6. ✅ ARM7 supports 3-stage pipeline architecture:

   * Fetch
   * Decode
   * Execute

7. ✅ Reduced gate count design, suitable for small, low-power, high-performance implementations

8. ✅ Die size is very small

9. ✅ ARM7 core supports on-chip hardware debugging technology 

### 🔧 JTAG Technology:

* ➤ After downloading the program, we can debug step-by-step using a JTAG cable.
* ➤ 64-pin controller:

  * 16–20 pins are reserved for hardware debugging


### 🟣 Additional ARM7 Architecture Features:

10. ✅ Uniform and fixed-length instruction set
      – Simplifies instruction decoding.

11. ✅ Load and store multiple instructions
      – Maximizes data throughput.

12. ✅ ARM7 core supports 32-bit registers
      – 16 registers are available for use
      – Each peripheral has a minimum of 10 registers

---

### 📊 Block Diagram (Label Summary):

* ARM7 Core connected to:

  * Memory
  * Timer
  * UART (with its own register set)
  * RTC (with its own register set)

---

### 📘 References for Further Learning:

* ARM System Developer's Guide
  – by *Andrew Sloss*
  – (Covers theory information)

* LPC214x User Manual
  – (Covers practical information)
  

13) ARM7 core supports 7 modes of operation.

*user* → non-privileged mode
  *(user can't write into the some Registers)*

*system*

*supervisor*

*FIQ*

*IRQ*

*Abort*

*undefined*

→ privileged modes
*(user will be able to write on some Registers)*

---

14) In ARM based SoC, overvoltage protection ckt not inside CPU but on its SoC as a chip.

---

☀️ on μC RTOS can be use GPOS

* GPOS → on microprocessor only
  *(general purpose operating system)*

GPOS size is large.
RTOS size is small.

---

➜ In mobile phone 98% to 99% use ARM Cortex.

ARM Cortex (32 bits and 64 bits).

Here is the extracted content from the second image:

---

### ARM Versions:

* ARM 7 → *only for study purpose*
* ARM 9
* ARM 11
* ARM Cortex

---

### ARM-based SoC – ARM Controller Block Diagram:

```
     +-------------+
     |  ARM Core   |
     | Processor   |
     +-------------+
           |
  -------------------------
  |     |     |      |     |
UART   I2C  Timer  Memory
```

Label: *ARM based SoC - ARM Controller*

---

### Pipelining Stages:

* ARM 7 → (3-stage pipeline)
* ARM 9 → (5-stage pipeline)
* ARM 11 → (8-stage pipeline)

---

### ARM Cortex Families:

* Series A → *in mobile phone*
* Series M → *microcontroller*
* Series R → *Real Operating System*

### Interrupts and Exceptions

* When Interrupt or Exception occurs, ARM mode is changed.

#### Diagram:

```
   +-----+       Interrupt
   | CPU | <-----------------+
   +-----+                  |
                            |
                        +----------+
                        | External |
                        |  Device  |
                        +----------+
```

* Interrupt: Stops the external event.
  It is an asynchronous event.

---

### *✴✴✴ Exception ✴✴✴*

* An exception is a predefined error condition.
  Examples:

  * Division by zero
  * Illegal instruction
  * Segmentation fault

* Due to interrupt or exception, CPU switches to any one of the 7 modes.

---

### Interview Question ::

Explain about modes:

---

#### 1) User Mode:

* Normal program execution state.
* Upon reset, startup code is executed and it will clear the memory registers.


### Note:

This mode can only be changed when an interrupt or exception is generated.

* Through instruction, the processor changes the mode of exception, then the user has to modify the CPSR register.

---

### CPSR = Current Program Status Register

---

### In 3 cases, mode is changed:

1. By interrupt occurs
2. By exception
3. By CPSR register

---

* In user mode, CPSR is a read-only register, can't be changed.

* In user mode:

  ```asm
  MOV CPSR, #data
  ```

  * The assembler won’t generate an error, but it won’t be able to modify CPSR.

---

### 2) System Mode

* Privileged mode of user.

#### Flow:

```
Startup code
     ↓
   main()
     ↓
   user mode
```

### 🔽 How to go to System Mode:

* With using CPSR (because CPSR can’t be accessed in user mode).

---

### 3) Supervisor Mode

* Mode of core after reset.

#### Flow:

```
After Reset
    ↓
Startup Code
    ↓
main()
 ↖         ↘
Supervisor Mode
```

---

* After reset and before `main()`, the processor will be in supervisor mode.
* Default mode of ARM processor.
* After reset the µP (microprocessor), the startup code is run in supervisor mode.
* Only in supervisor mode, the MSR instruction will be available using which we can change the mode by modifying CPSR.


### 4) FIQ Mode (Fast Interrupt Request)

* Fast Interrupt Request.
* Low latency interrupt service.

Low Latency:
Means CPU response to interrupt is faster.

#### Diagram:

```
Interrupt
   ↑
  ARM7 TDMI → MAC Unit  
        ↑
   Core Processor Name  
        ↑
  H/W Debug Technology
```

---

### 5) IRQ Mode (Interrupt Request)

* Interrupt Request.
* Compared to FIQ mode, IRQ latency is more.

---

### 6) Abort Mode

* This mode is selected when data or instruction fetch is aborted.
* ARM processor attempts to fetch an instruction from an address without the correct access permission, then the processor goes to the Abort mode.

---

📏 Size of ARM Program Counter = 32-bit


### LPC2148 Memory Map

* 4 GB
* ↓
* 82 KB RAM
* ↓
* Reserved
* ↓
* 512 KB Flash Memory
* ↓
* 0 GB

---

### 7) Undefined Mode

* This mode is selected when undefined instruction is fetched.

  * Example: *illegal opcode* (illegal instruction).
* Then microprocessor (µp) goes to this undefined mode.

---

### 8) ARM7TDMI-S Processor

* ARM7 = Family name
* T = THUMB instruction set
* D = Hardware Debug Technology
* M = MAC Unit
* I = Interrupt (FIQ)
* S = Synthesize


### 9) THUMB Instruction Mode

* It is also called a 16-bit instruction set.

| Family | Architecture | Instruction Set Support     |
| ---------- | ---------------- | ------------------------------- |
| ARM7       | ARMv3            | Only 32-bit instruction set     |
| ARM7       | ARMv4T           | 16-bit & 32-bit instruction set |

📌 Note:

* 16-bit instruction set = THUMB instruction set
* 32-bit instruction set = ARM instruction set

---

### 10) Processor Operating Status

1. ARM State
2. THUMB State

| ARM State                      | THUMB State                         |
| ---------------------------------- | --------------------------------------- |
| Processor executes 32-bit word | Processor executes 16-bit half word |
| aligned ARM instruction.           | aligned instruction.                    |

---

### Bit Definitions

* 64 bits = double word
* 32 bits = word
* 16 bits = half word
* 8 bits = byte
* 4 bits = nibble

### 🔄 Upon Reset, ARM Processor:

* Enters Supervisor mode
* Executes ARM instruction (32-bit instruction)

---

### 📊 Instruction Count in ARM7:

```
ARM Instruction   = 51  
THUMB Instruction = 81
```

---

### 🔁 Mode Switching:

```
[ ARM mode ] ⇄ [ THUMB mode ]
```

---

### 🔃 THUMB Instructions:

* Dynamically decompressed to ARM instructions during execution.
* Helps in reducing instruction size and improving memory efficiency.

---

### 📉 Program Size Over UART:

* ARM ➝ UART: Program size is large
* THUMB ➝ UART: Program size is small

---

### 📦 Instruction Flow Diagram:

```
THUMB instruction → Pipeline → THUMB Decompressor → Decoded
```

---

### ✅ Advantage of THUMB:

1. Reduces the code size.


### 🛠️ Hardware Synthesis:

* Done using software (VHDL).

---

### 🔄 State Change via Bx Instruction:

* Switch between:

  * ARM to THUMB
  * THUMB to ARM

---

### 📌 ARM7 Modes:

* 8 modes available in ARM7 processor.

---

### 📊 Registers in ARM7:

* Total: 37 registers
* All are 32-bit registers.

---

### 🧠 Register Usage:

* 16 registers are used in USER or SYSTEM mode.
* Remaining registers are hidden and called Banked Registers.

---

### 👻 Invisible Registers = Banked Registers

---

### 📦 Banked Register Representation (Concept from 8051 RAM):

```
Banked Register Layout:
------------------------
| R0 to R7 (RB3)       |
| R0 to R7 (RB2)       |
| R0 to R7 (RB1)       |
| R0 to R7 (RB0)       |
```

---

### 🧮 Register Breakdown in ARM:

* Available for user: 16 registers
* Banked Registers: 37 - 16 = 21 registers

```
Banked Registers = 21 (Invisible Registers)

```
The image shows a handwritten note on ARM7 Register Set. The content of the note is as follows:
* ARM7 Register Set *
Ro
R1
R2
:
A2
General purpose Registers
Special Function Registers
R13 (Stack pointer) (SP)
R14 (Link Register) (LR)
R15 (Program Counter) (PC)
all registers of ARM7 can hold the data or address.
eg: mov Ro, #data is support in ARM.
Return address is store into Link register.
3 case :-
Function Call.
Interrupt.
Mode change.
ARM7 Stack is descending Stack.
Stack size = 4 bytes.
with every push instruction the sp will be decremented by 4 bytes.
Instruction to write into program counter is present in ARM7.
Meta AI response: The image shows a handwritten note on ARM7 Register Set.
The content of the note is as follows: * ARM7 Register Set * Ro R1 R2 : A2 General purpose Registers Special Function Registers R13 (Stack pointer) (SP) R14 (Link Register) (LR) R15 (Program Counter) (PC) all registers of ARM7 can hold the data or address. eg: mov Ro, #data is support in ARM.
Return address is store into Link register. 3 case :- Function Call. Interrupt. Mode change.
ARM7 Stack is descending Stack. Stack size = 4 bytes. with every push instruction the sp will be decremented by 4 bytes.
Instruction to write into program counter is present in ARM7.
