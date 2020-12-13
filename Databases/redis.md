# Redis

- Start a redis instance within a Docker Container:
```
➜  ~ sudo docker run --name redisdb -p 6379:6379 redis
```

- Access `redis-cli` via container:
```
➜  ~ sudo docker exec -it redisdb redis-cli
```

- Set & Get data (key/value pairs):
```
127.0.0.1:6379> set name "Tim"
OK
127.0.0.1:6379> get name
"Tim"
```