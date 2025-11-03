# 🧠 Toy OS Simulator

A two-phase operating system simulator that demonstrates core OS concepts — from basic instruction execution to advanced memory management with paging.

---

## 📁 Project Structure

```
Toy-OS-Simulator/
│
├── Phase-1/
│   ├── phase1.cpp           # Basic OS simulation source code
│   ├── input_Phase1.txt     # Job input file with control cards
│   └── output.txt           # Execution output
│
├── Phase-2/
│   ├── ph2.cpp              # Memory management simulation source code
│   ├── input_phase2.txt     # Process and memory operation commands
│   └── output.txt           # Paging simulation output
│
└── README.md                # This file
```

---

## 🚀 Quick Start

### Phase 1 — Basic OS Execution

```bash
cd Phase-1
g++ phase1.cpp -o phase1
./phase1
```

**Input:** `input_Phase1.txt`  
**Output:** `output.txt`

### Phase 2 — Memory Management & Paging

```bash
cd Phase-2
g++ ph2.cpp -o ph2
./ph2
```

**Input:** `input_phase2.txt`  
**Output:** Console and/or `output.txt`

---

## 🧩 Phase 1 — Basic OS Simulation

### 🎯 Objective

Simulate a simple operating system that can:
- Load and execute user programs from input files
- Allocate memory for processes
- Execute CPU instructions
- Handle I/O operations through interrupts

This phase establishes the foundation of **process management** — mimicking how an OS loads and runs batch jobs.

### 📝 Input File Format

The input file (`input_Phase1.txt`) contains simulated jobs using control cards:

| Control Card | Purpose |
|--------------|---------|
| `$AMJ` | Start of job (Assign Memory for Job) |
| `$DTA` | Start of data section |
| `$END` | End of job |

**Example:**
```
$AMJ000100050001
GD20 PD20 H
$DTA
HELLO WORLD
$END0001
```

### ⚙️ System Components

| Component | Description |
|-----------|-------------|
| **Memory** | 100 blocks × 4 bytes each (simulates RAM) |
| **Registers** | IR (Instruction Register), R (General Purpose), IC (Instruction Counter), C (Condition Flag) |
| **MOS** | Master Operating System — handles interrupts (READ, WRITE, TERMINATE) |
| **Buffer** | Simulates I/O buffer for data transfer |

### 💻 Instruction Set

| Instruction | Description |
|-------------|-------------|
| `GD xx` | **Get Data** — Read from input, load into memory block xx |
| `PD xx` | **Put Data** — Write memory block xx to output |
| `LR xx` | **Load Register** — Load memory xx into register R |
| `SR xx` | **Store Register** — Store R into memory xx |
| `CR xx` | **Compare Register** — Compare R with memory xx |
| `BT xx` | **Branch Toggle** — Jump to xx if condition C is true |
| `H` | **Halt** — Stop execution |

### 🔔 Interrupt Handling

When the CPU needs I/O or must stop, it sets **SI (System Interrupt)**:

- **SI = 1**: READ (GD instruction)
- **SI = 2**: WRITE (PD instruction)
- **SI = 3**: TERMINATE (H instruction)

Control transfers to the MOS, which performs the requested operation.

### 📤 Output

Results are written to `output.txt`:
```
HELLO WORLD
```

### 🧠 Key Learning Points

✅ How an OS loads, runs, and terminates programs  
✅ Instruction cycle: **Fetch → Decode → Execute**  
✅ I/O handling through software interrupts  
✅ Register-memory interaction basics

---

## 🧮 Phase 2 — Memory Management & Paging

### 🎯 Objective

Extend the basic OS with realistic **Memory Management Unit (MMU)** simulation:
- Virtual-to-physical address translation
- Page tables and TLB (Translation Lookaside Buffer)
- Page fault handling and replacement policies

### ⚙️ System Components

| Component | Description |
|-----------|-------------|
| **Page Table** | Maps virtual pages to physical frames |
| **TLB** | Small cache for fast address translation (4 entries) |
| **Page Fault Handler** | Loads missing pages into memory |
| **Replacement Policy** | FIFO (First In First Out) for page replacement |
| **PCB** | Process Control Block — tracks process ID, pages, faults |

### 🔄 Paging Workflow

1. Program issues memory access → `ACCESS 1 1024`
2. OS checks **TLB**:
   - **Hit** → Fast translation ✅
   - **Miss** → Check Page Table
3. If page not in memory → **Page Fault**:
   - Load page into free frame
   - If memory full → Replace page (FIFO)
   - Update TLB
4. Perform read/write on resolved physical frame

### 💻 Supported Commands

| Command | Description |
|---------|-------------|
| `CREATE <pid> <pages>` | Create new process with N pages |
| `ACCESS <pid> <address>` | Read from memory address |
| `WRITE <pid> <address>` | Write to memory address |
| `MEMMAP` | Display memory allocation map |
| `STATS` | Show TLB hits/misses, page faults, free frames |
| `TERMINATE <pid>` | Free all memory for process |

### ⚙️ Configuration

| Parameter | Value |
|-----------|-------|
| Page Size | 1024 bytes |
| Physical Memory | 64 frames |
| Virtual Memory | 256 pages per process |
| TLB Size | 4 entries |

### 📊 Output

The simulator logs:
- Address translations
- TLB hits/misses
- Page replacements
- Page fault statistics

### 🧠 Key Learning Points

✅ How real OS handles virtual memory  
✅ Paging and TLB operation in CPUs  
✅ Dynamic page fault resolution  
✅ Process memory tracking via PCB

---

## 📊 Comparison: Phase 1 vs Phase 2

| Concept | Phase 1 | Phase 2 |
|---------|---------|---------|
| **Purpose** | Basic OS job execution | Virtual memory & paging |
| **Memory Model** | Simple 100×4 memory array | Paging + TLB + Page Table |
| **Operations** | Instructions (GD, PD, H, etc.) | Commands (ACCESS, CREATE, etc.) |
| **Interrupts** | READ/WRITE/TERMINATE | Page Faults, TLB Misses |
| **Focus** | Instruction Cycle & I/O | Memory Management & Translation |

---

## 🛠️ Requirements

- **Compiler:** g++ (or any C++ compiler)
- **C++ Standard:** C++11 or later
- **OS:** Linux, macOS, or Windows (with MinGW)

---
