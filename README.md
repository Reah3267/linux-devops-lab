<div align="center">

# 🐧 linux-devops-lab

### learning linux one command (and one error) at a time ⚡

`build → break → debug → repeat`

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![Learning](https://img.shields.io/badge/Status-learning_in_public-8B5CF6?style=for-the-badge)

**A hands-on learning log for Junior DevOps / Linux / IT Support roles.**

</div>

---

## ✦ the plot

I'm learning Linux on **Ubuntu via WSL2 (Windows 11)**, practicing commands in the terminal, and documenting the *why*, not just the output.

This is a **learning portfolio**, not a claim of production DevOps experience. Exercises and explanations are added as I complete them.

## ✦ progress tracker

| Lab | Focus | Status |
| --- | --- | --- |
| [Day 01](day-01-linux-basics/README.md) | Files, folders & terminal navigation | ✅ Practiced |
| [Day 02](day-02-permissions-processes/README.md) | Permissions, process management & signals | ✅ Practiced |
| [Day 03](day-03-server-health-check/README.md) | System monitoring & manual health report | ✅ Completed (manual lab) |
| [Day 04](day-04-networking-basics/README.md) | Networking basics & HTTP connectivity | ✅ Practiced (curl verified) |
| Future labs | Bash, logs, services, automation | 🗓️ Planned |

## ✦ skills i'm building

- **Linux CLI:** `pwd`, `ls`, `cd`, `mkdir`, `touch`, `cat`, `cp`, `mv`, `rm`
- **Permissions:** `chmod`, octal modes, user/group/other permissions
- **Processes:** `ps`, `grep`, `kill`, background jobs, process IDs
- **Monitoring:** `uptime`, `free -h`, `df -h`, `top`, `ps -p`
- **Networking:** `curl -I` (verified HTTP response); exploring `ping`, `ip`, and DNS checks
- **Workflow:** running commands, checking results, correcting mistakes, keeping notes

## ✦ lab notes

Each lab contains commands I've practiced, what they do, and small interview-style explanations. Command snippets are **examples to reproduce locally**, not copies of terminal output or proof of a completed automated test suite.

> learning goal: understand what a command changes, how to verify it, and what to try when something goes wrong.

## ✦ setup

- Windows 11 + WSL2
- Ubuntu terminal
- Git and GitHub for version control

To try the examples, open an Ubuntu terminal and work inside a practice directory:

```bash
mkdir -p ~/devops-practice
cd ~/devops-practice
```

**Safety note:** practice `rm`, `chmod`, and `kill` only on your own test files/processes. Don't paste commands blindly into production systems.

---

<div align="center">

*small steps. real terminal time. 🚀*

</div>
