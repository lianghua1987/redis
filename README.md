# Redis

### Command

#### OrderSet

```
127.0.0.1:6379> flushdb
127.0.0.1:6379> zadd class 12 lily 13 lucy 5 john 21 hanmeimei 30 hua
127.0.0.1:6379> zrank class hua
(integer) 4
127.0.0.1:6379> zrange class 0 4
1) "john"
2) "lily"
3) "lucy"
4) "hanmeimei"
5) "hua"
127.0.0.1:6379> zrangebyscore class 7 21
1) "lily"
2) "lucy"
3) "hanmeimei"
127.0.0.1:6379> zrangebyscore class 0 100 
1) "john"
2) "lily"
3) "lucy"
4) "hanmeimei"
5) "hua"
127.0.0.1:6379> zrangebyscore class 0 100 limit 3 2
1) "hanmeimei"
2) "hua"
127.0.0.1:6379> zrange class 1 2 withscores
1) "lily"
2) "12"
3) "lucy"
4) "13"
127.0.0.1:6379> zrank class zhangfei
(nil)
127.0.0.1:6379> zrange class 0 -1
1) "john"
2) "lily"
3) "lucy"
4) "hanmeimei"
5) "hua"
127.0.0.1:6379> zrevrange class 0 -1
1) "hua"
2) "hanmeimei"
3) "lucy"
4) "lily"
5) "john"
127.0.0.1:6379> zrange class 0 -1 withscores
 1) "john"
 2) "5"
 3) "lily"
 4) "12"
 5) "lucy"
 6) "13"
 7) "hanmeimei"
 8) "21"
 9) "hua"
10) "30"
127.0.0.1:6379> zremrangebyscore class 12 21
(integer) 3
127.0.0.1:6379> zrange class 0 -1 withscores
1) "john"
2) "5"
3) "hua"
4) "30"
127.0.0.1:6379> zadd class 12 lily 13 lucy 21 hanmeimei
(integer) 3
127.0.0.1:6379> zrange class 0 -1 withscores
 1) "john"
 2) "5"
 3) "lily"
 4) "12"
 5) "lucy"
 6) "13"
 7) "hanmeimei"
 8) "21"
 9) "hua"
10) "30"
127.0.0.1:6379> zremrangebyrank class 0 2
(integer) 3
127.0.0.1:6379> zrange class 0 -1 withscores
1) "hanmeimei"
2) "21"
3) "hua"
4) "30"
127.0.0.1:6379> zrem class hua
(integer) 1
127.0.0.1:6379> zrange class 0 -1 withscores
1) "hanmeimei"
2) "21"
127.0.0.1:6379> zrem class hanmeimei
(integer) 1
127.0.0.1:6379> zrange class 0 -1 withscores
(empty list or set)
127.0.0.1:6379> zadd class 12 lily 13 lucy 5 john 21 hanmeimei 30 hua 
(integer) 5
127.0.0.1:6379> zcard class // count number
(integer) 5
127.0.0.1:6379> zrange class 0 -1 withscores
 1) "john"
 2) "5"
 3) "lily"
 4) "12"
 5) "lucy"
 6) "13"
 7) "hanmeimei"
 8) "21"
 9) "hua"
10) "30"
127.0.0.1:6379> zcount class 13 20
(integer) 1
127.0.0.1:6379> keys *
1) "class"
127.0.0.1:6379> zadd set1 1 one 2 two 4 four
(integer) 3
127.0.0.1:6379> zadd set2 2 two 5 five
(integer) 2
127.0.0.1:6379> zinterstore out 2 set1 set2 weights 2 3
(integer) 1
127.0.0.1:6379> zrange out 0 -1 withscores
1) "two"
2) "10"
127.0.0.1:6379> zrange set1 0 -1 withscores
1) "one"
2) "1"
3) "two"
4) "2"
5) "four"
6) "4"
127.0.0.1:6379> zrange set2 0 -1 withscores
1) "one"
2) "1"
3) "two"
4) "2"
5) "five"
6) "5"
127.0.0.1:6379> zrange set3 0 -1 withscores
1) "one"
2) "1"
3) "seven"
4) "7"
5) "eleven"
6) "11"
127.0.0.1:6379> zinterstore out 3 set1 set2 set3 weights 5 3 1 aggregate sum
(integer) 1
127.0.0.1:6379> zrange out 0 -1 withscores // 1 * 5 + 1 * 3 + 1* 1 = 9
1) "one"
2) "9"
127.0.0.1:6379> zinterstore out 3 set1 set2 set3 weights 5 3 1 aggregate max
(integer) 1
127.0.0.1:6379> zrange out 0 -1 withscores
1) "one"
2) "5"
```

