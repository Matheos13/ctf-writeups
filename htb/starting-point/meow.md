# Meow (Hack The Box, Starting Point)

| | |
|---|---|
| OS | Linux |
| Difficulty | Very Easy (Starting Point, Tier 0) |
| Date | 2026-09-28 |
| Key techniques | Telnet, blank root password |

## Summary

Telnet was open and the root account had no password. Logging in as root over telnet gave full access straight away, and the flag was in root's home directory. My first box.

## Recon

```bash
nmap -sV <target-ip>
```

Port 23 (telnet) is open. Telnet is an old remote login protocol that sends everything, including passwords, in plain text.

## Foothold

Before trying anything fancy, try default and blank credentials. Here `root` with an empty password worked:

```bash
telnet <target-ip>
# login: root
# password: (blank)
```

That drops you straight into a root shell, so there is no privilege escalation step on this box.

## Flag

```bash
ls
# flag.txt  snap
cat flag.txt
```

Flag redacted.

## Lessons learned

- Always try default and blank credentials on any login service first.
- Placeholders like `<ip>` in commands are meant to be replaced, not typed literally (bash throws `syntax error near unexpected token 'newline'`).
- Telnet is plaintext, so anyone on the network can sniff the login. It should be disabled and replaced with SSH.
- **Defender view:** scan for port 23 across the network, disable telnet, and audit for accounts with empty passwords in `/etc/shadow`.
