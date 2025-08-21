# Redis: A Complete Guide

---

## Introduction

Redis (REmote DIctionary Server) is an open-source, in-memory key-value data store. It is widely used for caching, session management, real-time analytics, and as a message broker. Redis is known for its speed, simplicity, and versatility.

---

## Key Features

- **In-memory storage:** Data is stored in RAM for ultra-fast access.
- **Persistence:** Supports snapshotting and append-only file (AOF) for durability.
- **Data structures:** Strings, lists, sets, sorted sets, hashes, bitmaps, hyperloglogs, streams, and geospatial indexes.
- **Pub/Sub:** Built-in publish/subscribe messaging system.
- **Replication:** Master-slave replication for high availability.
- **Clustering:** Horizontal scaling via Redis Cluster.
- **Transactions:** Supports atomic operations using MULTI/EXEC.
- **Scripting:** Lua scripting for advanced logic.

---

## Installation

### On Linux (Debian/Ubuntu)

```bash
sudo apt update
sudo apt install redis-server redis-tools
```

### On Other Platforms

- Windows: Use WSL or Docker
- macOS: `brew install redis`
- Docker: `docker run --name redis -p 6379:6379 -d redis`

---

## Basic Configuration

- Default config file: `/etc/redis/redis.conf`
- Start Redis server: `sudo systemctl start redis-server`
- Check status: `sudo systemctl status redis-server`
- Stop server: `sudo systemctl stop redis-server`

---

## Connecting to Redis

- Local connection: `redis-cli`
- Remote connection: `redis-cli -h <host> -p <port>`
- Authenticate (if required): `AUTH <password>`

---

## Data Structures & Commands

### Strings

- `SET key value` — Set value
- `GET key` — Get value
- `INCR key` — Increment integer value
- `APPEND key value` — Append to string

### Lists

- `LPUSH key value` — Add to head
- `RPUSH key value` — Add to tail
- `LPOP key` — Remove from head
- `RPOP key` — Remove from tail
- `LRANGE key start stop` — Get range

### Sets

- `SADD key value` — Add member
- `SMEMBERS key` — List members
- `SREM key value` — Remove member

### Hashes

- `HSET key field value` — Set field
- `HGET key field` — Get field
- `HGETALL key` — Get all fields

### Sorted Sets

- `ZADD key score member` — Add member
- `ZRANGE key start stop` — Get range
- `ZREM key member` — Remove member

### Other Structures

- `BITOP`, `PFADD`, `XADD`, `GEOADD` — Bitmaps, HyperLogLogs, Streams, Geospatial

---

## Server Management

- `INFO` — Server info
- `CONFIG GET <param>` — Get config
- `CONFIG SET <param> <value>` — Set config
- `MONITOR` — Real-time command log
- `CLIENT LIST` — List clients
- `FLUSHDB` — Delete all keys in current DB
- `FLUSHALL` — Delete all keys in all DBs

---

## Security

- Set a strong password in `redis.conf` (`requirepass <password>`)
- Bind to localhost or restrict access (`bind 127.0.0.1`)
- Disable dangerous commands (`rename-command FLUSHALL ""`)
- Use firewalls to restrict access

---

## Persistence

- **RDB snapshots:** Periodic dumps to disk
- **AOF:** Logs every write operation
- Configure in `redis.conf` (`save`, `appendonly`)

---

## Replication & Clustering

- **Replication:**
  - `SLAVEOF <master_ip> <master_port>`
- **Cluster:**
  - Use `redis-trib.rb` or `redis-cli --cluster` for setup

---

## Pub/Sub

- `PUBLISH channel message` — Send message
- `SUBSCRIBE channel` — Listen for messages

---

## Transactions & Scripting

- `MULTI` — Start transaction
- `EXEC` — Execute transaction
- `DISCARD` — Cancel transaction
- `WATCH key` — Monitor key for changes
- `EVAL <script> <numkeys> <key> [args...]` — Run Lua script

---

## Useful Tools

- `redis-cli` — Command-line interface
- `redis-benchmark` — Performance testing
- `redis-check-aof` / `redis-check-rdb` — Data integrity

---

## Redis Cheat Sheet 1: redis-cli Commands

| Command                       | Description                   |
| ----------------------------- | ----------------------------- |
| redis-cli -h <host> -p <port> | Connect to Redis server       |
| AUTH <password>               | Authenticate with password    |
| INFO                          | Get server info               |
| CONFIG GET \*                 | Get all config parameters     |
| MONITOR                       | Real-time command log         |
| CLIENT LIST                   | List connected clients        |
| KEYS \*                       | List all keys                 |
| EXISTS <key>                  | Check if key exists           |
| DEL <key>                     | Delete a key                  |
| EXPIRE <key> <seconds>        | Set key expiration            |
| TTL <key>                     | Get time-to-live for a key    |
| SELECT <db>                   | Switch database               |
| FLUSHDB                       | Delete all keys in current DB |
| FLUSHALL                      | Delete all keys in all DBs    |
| SAVE                          | Save DB snapshot              |
| BGSAVE                        | Background save DB snapshot   |
| PUBLISH <channel> <message>   | Publish message to channel    |
| SUBSCRIBE <channel>           | Subscribe to channel          |
| MULTI                         | Start transaction             |
| EXEC                          | Execute transaction           |
| DISCARD                       | Cancel transaction            |
| WATCH <key>                   | Watch key for changes         |
| EVAL "lua-script" <numkeys>   | Run Lua script                |

---

## Redis Cheat Sheet 2: Commands When Connected

| Command                 | Description                          |
| ----------------------- | ------------------------------------ |
| SET key value           | Set value for key                    |
| GET key                 | Get value of key                     |
| INCR key                | Increment integer value              |
| APPEND key value        | Append to string value               |
| LPUSH key value         | Add value to head of list            |
| RPUSH key value         | Add value to tail of list            |
| LPOP key                | Remove and get first element of list |
| RPOP key                | Remove and get last element of list  |
| LRANGE key 0 -1         | Get all elements in list             |
| SADD key value          | Add member to set                    |
| SMEMBERS key            | List all members of set              |
| SREM key value          | Remove member from set               |
| HSET key field value    | Set field in hash                    |
| HGET key field          | Get field value from hash            |
| HGETALL key             | Get all fields and values from hash  |
| ZADD key score member   | Add member to sorted set             |
| ZRANGE key 0 -1         | Get all members in sorted set        |
| ZREM key member         | Remove member from sorted set        |
| KEYS \*                 | List all keys                        |
| DEL key                 | Delete key                           |
| EXISTS key              | Check if key exists                  |
| EXPIRE key seconds      | Set expiration for key               |
| TTL key                 | Get time-to-live for key             |
| INFO                    | Get server info                      |
| DBSIZE                  | Get number of keys in current DB     |
| TIME                    | Get server time                      |
| PUBLISH channel message | Publish message to channel           |
| SUBSCRIBE channel       | Subscribe to channel                 |
| MULTI                   | Start transaction                    |
| EXEC                    | Execute transaction                  |
| DISCARD                 | Cancel transaction                   |
| WATCH key               | Watch key for changes                |

---

## References

- [Redis Documentation](https://redis.io/documentation)
- [Redis Commands](https://redis.io/commands)
- [Redis Security](https://redis.io/topics/security)
