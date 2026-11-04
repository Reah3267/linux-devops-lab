# day 06 — bash scripting & automation 🐚⚡

> **Status:** ✅ Completed — 17 Oct 2026  
> **Environment:** Ubuntu on WSL2  
> **Focus:** Bash scripting, system monitoring, variables, conditionals, and debugging

## ✦ mission

Turn individual Linux monitoring commands into a reusable Bash script.

## ✦ project: `server-monitor.sh`

**Practice location:** `~/devops-practice/linux-challenge/server-monitor.sh`

The completed practice script ran commands to inspect:

| Command | Purpose |
| --- | --- |
| `whoami` | Identify the current user |
| `hostname` | Identify the machine |
| `date` | Record the time of the check |
| `uptime` | View uptime and load averages |
| `df -h /` | Inspect the root filesystem's disk usage |
| `free -h` | Inspect memory and swap usage |

### reproducible monitoring example

This example demonstrates the same monitoring commands. It is **not claimed to be a byte-for-byte copy** of the original local script.

```bash
#!/usr/bin/env bash

echo "=== Server Monitor ==="
echo "User: $(whoami)"
echo "Host: $(hostname)"
echo "Checked at: $(date)"

echo
echo "=== Uptime ==="
uptime

echo
echo "=== Root Disk Usage ==="
df -h /

echo
echo "=== Memory ==="
free -h
```

To save and run a script like this:

```bash
chmod +x server-monitor.sh
./server-monitor.sh
```

## ✦ debugging notes

During the exercise, the script initially had **variable and `if` statement syntax errors**. Those were corrected and the monitoring script was run successfully.

Lessons from the debugging process:

- Use `$(command)` to capture a command's output.
- Quote variable expansions when appropriate.
- Bash `if` statements require correct syntax and a closing `fi`.
- Test changes by running the script and inspecting the output.

## ✦ outcome

The Day 6 exercise was completed and assessed during practice. The original script and full terminal transcript are not committed here; the example above is a reproducible learning reference.

[← Back to overview](../README.md)
