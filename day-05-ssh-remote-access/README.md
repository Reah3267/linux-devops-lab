# day 05 — ssh & remote access 🔐🐧

> **Status:** ✅ Practice completed  
> **Environment:** Ubuntu on WSL2  
> **Focus:** SSH client/server, local connections, public-key authentication, and safe permissions

## ✦ mission

Learn how Linux administrators connect to another shell securely, check the SSH service, and set up key-based authentication. This lab used **localhost** on the practice machine — not a production remote server.

## ✦ commands from the practice session

### 1. Inspect SSH

```bash
ssh -V
which ssh
sudo systemctl status ssh
systemctl is-active ssh
```

`ssh -V` checks the installed client version; `which ssh` locates the client; `systemctl` reports on the SSH service. A version string is not reproduced here because the exact output was not recorded.

### 2. Manage the service

```bash
sudo systemctl start ssh
sudo systemctl stop ssh
sudo systemctl enable ssh
```

- **start** runs the service now.
- **stop** stops it now.
- **enable** configures it to start automatically when the service manager boots.

These are practice commands, not evidence that all three service states were simultaneously active.

### 3. Connect to localhost

```bash
ssh riya@localhost
whoami
hostname
echo "$SSH_CONNECTION"
exit
```

`whoami` and `hostname` help identify the shell you reached. `SSH_CONNECTION` can show connection details within an SSH session.

### 4. Set up public-key authentication

```bash
ssh-keygen -t ed25519 -C "devops-practice"
chmod 700 ~/.ssh
cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

**Recorded checks:** `~/.ssh` had permission mode **700**, and `authorized_keys` had mode **600**. The public key can be placed in `authorized_keys`; the **private** key must never be copied there or committed to GitHub.

### 5. Test key-only SSH authentication

```bash
ssh -o PreferredAuthentications=publickey -o PasswordAuthentication=no riya@localhost
```

The key-only test was attempted and marked **done** during practice. Its exact terminal response was not retained, so this README does not claim a captured successful login transcript.

## ✦ why the permissions matter

| Path | Mode | Meaning |
| --- | --- | --- |
| `~/.ssh` | `700` | Only the owner can access the directory |
| `~/.ssh/authorized_keys` | `600` | Only the owner can read/write authorized public keys |

SSH can reject authentication if sensitive files or directories have unsafe permissions.

## ✦ troubleshooting notes

- **Connection refused:** Check whether the SSH server is installed, running, and listening on the intended port.
- **Permission denied (publickey):** Check key selection, `authorized_keys`, ownership, permissions, and server configuration.
- **Service command fails in WSL:** Confirm that systemd is enabled in the distribution and inspect the service status.
- **Password prompt appears:** Key-based authentication may not have been selected or accepted; verify before claiming passwordless login.

## ✦ next upgrade

Repeat the key-only SSH test, capture a **redacted** successful login check, and practice reviewing SSH service logs. Never publish private keys, passwords, tokens, or identifying connection details.

[← Back to overview](../README.md)
