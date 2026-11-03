# day 08 — linux services & systemd ⚙️🐧

> **Status:** 🔄 In progress — restarted from the beginning on 03 Nov 2026  
> **Environment:** Ubuntu on WSL2  
> **Focus:** Linux services, systemd, journal logs, cron, and Nginx

## ✦ the mission

Understand how Linux services start, stop, run in the background, and produce logs. This is a learning lab, not a production deployment.

## ✦ service management

Useful commands for the restarted Day 8 lessons:

```bash
systemctl status cron
systemctl is-active cron
systemctl is-enabled cron
sudo systemctl start cron
sudo systemctl restart cron
journalctl -u cron --no-pager -n 15
```

- `status`: inspect service state and recent details
- `is-active`: check whether a service is currently active
- `is-enabled`: check whether it is configured to start automatically
- `start` / `restart`: manage a service
- `journalctl -u`: inspect logs for a specific unit

## ✦ previously verified: scheduled monitoring

During earlier practice, `cron` was checked and reported **active** and **enabled**.

The cron journal showed scheduled jobs running at **06:00:01**, including commands equivalent to:

```bash
date >> /path/to/heartbeat.log
/path/to/server-monitor.sh >> /path/to/server-report.txt 2>&1
```

The actual practice paths are omitted here because they have not been reverified for this restart.

### what the redirection means

- `>>` appends output to an existing file or creates the file if needed.
- `2>&1` sends standard error to the same destination as standard output.
- A cron log entry confirms the scheduler invoked the command; it does **not**, by itself, prove that every part of the script succeeded.

## ✦ Nginx service exploration

Earlier Day 8 work involved Nginx and a custom webpage. The restarted lesson can revisit these checks:

```bash
sudo systemctl status nginx
sudo nginx -t
curl -I http://localhost
journalctl -u nginx --no-pager -n 20
```

These commands are a **practice checklist**, not newly verified outputs. Existing Nginx work does not need to be deleted to restart the lesson.

## ✦ restart checklist

- [ ] Review what a Linux service and systemd unit are
- [ ] Inspect `systemctl status`, `is-active`, and `is-enabled`
- [ ] Practice starting, stopping, and restarting a test service safely
- [ ] Read service logs with `journalctl`
- [ ] Revisit Nginx and test its configuration
- [ ] Record verified outputs and troubleshooting notes

## ✦ next update

As each restarted Day 8 lesson is completed, replace checklist items with actual results. Do not commit secrets, private keys, or machine-specific credentials.

[← Back to overview](../README.md)
