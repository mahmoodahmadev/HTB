# HackTheBox Lab: Redeemer

---

## Introduction

This lab explores enumeration and exploitation of a Redis server running on a non-standard port. Redis is an in-memory database, often used for caching and fast data retrieval. The objective is to discover the Redis service, connect to it, enumerate its contents, and retrieve the flag.

---

## Recon & Enumeration

### VPN Connection

- Ensure VPN is connected and target IP is accessible.

### Nmap Scan

> **Note:** The Redis server was running on port **6973**. Since nmap by default scans only the first thousand ports, I had to scan ports in batches of a thousand to discover the service.

```bash
nmap -A -p- <Target-IP>
```

- Key findings:
  - Port 6973 open (Redis)
  - Service version detected

---

## Redis Enumeration

### What is Redis?

- Redis (REmote DIctionary Server) is an open-source, NoSQL key-value data store.
- Data is stored in RAM for fast access, but is also periodically written to disk for persistence.
- Commonly used for caching, session management, and message brokering.

### Installing redis-cli

- Install the Redis command-line tools:
  ```bash
  sudo apt install redis-tools
  ```
- View help and options:
  ```bash
  redis-cli --help
  ```

### Connecting to Redis

- Connect to the Redis server on the discovered port:
  ```bash
  redis-cli -h <Target-IP> -p 6973
  ```
- On success, you should see the Redis prompt.

### Enumerating the Database

- Get server info and statistics:
  ```bash
  info
  ```
- Check available databases and their indices (usually index 0).
- Select the database:
  ```bash
  select 0
  ```
- List all keys:
  ```bash
  keys *
  ```
- Retrieve the value for a specific key:
  ```bash
  get <key>
  ```

---

## Flag & Proof

- **Flag:** Retrieved from the value of a key in the Redis database.

---

## Takeaways

- Always scan all ports, especially when default scans miss non-standard services.
- Redis commonly runs on port 6379, but can be configured to use any port.
- Use `redis-cli` for interactive enumeration and data retrieval.
- The `info`, `keys *`, and `get <key>` commands are essential for basic Redis enumeration.
- Non-standard ports are often used to evade default scans—be thorough in your recon.
- Enumerate all keys and review their values for flags or sensitive information.
- Understanding service defaults and common misconfigurations is key in CTFs and real-world engagements.

---

## Extra Notes

- Use `redis-cli -h` for help and command options.
- Data retrieved from Redis is stored in RAM, so persistence may vary.
- Always check for hints or additional data in non-flag keys.

---

## References

- [Redis Documentation](https://redis.io/documentation)
- [HTB Academy: Introduction to Databases](https://academy.hackthebox.com/module/details/13)
