# Methodology

The checklist I run on every box. Updated as I learn.

## 1. Recon

```bash
nmap -p- --min-rate 5000 -oN nmap/allports $IP
nmap -sC -sV -p <ports> -oN nmap/targeted $IP
nmap -sU --top-ports 50 $IP
```

## 2. Web (80 / 443 / 8080)

- [ ] Add the hostname to `/etc/hosts` and look for vhosts
- [ ] Page source, `robots.txt`, JS files, cookies
- [ ] Tech stack and versions, then searchsploit / CVEs
- [ ] Login forms: default creds, SQL injection, weak password reset
- [ ] File upload, LFI / path traversal, SSTI, command injection

```bash
ffuf -u http://$HOST/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt
ffuf -u http://$HOST -H "Host: FUZZ.$HOST" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -fs <size>
```

## 3. Other services

```bash
smbclient -L //$IP -N
netexec smb $IP -u '' -p '' --shares
```

- [ ] FTP anonymous login
- [ ] SSH version, reused credentials

## 4. Foothold

- [ ] Stabilise the shell: `python3 -c 'import pty;pty.spawn("/bin/bash")'`, then `stty raw -echo; fg`

## 5. Linux privesc

```bash
sudo -l
find / -perm -4000 -type f 2>/dev/null
getcap -r / 2>/dev/null
cat /etc/crontab; ls -la /etc/cron*
ss -tlnp
```

- [ ] Config files and shell history for credentials
- [ ] Check every interesting binary on GTFOBins
- [ ] Run linPEAS if stuck

## 6. Windows privesc

```powershell
whoami /priv
whoami /groups
```

- [ ] SeImpersonatePrivilege: potato attacks
- [ ] Stored credentials, unquoted service paths, AlwaysInstallElevated
- [ ] Run winPEAS if stuck

## 7. While working

- Save every key command and screenshot as I go
- Write the writeup the same day
