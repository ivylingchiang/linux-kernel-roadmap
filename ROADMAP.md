# 🗺 Linux Kernel & System Software Roadmap

> **Goal:** From Zero to Kernel Engineer / System Software Developer.  
> **Philosophy:** `Theory × Source Code × Experiments × Implementation × Summary`

---

## 📅 12-Month High-Level Timeline


```

Month 1       Months 2-3     Months 4-5     Months 6-8     Month 9      Months 10-11    Month 12
┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌────────────┐  ┌────────────┐
│ Phase 0  │  │ Phase 1  │  │ Phase 2  │  │ Phase 3  │  │ Phase 4  │  │  Phase 5   │  │  Phase 6   │
│ Env Setup│─>│  CS:APP  │─>│Linux Prog│─>│ Kernel   │─>│  Kernel  │─>│ Source     │─>│ Portfolio  │
│  & Tools │  │ Core     │  │ & POSIX  │  │ Internals│  │ Modules  │  │ Reading    │  │ Projects   │
└──────────┘  └──────────┘  └──────────┘  └──────────┘  └──────────┘  └────────────┘  └────────────┘

```

| Timeframe | Phase | Focus Area | Primary Deliverables | Status |
| :--- | :--- | :--- | :--- | :---: |
| **Month 1** | **Phase 0** | Environment & Toolchain | QEMU + GDB Debugger, Kernel Build | 🟡 |
| **Months 2–3** | **Phase 1** | Computer Systems (CS:APP) | `mini-readelf`, Memory Simulator | ⚪ |
| **Months 4–5** | **Phase 2** | Linux System Programming | Mini Shell, `mini-ps`, `mini-strace` | ⚪ |
| **Months 6–8** | **Phase 3** | Linux Kernel Internals | Subsystem Tracing & Benchmarks | ⚪ |
| **Month 9** | **Phase 4** | Kernel Modules & Drivers | LKM Suite, Character Device Driver | ⚪ |
| **Months 10–11**| **Phase 5** | Kernel Source Code Analysis | Function Call Graphs & Flowcharts | ⚪ |
| **Month 12** | **Phase 6** | Portfolio Projects & Patch | Capstone Tools, Upstream Kernel Patch | ⚪ |

---

## 📁 Directory Creation Policy

The repository stays minimal on purpose: only `environment/`, `notes/`, and `experiments/`
exist right now (see their own `README.md` for what goes where).

Every "Directory Structure" block shown below (`csapp/`, `linux-programming/`, `linux-kernel/`,
`modules/`, `source-reading/`, `projects/`, ...) is a **reference for what to create when that
phase actually starts** — not a checklist to build in advance. When you begin Phase N, create
only the folders that phase's section describes, named to match.

---

## 🛠 Phase 0: Environment & Toolchain Setup (Month 1)

> **Goal:** Build a reproducible kernel build, run, and debugging environment using QEMU & GDB.

### Directory Structure

```

environment/
├── README.md
├── ubuntu.md
├── kernel-build.md
├── qemu.md
├── gdb.md
└── debugging-tools.md

```

### Labs & Deliverables

#### 🧪 Lab 0-1: Ubuntu Development Environment
- **Learning:** Linux filesystem hierarchy, package management, native compilation toolchains.
- **Tools to Install:** `gcc`, `g++`, `clang`, `cmake`, `make`, `gdb`, `bear`, `graphviz`, `ctags`, `cscope`, `ripgrep`, `fd`.
- **Deliverables:** `environment/setup.sh` (Automated setup script).
- **Verification:**
  - [ ] Compiles C/C++ projects without toolchain errors.
  - [ ] VSCode Remote WSL/SSH operates smoothly.
  - [ ] `clangd` completion and symbol indexing work across headers.

#### 🧪 Lab 0-2: Compile Linux Kernel from Source
- **Workflow:**

```

Download Kernel Source ──> Configure (.config) ──> Compile (make) ──> Boot Kernel Image

```
- **Deliverables:** `environment/kernel-build/{config, build-log.md, screenshots/}`.
- **Verification:** Successfully generate `arch/x86/boot/bzImage`.

