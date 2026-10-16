# day 01 — terminal basics 🐧

> status: **practiced** · environment: **Ubuntu on WSL2**

## mission

Get comfortable moving around the Linux filesystem and creating, reading, copying, renaming, and deleting practice files.

## commands i practiced

| Command | What it does |
| --- | --- |
| `pwd` | Print current working directory |
| `whoami` | Show current username |
| `ls -la` | List files, including hidden ones, with details |
| `cd directory` | Change directory |
| `mkdir directory` | Create a directory |
| `touch file.txt` | Create an empty file (or update its timestamp) |
| `echo "hello" > file.txt` | Write text, replacing existing file content |
| `cat file.txt` | Read file content |
| `cp a.txt b.txt` | Copy a file |
| `mv a.txt b.txt` | Rename or move a file |
| `rm file.txt` | Delete a file |
| `rmdir empty-folder` | Remove an empty directory |

## hands-on mini lab

I practiced under `~/devops-practice/linux-challenge/`, creating and copying files and writing a short note about becoming DevOps-ready.

Try a **safe, reproducible version** in your own Ubuntu terminal:

```bash
mkdir -p ~/devops-practice/day1-demo
cd ~/devops-practice/day1-demo
pwd
touch linux.txt
echo "I am becoming devops ready" > linux.txt
cp linux.txt backup.txt
ls -lh
cat backup.txt
```

**Expected check:** both `linux.txt` and `backup.txt` should contain the same line.

## next

Move on to Linux permissions and processes in [Day 02](../day-02-permissions-processes/README.md).
