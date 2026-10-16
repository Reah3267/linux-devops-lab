# day 02 — permissions & processes 🔐

> status: **practiced** · environment: **Ubuntu on WSL2**

## mission

Understand who can read/write/execute files, how octal permissions work, and how to inspect or stop processes.

## permissions: the basics

Linux file permissions are organized as **user / group / others**:

- `r = 4` — read
- `w = 2` — write
- `x = 1` — execute

| Mode | Meaning |
| --- | --- |
| `600` | Owner can read and write; no access for group/others |
| `755` | Owner can read/write/execute; group/others can read/execute |
| `530` | Owner read/execute; group write/execute; others no access |

## commands i practiced

```bash
ls -l
chmod 600 devops-secret.txt
chmod 530 permission-test.txt
ps
ps -p 1234
```

The process ID `1234` is an **example**. Use the actual PID shown on your machine.

## hands-on mini lab

I practiced with `permission-test.txt`, `devops-secret.txt`, and background `sleep` processes. Here is a reproducible version:

```bash
mkdir -p ~/devops-practice/day2-demo
cd ~/devops-practice/day2-demo

touch permission-test.txt devops-secret.txt
chmod 530 permission-test.txt
chmod 600 devops-secret.txt
ls -l

sleep 300 &
pid=$!
echo "Background PID: $pid"
ps -p "$pid"
kill "$pid"
```

**Expected check:** `ls -l` should show the permission modes; `ps -p "$pid"` should show the running sleep process before it is stopped.

## next

Day 03 is **not started yet**. This repository will grow as I finish more practical Linux work.

[← Back to overview](../README.md)