#### 🧪 Lab 0-3: QEMU Kernel Booting
- **Goal:** Boot custom kernel images cleanly in virtualized user-space without physical hardware risk.
- **Deliverables:** `environment/qemu/run-qemu.sh`.
- **Verification:**
- [ ] Boot sequence reaches Linux shell / init prompt.
- [ ] Intentionally trigger and analyze kernel panic debug logs.

#### 🧪 Lab 0-4: Remote Kernel Debugging via GDB
- **Tools:** GDB, KGDB, QEMU `-s -S` flags.
- **Debug Target Sequence:** `start_kernel()` ──> `rest_init()` ──> `schedule()`
- **Deliverables:** `environment/gdb/{breakpoint.md, commands.md, screenshots/}`.

---

## 💻 Phase 1: Computer Systems Core (Months 2–3)

> **Goal:** Bridge the gap between low-level system hardware, assembly language, and memory abstractions.

### Directory Structure

```

csapp/
├── README.md
├── chapter01/ ~ chapter12/
└── labs/

```

### Milestone Projects

#### 🚀 Project 1: Binary Analyzer (`mini-readelf`)
- **Key Concepts:** ELF format headers, Symbol tables, Linking & Loading.
- **Usage:** `./mini-readelf <binary_file>`
- **Output:** ELF Header metadata, Section Headers, Symbol Tables.
- **Verification:** Correctly parses custom binaries and standard system utilities.

#### 🚀 Project 2: Memory Simulator (`memory-simulator`)
- **Key Concepts:** Virtual Memory, Page Tables (Multi-level), TLB caching, Page Fault handling.
- **Capabilities:** Simulates address translation, TLB hits/misses, and page replacement strategies.

---

## 🐧 Phase 2: Linux System Programming (Months 4–5)

> **Goal:** Master Linux POSIX APIs, IPC, process lifecycle, and kernel-user boundary interactions.

### Directory Structure

```

linux-programming/
├── process/
├── thread/
├── pipe/
├── socket/
├── signal/
├── mmap/
├── epoll/
└── io/

```

### Milestone Projects

#### 🚀 Project 3: Mini Shell (`mini-shell`)
- **APIs:** `fork()`, `execvp()`, `waitpid()`, `pipe()`, `dup2()`.
- **Feature Set:** Pipeline execution (`ls | grep txt`), I/O redirection (`>`, `<`), background execution (`&`).

#### 🚀 Project 4: Process Status Monitor (`mini-ps`)
- **Concepts:** Interfacing directly with the `/proc` pseudo-filesystem.
- **Output:** Process ID (PID), CPU usage, Resident Memory (RSS), Executable Command Line.

#### 🚀 Project 5: System Call Tracer (`mini-strace`)
- **Concepts:** Kernel process control & instrumentation via `ptrace()`.
- **Capabilities:** Inspect system call numbers, parameters, and return values of target processes in real-time.

---

## 🧠 Phase 3: Linux Kernel Internals (Months 6–8)

> **Goal:** Understand critical kernel subsystems through deep architectural analysis and tracing.

### Subsystem Standard Structure

```

linux-kernel//
├── README.md
├── source-analysis.md
├── experiment.md
└── diagram.png

```

### Core Focus Areas & Experiments

#### 1. Process Scheduler (`/kernel/sched/`)
- **Topics:** Process creation (`copy_process`), CFS / EEVDF scheduling algorithms, Context switching mechanics.
- **Experiment:** Measure process & thread wake-up latencies using `perf` and `ftrace`.

#### 2. Memory Management (`/mm/`)
- **Topics:** Buddy Allocator, Slab/Slub Allocator, Page Fault handling (`handle_mm_fault`), `mmap` zero-copy architecture.
- **Experiment:** Trace page fault frequency and allocation latency during high memory pressure.

#### 3. Virtual File System (`/fs/`)
- **Topics:** VFS abstraction layers (`inode`, `dentry`, `file`), Mount points, Block I/O layer.
- **Experiment:** Trace filesystem system calls through kernel VFS down to block devices.