#### Hash

```
127.0.0.1:6379> flushdb
OK
127.0.0.1:6379> hset user1 name lisi
(integer) 1
127.0.0.1:6379> hset user1 age 28
(integer) 1
127.0.0.1:6379> hset user1 height 175
(integer) 1
127.0.0.1:6379> hgetall user1
1) "name"
2) "lisi"
3) "age"
4) "28"
5) "height"

127.0.0.1:6379> hmset user2 name wangwu age 30 height 100
OK
127.0.0.1:6379> hgetall user2
1) "name"
2) "wangwu"
3) "age"
4) "30"
5) "height"
6) "100"

127.0.0.1:6379> hget user1 name
"lisi"
127.0.0.1:6379> hdel user1 name
(integer) 1
127.0.0.1:6379> hgetall user1
1) "age"
2) "28"
3) "height"
4) "175"

127.0.0.1:6379> hlen user1
(integer) 2
127.0.0.1:6379> hlen user2
(integer) 3

127.0.0.1:6379> hexists user1 name
(integer) 0
127.0.0.1:6379> hexists user1 height
(integer) 1

127.0.0.1:6379> hget user1 age
"28"
127.0.0.1:6379> hincrby user1 age 1
(integer) 29
127.0.0.1:6379> hincrbyfloat user1 age 1.5
"30.5"
```

### Transaction

##### Fundamental

```
127.0.0.1:6379> flushdb
OK
127.0.0.1:6379> set wang 200
OK
127.0.0.1:6379> set zhao 700
OK
127.0.0.1:6379> multi
OK
127.0.0.1:6379> decrby zhao 100
QUEUED
127.0.0.1:6379> incrby wang 100
QUEUED
127.0.0.1:6379> exec
1) (integer) 600
2) (integer) 300

127.0.0.1:6379> multi
OK
127.0.0.1:6379> decrby zhao 100
QUEUED
127.0.0.1:6379> INVALID COMMAND
(error) ERR unknown command 'INVALID'
127.0.0.1:6379> get zhao
QUEUED
127.0.0.1:6379> exec
(error) EXECABORT Transaction discarded because of previous errors.
127.0.0.1:6379> get zhao
"600"

// Invalid Transaction
127.0.0.1:6379> multi
OK
127.0.0.1:6379> decrby zhao 100
QUEUED
127.0.0.1:6379> sadd wang pig
QUEUED // Queued, only do semantic validation
127.0.0.1:6379> exec
1) (integer) 500
2) (error) WRONGTYPE Operation against a key holding the wrong kind of value
127.0.0.1:6379> mget zhao wang
1) "500"
2) "300"

127.0.0.1:6379> multi
OK
127.0.0.1:6379> decrby zhao 100
QUEUED
127.0.0.1:6379> incrby wang 100
QUEUED
127.0.0.1:6379> discard
OK
127.0.0.1:6379> mget wang zhao
1) "300"
2) "500"
```

##### Multi - Threading

Thread1:

```
127.0.0.1:6379> flushdb
OK
127.0.0.1:6379> set ticket 1
OK
127.0.0.1:6379> set lisi 300
OK
127.0.0.1:6379> set wangwu 300
OK
127.0.0.1:6379> multi
OK
127.0.0.1:6379> decrby ticket 1
QUEUED
127.0.0.1:6379> decrby lisi 100
QUEUED

// wait
// wait
// wait
// wait
// wait
// wait
// wait
// wait
// wait

127.0.0.1:6379> exec
1) (integer) -1
2) (integer) 200
```

