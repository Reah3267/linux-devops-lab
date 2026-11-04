# day 08 — linux services & systemd ⚙️🐧

> **Status:** ✅ Completed — 04 Nov 2026 (practice lab)  
> **Environment:** Ubuntu on WSL2  
> **Focus:** Linux services, systemd, journal logs, cron, and Nginx

## ✦ the mission

Understand how Linux services start, stop, run in the background, and produce logs. This is a learning lab, not a production deployment.

## ✦ service management

Commands covered in the Day 8 service-management lab:

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

Earlier Day 8 work involved Nginx and a custom webpage. Commands used for Nginx service and configuration troubleshooting:

```bash
sudo systemctl status nginx
sudo nginx -t
curl -I http://localhost
journalctl -u nginx --no-pager -n 20
```

**Observed practice:** An Nginx access-log check returned HTTP 404 entries for a missing favicon and a deliberately nonexistent page. An Nginx error-log entry reported inherited sockets. These observations show log inspection; a 404 for a nonexistent path does not by itself mean Nginx is broken.

## ✦ completion notes

Day 8 practice is complete. Topics covered include service state checks, cron journal review, Nginx configuration checks, HTTP status interpretation, and access/error log inspection.

**Example access-log troubleshooting command:**

```bash
sudo grep '" 404 ' /var/log/nginx/access.log
```

**Example configuration validation:**

```bash
sudo nginx -t
```

The documented log lines were observed during practice. This README does not assert that all service commands produced a particular output unless recorded.

## ✦ next update

Future improvements: add redacted terminal output or a small reusable service-health script. Do not commit secrets, private keys, or machine-specific credentials.

[← Back to overview](../README.md)
