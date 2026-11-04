# day 09 — linux networking & troubleshooting 🌐🐧

> **Status:** ✅ Practiced — 04 Nov 2026  
> **Environment:** Ubuntu on WSL2  
> **Focus:** IP addressing, routes, connectivity, DNS, listening ports, Nginx

## ✦ mission

Trace a connection from the local Linux network interface through the default gateway to a public IP, verify DNS resolution, and inspect whether a web server is listening on its expected port.

## ✦ observed network details

| Item | Observed value |
| --- | --- |
| Local WSL IP address | `172.23.150.25` |
| Default gateway | `172.23.144.1` |
| Resolved IPv4 address for `google.com` | `142.251.222.174` |

These addresses were recorded during the practice session and may change when WSL or network conditions change.

## ✦ connectivity checks

### gateway

```bash
ping -c 4 172.23.144.1
```

**Observed:** 4 packets transmitted, 4 received, **0% packet loss**, average round-trip time **1.629 ms**.

### public IP

```bash
ping -c 4 8.8.8.8
```

**Observed:** 4 packets transmitted, 4 received, **0% packet loss**, average round-trip time **1988.395 ms**.

The public-IP check succeeded but had **high latency** during this sample. A single four-packet test does not establish long-term network performance.

## ✦ DNS resolution

```bash
getent ahostsv4 google.com
```

**Observed IPv4 result:** `142.251.222.174`.

This confirmed that name resolution returned an IPv4 address at the time of the test. The address may differ in future checks.

## ✦ inspecting listening ports

```bash
sudo ss -ltnp 'sport = :80'
```

**Observed:** Nginx was listening on:

- `0.0.0.0:80` — all IPv4 interfaces
- `[::]:80` — IPv6 interfaces

The output listed multiple Nginx process IDs. Listening on a port confirms a local socket is bound; it does **not** by itself prove the website returns a healthy HTTP response.

## ✦ troubleshooting sequence

The commands below are a reusable diagnostic workflow. The specific outputs documented above are the results verified in this session.

```bash
ip -4 addr
ip route
ping -c 4 172.23.144.1
ping -c 4 8.8.8.8
getent ahostsv4 google.com
sudo ss -ltnp 'sport = :80'
curl -I http://localhost
```

**How to interpret the checks:**

1. **IP / route:** Check that the interface has an address and a route to the gateway.
2. **Gateway ping:** Check reachability of the local next hop.
3. **Public-IP ping:** Test external IP reachability, noting latency and packet loss.
4. **DNS:** Check whether a hostname resolves.
5. **Port 80:** Check whether Nginx is bound to the expected port.
6. **HTTP:** Test the application layer separately; a listening socket alone is insufficient.

## ✦ what i learned

- Network troubleshooting is more effective when each layer is checked separately.
- Successful DNS resolution and successful ICMP ping answer different questions.
- High latency can occur even when packet loss is zero.
- `ss` helps identify services and ports before debugging the application itself.
- WSL network addresses may be ephemeral.

[← Back to overview](../README.md)