Thread 2:

```
127.0.0.1:6379> get ticket
"1"
127.0.0.1:6379> multi
OK
127.0.0.1:6379> decr ticket
QUEUED
127.0.0.1:6379> exec
1) (integer) 0
```

##### Watch

Thread1:

```
127.0.0.1:6379> flushdb
OK
127.0.0.1:6379> set ticket 1
OK
127.0.0.1:6379> set zhangsan 500
OK
127.0.0.1:6379> set lisi 500
OK
127.0.0.1:6379> watch ticket
OK
127.0.0.1:6379> multi
OK
127.0.0.1:6379> decr ticket
QUEUED
127.0.0.1:6379> decrby zhangsan 100
QUEUED

// wait
// wait
// wait
// wait
// wait
// wait
// wait
// wait
// wait
// wait
// wait

127.0.0.1:6379> exec
(nil)
127.0.0.1:6379> mget ticket zhangsan
1) "0"
2) "500"
```

Thread 2

```
127.0.0.1:6379> multi
OK
127.0.0.1:6379> decr ticket
QUEUED
127.0.0.1:6379> decrby lisi 100
QUEUED
127.0.0.1:6379> exec
1) (integer) 0
2) (integer) 400
```

```
127.0.0.1:6379> unwatch
OK
```

### Subscription

Publisher

```
127.0.0.1:6379> publish news 'hello world'
(integer) 0
127.0.0.1:6379> publish news 'test1'
(integer) 1
```

Subscriber

```
127.0.0.1:6379> subscribe news
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "news"
3) (integer) 1
1) "message"
2) "news"
3) "test1"
```

### Persistence

##### RDS - SNAPSHOT

The RDB persistence performs point-in-time snapshots of your dataset at specified intervals.

每隔**N分钟或者N**次写操作，从内存dump数据形成RDB文件，**压缩**，放在备份目录 - *redis.config*

```
daemonize yes
save 900 1
save 300 10
save 60 1000
rdbcompression yes
rdbchecksum yes
dbfilename dump.rdb
dir /Users/hliang/code/rdb
stop-writes-on-bgsave-error yes
```

Run:

```
./redis-server ../redis.config
./redis-benchmark -n 10000
```

Cons:

Data loss between data save point.

##### AOF - Log

AOF persistence logs every write operation received by the server, that will be played again at server startup, reconstructing the original dataset. Commands are logged using the same format as the Redis protocol itself, in an append-only fashion. Redis is able to rewrite the log on background when it gets too big.

```
appendonly no #是否打开aof日志功能
appendfsync always #每个命令都立即同步到aof，安全，速度慢
appendfsync everysec #折衷方案，每一秒写入一次，由操作系统判断缓冲区大小，同步频率低，速度快

no-appendfsync-on-rewrite yes #正在导出rdb快照时候是否要停止同步aof
auto-aof-rewrite-percentage 100 #aof文件大小比起上次重写时，增长100%
auto-aof-rewrite-min-size 64mb #aof文件至少超过64mb时候重写
```

Q: 在dump rdb过程中，aof如果停止同步，数据会不会丢失？

A：不会，所有操作缓存在内存的队列里，dump完成后统一操作。

Q：aof重写是什么？

A：aof重写是指把内存中的数据逆化成命令，写入aof日志里，解决aof日志过大问题。

Q：如果rdb和aof同时存在，优先用谁来恢复数据？

A：aof,在数据恢复时，如果存在.rdb（有内容），.aof（无内容），由于采用aof优先恢复，导致redis内存清空。

Q：rdb和aof是否可以同时使用？

A：可以，并且推荐。

Q：恢复时rdb和aof那个速度快？

A： rdb，应为其是数据的内存映射，直接载入内存，尔aof是命令，需要逐条执行。