# Redis

 - Caching
 - In-Memory Database (as opposed to On Disk)
   - can & does write to disk - see: https://redis.io/topics/persistence
 - Messaging via Pub/Sub
 - NoSQL
 - Fast 

## Redis-CLI

- Start a (new - will build image) redis instance within a Docker Container:
```
➜  ~ sudo docker run --name redisdb -p 6379:6379 redis
```
- Start existing container:
```
➜  ~ sudo docker start -a redisdb
```

- Access `redis-cli` via container:
```
➜  ~ sudo docker exec -it redisdb redis-cli
```

- Test connection:
```
127.0.0.1:6379> ping
PONG
```

- Set & Get data (key/value pairs):
```
127.0.0.1:6379> set name "Tim"
OK
127.0.0.1:6379> get name
"Tim"
127.0.0.1:6379> SET foo 101
OK
127.0.0.1:6379> GET foo
"101"
```

- Check if key exists:
```
127.0.0.1:6379> EXISTS foo
(integer) 1
127.0.0.1:6379> EXISTS bar
(integer) 0
```

- Delete a key:
```
127.0.0.1:6379> SET bar 202
OK
127.0.0.1:6379> GET bar
"202"
127.0.0.1:6379> EXISTS bar
(integer) 1
127.0.0.1:6379> DEL bar
(integer) 1
127.0.0.1:6379> EXISTS bar
(integer) 0
```

- Flush (i.e. delete) all data:
```
127.0.0.1:6379> FLUSHALL
OK
127.0.0.1:6379> GET foo
(nil)
```

- Set expiration on an item (uses seconds):
```
127.0.0.1:6379> SET greeting "Hello World"
OK
127.0.0.1:6379> EXPIRE greeting 30
(integer) 1
127.0.0.1:6379> TTL greeting
(integer) 21
127.0.0.1:6379> TTL greeting
(integer) 14
127.0.0.1:6379> TTL greeting
(integer) -2
127.0.0.1:6379> GET greeting
(nil)
```

- use `SETEX` to combine `SET` & `EXPIRE`
```
127.0.0.1:6379> SETEX greeting 30 "Hello World"
OK
```

- set multiple pairs in single command:
```
127.0.0.1:6379> MSET key01 "Howdy" key02 "There"
OK
127.0.0.1:6379> GET key02
"There"
```

- append value to existing key:
```
127.0.0.1:6379> APPEND key01 " World"
(integer) 11
127.0.0.1:6379> GET key01
"Howdy World"
```

- create a list:
```
127.0.0.1:6379> LPUSH demoList "Alpha"
(integer) 1
127.0.0.1:6379> LPUSH demoList "Bravo"
(integer) 2
127.0.0.1:6379> LPUSH demoList "Charlie"
(integer) 3
127.0.0.1:6379> LRANGE demoList 0 -1
1) "Charlie"
2) "Bravo"
3) "Alpha"
127.0.0.1:6379> RPUSH demoList "Yankee"
(integer) 4
127.0.0.1:6379> LRANGE demoList 0 -1
1) "Charlie"
2) "Bravo"
3) "Alpha"
4) "Yankee"
```

- create a hash (i.e. something similiar to a JS Object) with multiple key/value pairs:
```
127.0.0.1:6379> HMSET user:admin name "Alex Admin" email "admin@redis.com" isAdmin "True"
OK
127.0.0.1:6379> HGETALL user:admin
1) "name"
2) "Alex Admin"
3) "email"
4) "admin@redis.com"
5) "isAdmin"
6) "True"
```


- Subscribe (to a channel):
```
127.0.0.1:6379> subscribe sample-channel
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "sample-channel"
3) (integer) 1
4) "message"
5) "sample-channel"
6) "Hello World. This is a new message!"
```
- Publish (to a channel):
```
127.0.0.1:6379> publish sample-channel "Hello World. This is a new message!"
(integer) 1
```