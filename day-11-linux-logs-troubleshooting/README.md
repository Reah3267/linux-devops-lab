# day 11 — linux logs & troubleshooting 🔎🐧

> **Status:** ✅ Completed practice — 13 Nov 2026  
> **Environment:** Ubuntu on WSL2  
> **Focus:** systemd journals, SSH logs, error triage, oneshot services, and user timers

## ✦ mission

Investigate Linux services through their logs and unit configuration, rather than assuming that an `inactive` status always means something is broken.

## ✦ commands practiced

```bash
journalctl -n 10
sudo journalctl -u ssh --no-pager -n 20
sudo journalctl -p err -b -n 20 --no-pager
systemctl --user status ubuntu-insights-collect.service --no-pager
systemctl --user cat ubuntu-insights-collect.service
systemctl --user status ubuntu-insights-collect.timer --no-pager
journalctl --user -u ubuntu-insights-collect.service -n 20 --no-pager
```

These are diagnostic examples from the practice; journal contents depend on the machine and time.

## ✦ task 1 — read recent journal entries

`journalctl -n 10` showed recent journal records. This is a quick starting point before narrowing the investigation to a service or severity level.

## ✦ task 2 — inspect SSH authentication logs

The SSH journal included activity on **port 22** and a **public-key login**. Checking service-specific logs helps distinguish a successful authentication from a network or service problem.

## ✦ task 3 — filter errors from the current boot

```bash
sudo journalctl -p err -b -n 20 --no-pager
```

The error list included WSL PCI/`dxg` messages, DNS-related entries, and Ubuntu Insights collection/upload failures. A severity-filtered log is a **starting point for diagnosis**, not proof that every listed error is still active.

## ✦ task 4 — inspect the Ubuntu Insights user service

The user service `ubuntu-insights-collect.service` showed:

- Unit loaded and **inactive (dead)** when inspected.
- **TriggeredBy:** `ubuntu-insights-collect.timer`.
- Latest `ExecStart` exited with **0/SUCCESS**.
- Unit configured with `Type=oneshot` and `Restart=no`.
- Sandboxing settings included `ProtectHome=tmpfs` and `BindPaths=%h/.config %h/.cache`.

**Interpretation:** A oneshot service can run successfully and then become inactive. That state alone is not a failure. Earlier collection errors mentioned a missing `/root/.config` path and a namespace-spawn failure; the latest inspected run nevertheless succeeded.

## ✦ task 5 — inspect the timer and service history

```bash
systemctl --user status ubuntu-insights-collect.timer --no-pager
journalctl --user -u ubuntu-insights-collect.service -n 20 --no-pager
```

**Observed timer state:** `active (waiting)`, enabled, and loaded from `/usr/lib/systemd/user/ubuntu-insights-collect.timer`.

The timer was activated on **13 Nov 2026** and displayed a future trigger on **13 Dec 2026**. It schedules the oneshot service; it does not need to remain continuously running.

## ✦ troubleshooting takeaways

- Narrow logs by **unit**, **boot**, and **priority** instead of reading everything at once.
- `systemctl --user` targets the user's service manager; it is different from the system manager.
- For `Type=oneshot`, `inactive (dead)` after `0/SUCCESS` can be normal.
- `active (waiting)` on a timer means it is waiting for a scheduled trigger, not that the service is currently running.
- Compare **older errors** with the **latest execution result** before deciding a service is broken.
- Inspect the unit definition and sandbox restrictions before changing configuration.

## ✦ outcome

Completed the Day 11 log and service troubleshooting exercises. The conclusions above are based on observed statuses and logs, not on an unverified claim that every historical error was permanently fixed.

[← Back to overview](../README.md)
