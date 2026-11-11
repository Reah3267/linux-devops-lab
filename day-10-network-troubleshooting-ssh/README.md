# Day 10 — Network Troubleshooting & SSH 🐧

> **Status:** Completed hands-on in Ubuntu WSL2 · **Focus:** connectivity, DNS, SSH and socket activation

## What I practiced

- Tested external IP connectivity with `ping -c 4 8.8.8.8`.
- Resolved `google.com` using `getent ahostsv4 google.com`.
- Checked the OpenSSH client version with `ssh -V`.
- Inspected `ssh.service` and verified TCP port 22 listeners.
- Identified **systemd socket activation**: `ssh.service` was inactive while `systemd` owned the port 22 listening sockets.
- Connected to my own WSL2 Ubuntu instance using `ssh riya@127.0.0.1` and an existing passphrase-protected ED25519 key.
- Verified the SSH session using `echo "$SSH_CONNECTION"`, exited with `exit`, and confirmed the variable was blank in the original shell.
- Answered the troubleshooting scenario: when SSH is refused and port 22 is not listening, investigate the SSH service **and** socket first.

## Commands and observed results

### 1. Network connectivity

```bash
ping -c 4 8.8.8.8
```

Observed: **4 sent, 4 received, 0% packet loss**; average round-trip time **25.027 ms**. This verifies IP reachability for that test, not DNS or all application connectivity.

### 2. DNS resolution

```bash
getent ahostsv4 google.com
```

Observed: multiple IPv4 records, including `142.251.43.142` and `142.251.221.238`. The `STREAM`, `DGRAM` and `RAW` entries describe socket types in the resolver output; they do **not** mean connections were opened.

**Troubleshooting takeaway:** If pinging a public IP works but resolving a hostname fails, investigate DNS first.

### 3. SSH client and server

```bash
ssh -V
sudo systemctl status ssh
sudo ss -ltnp 'sport = :22'
```

Observed:
- OpenSSH client version: `OpenSSH_10.2p1` (Ubuntu package).
- `ssh.service`: `inactive (dead)`, with `TriggeredBy: ssh.socket`.
- Port `22`: listening on `0.0.0.0:22` and `[::]:22`, owned by `systemd` (PID 1).

**Why this matters:** An inactive `ssh.service` does not necessarily mean SSH is unavailable. With systemd socket activation, systemd can listen on the SSH port and activate the service for incoming connections.

### 4. Local SSH connection and verification

```bash
ssh riya@127.0.0.1
echo "$SSH_CONNECTION"
exit
echo "$SSH_CONNECTION"
```

Observed:
- First localhost connection prompted for host-key trust; the host key was added to `~/.ssh/known_hosts`.
- The SSH client requested the **passphrase for an existing private key**, not the Ubuntu account password.
- Ubuntu login succeeded.
- Inside SSH, `SSH_CONNECTION` returned:

```text
127.0.0.1 40446 127.0.0.1 22
```

These are `client_IP client_port server_IP server_port`. Port `40446` was an ephemeral client port; `22` was the server port.
- After `exit`, `echo "$SSH_CONNECTION"` produced no value in the original terminal.

## Troubleshooting playbook

**Scenario:** SSH says “connection refused” and `ss` shows no listener on port 22.

Start by inspecting the service and socket, without immediately reinstalling or restarting the machine:

```bash
sudo systemctl status ssh
sudo systemctl status ssh.socket
sudo ss -ltnp 'sport = :22'
```

Further checks depend on the results: service logs, SSH configuration, actual listening port, and network/firewall rules.

## Key lessons

- IP connectivity and DNS resolution are different checks.
- A listening port can be owned by systemd when socket activation is enabled.
- SSH **host keys** verify the server's identity; a user's **private key** authenticates the client. Do not publish private keys or passphrases.
- `SSH_CONNECTION` is set within an SSH login session, not automatically in the original local shell.
- Diagnose first, then change configuration.

---

*Documented from my Day 10 Ubuntu WSL2 practice. This was a localhost SSH exercise, not a deployment to a remote production server.*