---

## 🔌 Phase 4: Kernel Modules & Drivers (Month 9)

> **Goal:** Develop fully functional Loadable Kernel Modules (LKMs) and character device drivers.

### Directory Structure

```

modules/
├── hello/
├── procfs/
├── character-driver/
├── workqueue/
└── timer/

```

### Module Implementations

- **LKM 1: Hello Kernel Module**
  - Verify full module lifecycle: `insmod`, `rmmod`, `lsmod`, `dmesg`.
- **LKM 2: ProcFS Kernel Monitor**
  - Expose internal system state via `/proc/kernel_monitor`.
- **LKM 3: Character Device Driver**
  - Implement custom file operations: `open()`, `read()`, `write()`, `ioctl()`, `release()`.

---

## 🔍 Phase 5: Kernel Source Code Analysis (Months 10–11)

> **Goal:** Conduct line-by-line code walk-throughs of mission-critical Linux kernel paths.

### Standard Format per Entry

```

source-reading//<target_function>/
├── README.md
├── call-graph.png
└── walkthrough.md

```

### Entry Section Requirements
1. **Purpose:** Business logic and subsystem goal of the function.
2. **Call Graph:** Visual trace from Syscall ──> Kernel Core Function ──> Architecture / Hardware Driver.
3. **Source Code Annotations:** Detailed analysis of functions like `schedule()`, `copy_process()`, `do_page_fault()`.
4. **Summary:** Architectural takeaways, locking considerations, and concurrency mechanisms.

---

## 🏆 Phase 6: Portfolio Projects & Upstream Patch (Month 12)

> **Goal:** Build complex system portfolio projects and contribute back to the upstream Linux Kernel.


```

projects/
├── mini-top/               # High-performance CLI System Monitor
├── scheduler-visualizer/   # Visual interface for thread scheduling
├── toy-filesystem/         # RAM/Disk-based Custom Filesystem
└── kernel-patch/           # Upstream Kernel Contribution

```

### Portfolio Projects Overview
1. **Linux System Monitor (`mini-top`):** High-efficiency TUI utility monitoring per-core CPU usage, RAM utilization, and process states.
2. **Scheduler Visualizer:** Real-time visual timeline display showing task states, CPU allocations, runqueue latencies, and context switches.
3. **Toy File System (`toy-fs`):** Custom lightweight filesystem implementing custom disk layout with inodes, data blocks, and directory entries.
4. **Upstream Linux Kernel Patch:** Identify bugs or cleanups on the kernel mailing list (LKML), submit, and pass checkpatch verification.

---

## 📏 Engineering & Quality Standards

To maintain standard production quality across all directories, **every Project / Lab** must strictly follow this structure:


```

project-folder/
├── README.md         # Full project documentation
├── Makefile          # Clean compilation target (all, clean, test)
├── src/              # Source code files (.c, .h)
├── test/             # Unit tests or microbenchmarks
├── docs/             # Technical design & specs
└── screenshots/      # Execution captures & performance graphs

```

### Standard `README.md` Template
Every sub-project's README must contain these exact headers:
- `## Goal`
- `## Background`
- `## Design & Architecture`
- `## Implementation Details`
- `## Experiments & Benchmarks`
- `## Results`
- `## Lessons Learned`

---

## 🔀 Git Commit Message Guidelines

Avoid low-quality, ambiguous commit messages (e.g., `update`, `fix`, `test`). Use standardized scopes:

```text
phase0: setup ubuntu environment and toolchain
kernel: build linux kernel v6.x for qemu
qemu: add run script for automated kernel booting
module: implement character driver ioctl interface
scheduler: analyze schedule() call graph and context switch

```

---

## 🎯 Target Portfolio Value

Upon completing this roadmap, this repository will represent:

* **50+** Reproducible kernel & system experiments.
* **10+** Functional C/C++ system utilities and modules.
* Deep architectural source reading notes with call graphs.
* Real-world performance tracing and debugging experience.

