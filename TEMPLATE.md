# <Box name> (<Platform>)

| | |
|---|---|
| OS | Linux / Windows |
| Difficulty | Easy / Medium / Hard |
| Date | YYYY-MM-DD |
| Key techniques | e.g. SQL injection, SUID abuse |

## Summary

2 or 3 sentences: how I got in and how I got root.

## Recon

```bash
nmap -p- --min-rate 5000 -oN nmap/allports <ip>
nmap -sC -sV -p <ports> -oN nmap/targeted <ip>
```

Open ports and what stood out.

## Enumeration

What I checked, what worked, and dead ends worth noting.

## Foothold

The vulnerability, how I exploited it, and proof (`id`, `whoami`).

## Privilege escalation

How I went from user to root / SYSTEM.

## Lessons learned

- What was new to me
- What I'd check faster next time
- How a defender would detect or fix it
