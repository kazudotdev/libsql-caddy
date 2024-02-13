# Sample Project for libsql and local proxy (Caddy)


## How to run

```
docker compose up
```

## How to access via proxy

* Get version
```
curl http://example.localhost/version
```
* Admin API
```
# Create new namespace "test1"
curl -XPOST -H 'Content-Type: application/json' http://admin.example.localhost/v1/namespaces/test1/create -d '{}'
```
* Access every namespace
```
curl -XPOST -H 'Content-Type: application/json' http://test1.example.localhost -d '{"statements": ["CREATE TABLE IF NOT EXISTS users (username)", "INSERT INTO users VALUES (\"alice\")"]}'
curl -XPOST -H 'Content-Type: application/json' http://test1.example.localhost -d '{"statements": ["select * from users"]}' 

## Get following response.
## [{"results":{"columns":["username"],"rows":[["alice"]]}}]
```
```
sqld@75d352ad1e62:~$ ls -l iku.db/dbs/test1/
total 192
-rw-r--r-- 1 sqld sqld  4096 Feb 13 10:17 data
-rw-r--r-- 1 sqld sqld 32768 Feb 13 10:22 data-shm
-rw-r--r-- 1 sqld sqld 70072 Feb 13 10:21 data-wal
-rw-r--r-- 1 sqld sqld   790 Feb 13 10:23 stats.json
drwxr-xr-x 2 sqld sqld  4096 Feb 13 10:17 tmp
drwxr-xr-x 2 sqld sqld  4096 Feb 13 10:17 to_compact
-rw-r--r-- 1 sqld sqld 70104 Feb 13 10:21 wallog
sqld@75d352ad1e62:~$
```
