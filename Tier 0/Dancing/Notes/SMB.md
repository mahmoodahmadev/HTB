## SMB (Server Message Block) - Detailed Notes

### What is SMB?

SMB (Server Message Block) is a network protocol for sharing files, printers, and other resources between computers on a network. It originated with IBM and was later adopted and extended by Microsoft. SMB is most commonly used in Windows environments but is also supported on Linux and macOS via Samba.

### SMB Protocol Overview

- **Purpose:** File and printer sharing, network browsing, inter-process communication.
- **Ports:**
  - TCP 445 (Direct SMB over TCP)
  - TCP 139 (NetBIOS over TCP/IP, legacy)
- **Versions:**
  - SMB1: Legacy, insecure, deprecated.
  - SMB2: Improved performance and security.
  - SMB3: Enhanced security (encryption, improved authentication).

### How SMB Works

- **Client-Server Model:** Clients connect to SMB servers to access shared resources.
- **Shares:** Resources (folders, printers) are shared and accessed via UNC paths (e.g., `\\server\share`).
- **Authentication:** Supports anonymous and authenticated access (local/domain users).

### Common SMB Operations

- List available shares on a server
- Connect to a share
- Upload/download files
- Enumerate users and permissions
- Mount shares locally (Linux/Unix)

### SMB on Linux (Samba)

- **Samba:** Open-source implementation of SMB/CIFS for Unix/Linux.
- **Tools:**
  - `smbclient`: Command-line SMB client.
  - `mount.cifs`: Mount SMB shares as local directories.
  - `smbmap`: Enumerate shares and permissions.
  - `enum4linux`: SMB enumeration tool.

### Security Considerations

- **SMB1 is insecure:** Vulnerable to attacks (e.g., EternalBlue). Avoid using SMB1.
- **Use SMB2/3:** Improved security and performance.
- **Restrict access:** Limit share permissions, use strong passwords.
- **Keep software updated:** Patch SMB servers and clients regularly.

### SMB Path Syntax: Backslashes vs. Forward Slashes

- **Windows/SMB convention:** Uses backslashes (`\`) for UNC paths.
  - Example: `\\server\share\folder\file.txt`
- **Linux/Unix convention:** Uses forward slashes (`/`) for file paths.
  - Example: `/mnt/share/folder/file.txt`
- **SMB tools on Linux:** Accept both, but UNC paths often require double backslashes or forward slashes depending on the tool.
  - Example: `smbclient //server/share` or `smbclient \\server\share`
- **Escaping:** In Linux shells, backslashes may need escaping (e.g., `\\server\\share`).

## smbclient Interactive Command Cheatsheet

| Command               | Description                                                    |
| --------------------- | -------------------------------------------------------------- |
| `?` / `help`          | Show help for commands.                                        |
| `allinfo`             | Display all information about a file (attributes, times, etc). |
| `altname`             | Show the alternate (short) name for a file.                    |
| `archive`             | Set or clear the archive attribute on a file.                  |
| `backup`              | Copy files using backup semantics.                             |
| `blocksize`           | Set the block size for file transfers.                         |
| `cancel`              | Cancel a print job.                                            |
| `case_sensitive`      | Toggle case sensitivity for file operations.                   |
| `cd`                  | Change the current directory on the remote share.              |
| `chmod`               | Change permissions of a file (if supported).                   |
| `chown`               | Change owner of a file (if supported).                         |
| `close`               | Close a file.                                                  |
| `del` / `rm`          | Delete a file.                                                 |
| `deltree`             | Delete a directory and all its contents recursively.           |
| `dir` / `ls` / `l`    | List files and directories in the current remote directory.    |
| `du`                  | Show disk usage of files/directories.                          |
| `echo`                | Print text to the console.                                     |
| `exit` / `quit` / `q` | Exit the smbclient shell.                                      |
| `get`                 | Download a file from the remote share to your local machine.   |
| `getfacl`             | Get file access control list (ACL) information.                |
| `geteas`              | Get extended attributes of a file.                             |
| `hardlink`            | Create a hard link to a file.                                  |
| `history`             | Show command history.                                          |
| `iosize`              | Set the I/O size for file transfers.                           |
| `lcd`                 | Change the local directory on your machine.                    |
| `link`                | Create a symbolic link to a file.                              |
| `lock`                | Lock a file.                                                   |
| `lowercase`           | Toggle lowercase mode for file names.                          |
| `mask`                | Set file mask for file operations.                             |
| `md` / `mkdir`        | Create a directory on the remote share.                        |
| `mkfifo`              | Create a FIFO special file.                                    |
| `more`                | Display file contents page by page.                            |
| `mput`                | Upload multiple files from local to remote share.              |
| `newer`               | Only operate on files newer than a specified date.             |
| `notify`              | Set up notifications for file changes.                         |
| `open`                | Open a file.                                                   |
| `posix`               | Toggle POSIX semantics.                                        |
| `posix_encrypt`       | Toggle POSIX encryption.                                       |
| `posix_open`          | Open a file with POSIX semantics.                              |
| `posix_mkdir`         | Create a directory with POSIX semantics.                       |
| `posix_rmdir`         | Remove a directory with POSIX semantics.                       |
| `posix_unlink`        | Unlink (delete) a file with POSIX semantics.                   |
| `posix_whoami`        | Show current POSIX user info.                                  |
| `print`               | Print a file to a remote printer.                              |
| `prompt`              | Toggle prompting for multiple file operations.                 |
| `put`                 | Upload a file from local to remote share.                      |
| `pwd`                 | Show current directory on the remote share.                    |
| `queue`               | Show print queue.                                              |
| `readlink`            | Read the target of a symbolic link.                            |
| `rd` / `rmdir`        | Remove a directory.                                            |
| `recurse`             | Toggle recursion for directory operations.                     |
| `reget`               | Resume a failed download.                                      |
| `rename`              | Rename a file or directory.                                    |
| `reput`               | Resume a failed upload.                                        |
| `showacls`            | Show access control lists for files.                           |
| `setea`               | Set extended attributes for a file.                            |
| `setmode`             | Set file mode bits.                                            |
| `scopy`               | Copy files with server-side copy.                              |
| `stat`                | Show file status information.                                  |
| `symlink`             | Create a symbolic link.                                        |
| `tar`                 | Archive files to/from a tar file.                              |
| `tarmode`             | Set tar operation mode.                                        |
| `timeout`             | Set timeout for operations.                                    |
| `translate`           | Translate file names.                                          |
| `unlock`              | Unlock a file.                                                 |
| `volume`              | Show volume information.                                       |
| `vuid`                | Show virtual user ID.                                          |
| `wdel`                | Delete files matching a wildcard pattern.                      |
| `logon`               | Log on to a server.                                            |
| `listconnect`         | List current connections.                                      |
| `showconnect`         | Show details of current connection.                            |
| `tcon`                | Connect to a tree (share).                                     |
| `tdis`                | Disconnect from a tree (share).                                |
| `tid`                 | Show tree ID.                                                  |
| `utimes`              | Change file access/modification times.                         |
| `logoff`              | Log off from the server.                                       |
