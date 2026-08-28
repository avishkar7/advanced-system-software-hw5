# Adaptive Dynamic Tick Interval (xv6)

> Part of the [Advanced System Software](https://github.com/avishkar7/advanced-system-software) portfolio.

> **Status — work in progress.** This repository currently holds the xv6 base
> tree. I will add the modified kernel implementing the dynamic tick policy, the
> `runtime` test program, and the project report.

## Project

Modify xv6's tick-based kernel so the tick period is **dynamic** — adjusted by
the kernel at runtime based on process behavior — instead of a fixed interval.
The goal is to reduce the total number of ticks while preventing any single
process from monopolizing the CPU, then measure and report the performance
difference against the stock fixed-interval kernel.

## Approach

The kernel adjusts the tick interval adaptively in response to the operation of
processes in the system. Performance is evaluated with the provided `runtime`
user program against the original fixed-interval kernel.

- **Workloads:** `forktest`, `usertests`, and `ls`
- **Method:** averaged over 10 runs each
- **Metrics:** execution time, total ticks, context switches

See the project report for the policy description, what system information it
uses, the fixed-vs-dynamic comparison, terminal screenshots, and a discussion
of trade-offs and limitations.

## Layout

| Path | Contents |
|------|----------|
| `xv6-riscv/` | The xv6 kernel with the dynamic tick-interval implementation |
| `docs/handout.pdf` | Original final-project handout |

## Build & run

```bash
cd xv6-riscv
make qemu        # boot xv6 under QEMU
```

Requires the RISC-V toolchain and QEMU as provided in the course lab environment.
