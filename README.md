# CTF Writeups

My writeups for Hack The Box, TryHackMe and CTF challenges, written as I work toward offensive security and red teaming.

Each one covers recon, foothold, privilege escalation, and what I learned, including how a defender would catch or fix the issue.

> Hack The Box writeups are only published for **retired** machines, following HTB's rules. No flags or passwords for active content. Everything here was done on lab machines I was authorized to attack.

## Writeups

| Box / Challenge | Platform | OS | Difficulty | Key techniques |
|---|---|---|---|---|
| [Meow](htb/starting-point/meow.md) | HTB Starting Point | Linux | Very Easy | Telnet, blank root password |
| [Fawn](htb/starting-point/fawn.md) | HTB Starting Point | Unix | Very Easy | FTP anonymous login, nmap scripts |

## Structure

```
htb/            Hack The Box machines (starting-point/, retired/)
thm/            TryHackMe rooms
ctf/            CTF event challenges
TEMPLATE.md     the format every writeup follows
methodology.md  my recon and privesc checklist
```

## Toolkit

nmap · ffuf / gobuster + SecLists · Burp Suite · netexec · linPEAS / winPEAS · GTFOBins
