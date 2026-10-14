# day 03 — server health check 🩺🐧

> **Status:** Monitoring commands practiced; mini-project in progress  
> **Environment:** Ubuntu on WSL2  
> **Focus:** CPU, RAM, disk space, uptime, and process inspection

## ✦ today's mission

Learn to answer the first questions in Linux troubleshooting:

- Is the system running normally?
- How much memory is available?
- Is a filesystem running out of space?
- Which processes are active?

## ✦ commands practiced

| Command | Why it matters |
| --- | --- |
| `uptime` | Shows how long the system has been up and its load averages |
| `free -h` | Shows memory and swap usage in readable units |
| `df -h` | Shows filesystem space usage |
| `df -h /` | Checks the filesystem containing `/` |
| `top` | Interactive view of CPU, memory, and running processes |
| `ps -p PID` | Checks whether a specific process ID is currently listed |
| `ls -l` | Verifies file metadata and permissions |
| `cp` | Copies a report to a backup file |

**Troubleshooting lesson:** `df -h /` needs a space before `/`. A mistyped option such as `df -0h` does not mean the same thing as `df -h`.

## ✦ hands-on mini-project: server health report

**Local practice directory:**

```text
~/devops-practice/linux-challenge/day3-/server-health-check/
├── health-report.txt
└── health-report-backup.txt
```

The report was created using shell redirection:

```bash
echo "Linux Server Health Report" > health-report.txt
echo "CPU usage was low" >> health-report.txt
echo "RAM availability was high" >> health-report.txt
echo "Root filesystem usage was 1 percent" >> health-report.txt
```

Then backed up and checked:

```bash
cp health-report.txt health-report-backup.txt
ls -l
cat health-report.txt
```

### Observed output

```text
-rw-rw-r-- 1 riya riya 107 Oct 14 07:14 health-report-backup.txt
-rw------- 1 riya riya 107 Oct 14 07:14 health-report.txt

Linux Server Health Report
CPU usage was low
RAM availability was high
Root filesystem usage was 1 percent
```

**Important:** These are observations recorded during practice, not a live monitoring dashboard or an automated collection script. The backup had different permissions from the original report at the time of inspection.

### Process check

The following command was run:

```bash
ps -p 1240
```

It displayed the header but no process row. This means that PID **1240 was not listed at that moment**; the output alone does not prove why it was absent.

Earlier process practice also included running a temporary `sleep 120` process, inspecting its PID, and terminating it.

## ✦ interview checkpoint

**Q: What's the difference between `free -h` and `df -h`?**

`free -h` reports memory/swap; `df -h` reports filesystem space.

**Q: Why check `uptime`?**

It shows system uptime and load averages, useful context when diagnosing performance.

**Q: Does `ps -p PID` showing no row mean `kill` worked?**

Not necessarily. The process might have already exited or the PID might be incorrect. Verify the sequence before making that claim.

## ✦ next upgrade

Convert these manual observations into a **Bash health-check script** that collects real command output, saves a timestamped report, and checks its own results. This is **planned**, not yet completed.

[← Back to overview](../README.md)
