# 🧠 Toy OS Project

This project simulates a simple **Toy Operating System** built in two phases:

- **Phase 1:** Basic instruction execution, memory management, and I/O operations.  
- **Phase 2:** Paging, Memory Management Unit (MMU), and TLB simulation.

---

## 📁 Folder Structure
ToyOS/
│
├── Phase1/
│ ├── phase1.cpp
│ ├── input_Phase1.txt
│ 
│
├── Phase2/
│ ├── ph2.cpp
│ ├── input_phase2.txt
│ 
│
├── README.md
└── .gitignore

yaml
Copy code

---

## 🧮 Compilation & Execution Commands

### ▶️ Phase 1
```bash
cd Phase1
g++ phase1.cpp -o phase1
./phase1
Output: output.txt will be generated in the Phase1 folder.

▶️ Phase 2
bash
Copy code
cd Phase2
g++ ph2.cpp -o ph2
./ph2
Output: output.txt will be generated in the Phase2 folder.

🧩 Toy OS — Phase 1 🧠
🧩 Overview
This phase simulates a basic operating system environment that loads, interprets, and executes simple user programs from an input file.
It models essential OS concepts such as:

Memory allocation

Instruction execution

Register operations

Simple I/O handling via interrupts

The simulation reads control cards ($AMJ, $DTA, $END) and program instructions from an input file (input_Phase1.txt).

⚙️ Components
1. Virtual Machine (VM)
The VM class manages:

Memory (100 × 4 bytes): stores program instructions and data.

Registers:

IR — Instruction Register

R — General-purpose Register

IC — Instruction Counter

C — Toggle flag (used for conditional branching)

SI — System Interrupt indicator

Buffer: Temporary storage for I/O operations.

2. Master and Slave Modes
Master Mode (MOS): Handles OS-level operations such as READ, WRITE, and TERMINATE.

Slave Mode (User Program Execution): Executes user-level instructions until an interrupt occurs.

🧮 Supported Instructions
Instruction	Operation
GD xx	Get Data — reads a line from input into memory starting at block xx.
PD xx	Put Data — writes a memory block xx to output.
H	Halt — terminates program execution.
LR xx	Load Register — loads data from memory block xx into register R.
SR xx	Store Register — stores contents of R into memory block xx.
CR xx	Compare Register — compares R with memory block xx, sets toggle flag C.
BT xx	Branch Toggle — jumps to memory block xx if C is true.

📂 Input Format
Example (input_Phase1.txt):

bash
Copy code
$AMJ000100050001
GD20 PD20 H
$DTA
HELLO WORLD
$END0001
Explanation:
$AMJ — Start of job

$DTA — Start of data section

$END — End of job

🧠 Learning Outcomes
Understanding instruction execution cycles.

Simulating interrupts and basic OS control.

Implementing minimal memory management.

⚙️ Toy OS — Phase 2 🔧
🧩 Overview
This phase extends the Toy OS into a paging and memory management simulator that mimics the behavior of a real MMU (Memory Management Unit).
It introduces:

Virtual-to-physical address translation

Page tables and TLB (Translation Lookaside Buffer)

Page faults and replacement policies

Process creation, termination, and statistics reporting

⚙️ Core Components
1. Memory Management Unit (MMU)
Maintains a page table per process.

Handles page faults, TLB hits/misses, and page replacements (FIFO policy).

Simulates interrupts such as Page Faults and Segmentation Faults.

2. Process Control Block (PCB)
Each process tracks:

Process ID (pid)

Page Table entries

Allocated pages

Page fault count

Current state (NEW, READY, RUNNING, WAITING, TERMINATED)

3. Translation Lookaside Buffer (TLB)
Stores recent virtual-to-physical page mappings.

Uses FIFO replacement when full.

Tracks TLB hit/miss statistics.

🧮 Supported Commands
Command	Description
CREATE <pid> <pages>	Creates a new process with the given number of pages.
ACCESS <pid> <address>	Accesses a virtual address (read). May trigger a page fault.
WRITE <pid> <address>	Writes to a virtual address. Marks the page as dirty.
MEMMAP	Displays current memory allocation for all processes.
STATS	Prints TLB hit/miss rates and free frame info.
TERMINATE <pid>	Terminates a process and frees its memory.

📂 Input Format
Example (input_phase2.txt):

pgsql
Copy code
CREATE 1 10
ACCESS 1 0
WRITE 1 512
ACCESS 1 1024
MEMMAP
STATS
TERMINATE 1
💡 Paging Configuration
Parameter	Value	Description
Page Size	1024 bytes	Each page = 1 KB
Physical Memory	64 frames	64 KB total
Virtual Memory	256 pages	256 KB per process
TLB Size	4 entries	FIFO replacement

🧠 Learning Outcomes
Implementation of paging and address translation.

Simulation of TLB caching and replacement.

Handling of page faults, segmentation faults, and process lifecycle.

Understanding low-level memory management in operating systems.

🏁 Summary
Phase	Focus	Key Concepts
Phase 1	Basic OS simulation	Instruction execution, memory & I/O operations
Phase 2	Advanced memory management	Paging, TLB, page faults, process control