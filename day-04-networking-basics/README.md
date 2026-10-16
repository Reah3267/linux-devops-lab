# day 04 — linux networking basics 🌐🐧

> **Status:** Practiced — networking and HTTP connectivity  
> **Environment:** Ubuntu on WSL2  
> **Focus:** Network diagnostics, HTTP response headers, and troubleshooting

## ✦ today's mission

Understand how to check whether a remote website responds and how to interpret the result — useful for **Linux support, cloud operations, and junior DevOps** interviews.

## ✦ hands-on check: HTTP response headers

I ran this command in my Ubuntu terminal:

```bash
curl -I https://example.com
```

The response began with:

```text
HTTP/2 200
content-type: text/html; charset=utf-8
server: cloudflare
```

**What this confirms:** At that moment, the request reached an HTTP endpoint and received a successful HTTP response. It is **not** proof that every network path, DNS server, or website is healthy.

### reading the output

| Header / status | Meaning |
| --- | --- |
| `HTTP/2 200` | The server returned an HTTP success status over HTTP/2 |
| `content-type: text/html; charset=utf-8` | The response is identified as HTML using UTF-8 |
| `server: cloudflare` | The response identifies Cloudflare as the server software or intermediary |
| `date` | Timestamp provided by the responding server |
| `cf-cache-status: HIT` | Cloudflare reports a cache hit for this response |

## ✦ useful networking commands

These are commands to know and **practice or verify separately**; only the `curl -I` result above is recorded as confirmed output here.

```bash
ping -c 4 example.com     # Test ICMP reachability if permitted
ip addr                   # Inspect local network interfaces
ip route                   # View routing table
getent hosts example.com   # Check name resolution
curl -I https://example.com # Request response headers
```

Some sites block ICMP ping even when HTTPS works. A failed ping by itself does not prove a website is down.

## ✦ troubleshooting flow

1. **Check local addressing:** `ip addr`
2. **Check routes:** `ip route`
3. **Check name resolution:** `getent hosts example.com`
4. **Check HTTP/HTTPS:** `curl -I https://example.com`
5. **Interpret the actual error:** DNS failure, connection timeout, TLS error, or HTTP status code

## ✦ next upgrade

Collect actual output from `ip addr`, `ip route`, and `getent hosts` in a future lab. Later, build a simple **Bash connectivity checker** that logs results and errors.

[← Back to overview](../README.md)
