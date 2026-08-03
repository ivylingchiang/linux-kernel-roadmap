# Experiments

This is where hands-on experiments live, regardless of which roadmap phase they belong to
(booting, tracing, benchmarking, kernel module tests, etc.).

## Naming Convention

Create a subfolder **only when you start that experiment** — don't pre-create topic folders.

```text
experiments/
└── <topic>/                # e.g. scheduler, mmap, page-fault, boot
    ├── README.md            # Goal, method, how to reproduce
    ├── setup.sh / Makefile  # Whatever is needed to run it (optional)
    └── results/             # Logs, traces, screenshots, benchmark output
```

`<topic>` should match whatever subsystem or concept you're actively experimenting with
(e.g. `experiments/scheduler/`, `experiments/mmap/`). Reference `ROADMAP.md` for the
subsystems each phase focuses on.

## Suggested `README.md` per experiment

- **Goal** — what question this experiment answers
- **Method** — tools used (`perf`, `ftrace`, `strace`, QEMU, GDB, ...) and steps to reproduce
- **Results** — what was observed
- **Takeaways** — what this taught you
