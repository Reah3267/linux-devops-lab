# day 07 — cron job automation ⏰🐧

> **Status:** ✅ Completed — 23–24 Oct 2026  
> **Environment:** Ubuntu on WSL2  
> **Focus:** Cron scheduling, output redirection, monitoring automation, and troubleshooting

## ✦ mission

Schedule the Day 6 server-monitoring script to run automatically, and create a separate heartbeat log.

## ✦ scheduled jobs

These entries were configured in the user's crontab:

```cron
*/10 * * * * /home/riya/devops-practice/linux-challenge/server-monitor.sh >> /home/riya/devops-practice/linux-challenge/server-report.txt 2>&1
*/15 * * * * date >> /home/riya/devops-practice/linux-challenge/d7-cron/heartbeat.log
```

| Schedule | Action |
| --- | --- |
| `*/10 * * * *` | Run the server-monitoring script every 10 minutes |
| `*/15 * * * *` | Append the date and time to a heartbeat log every 15 minutes |

### useful checks

```bash
crontab -l
systemctl is-active cron
journalctl -u cron --no-pager -n 20
tail -n 10 ~/devops-practice/linux-challenge/server-report.txt
tail -n 10 ~/devops-practice/linux-challenge/d7-cron/heartbeat.log
```

## ✦ debugging notes

An early crontab entry contained an invalid double output-redirection sequence (`>> >>`). After correcting the syntax, the monitoring report received a fresh entry during the 23 Oct practice session.

**Verified scheduler evidence:** On **24 Oct at 06:00:01**, cron journal entries showed both the heartbeat command and monitoring script being launched.

### what the operators mean

- `>>` appends output to a file.
- `2>&1` sends standard error to the same destination as standard output.
- A cron journal entry verifies **invocation**; it does not automatically prove that every line of a script succeeded. The updated report provided an additional check for the monitoring job.

## ✦ outcome

The Day 7 scheduled automation exercise was completed. The cron expressions and paths above are from the practice setup; no credentials or secrets are included.

[← Back to overview](../README.md)
