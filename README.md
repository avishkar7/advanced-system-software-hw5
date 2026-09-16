# Adaptive Dynamic Tick Interval (xv6)

> Part of the [Advanced System Software](https://github.com/avishkar7/advanced-system-software) portfolio.

## Project

Modify xv6's tick-based kernel so the tick period is **dynamic** — adjusted by
the kernel at runtime based on process behavior — instead of a fixed interval.
The goal is to reduce the total number of ticks while preventing any single
process from monopolizing the CPU, then measure and report the performance
difference against the stock fixed-interval kernel.

## Approach

The scheduler replaces the fixed `1000000`-cycle timer interval with a
`dynamic_tick_rate` that it adjusts each pass from the runnable-process count
and per-slice run time: the interval shrinks under many runnable processes for
responsiveness and grows back when the system is idle. The kernel also tracks
`total_ticks`, `total_context_switches`, and per-state process counts.

These metrics are exposed to userspace through new system calls
(`get_context_switches`, `get_tick_rate`, `get_total_ticks`, and
`get_total_proc_*`). Performance is evaluated against the stock fixed-interval
kernel using instrumented `forktest`, `usertests`, and `ls`, driven by
`xv6-riscv/test-xv6.py`.

- **Workloads:** `forktest`, `usertests`, and `ls`
- **Method:** averaged over 10 runs each
- **Metrics:** execution time, total ticks, context switches

See the project report for the policy description, what system information it
uses, the fixed-vs-dynamic comparison, terminal screenshots, and a discussion
of trade-offs and limitations.

## Layout

| Path | Contents |
|------|----------|
| `xv6-riscv/kernel/` | Kernel with the dynamic tick policy and metric syscalls |
| `xv6-riscv/user/` | User programs, incl. instrumented `forktest`, `usertests`, `ls` |
| `xv6-riscv/test-xv6.py` | QEMU benchmark driver |
| `report/report.pdf` | Project write-up (policy, fixed-vs-dynamic study) |
| `docs/handout.pdf` | Original final-project handout |

## Build & run

```bash
cd xv6-riscv
make qemu        # boot xv6 under QEMU
```

Requires the RISC-V toolchain and QEMU as provided in the course lab environment.
