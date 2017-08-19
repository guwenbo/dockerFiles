# redis master-slave setup

## Reference

https://redis.io/

## what is redis

Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries. Redis has built-in replication, Lua scripting, LRU eviction, transactions and different levels of on-disk persistence, and provides high availability via Redis Sentinel and automatic partitioning with Redis Cluster.

## how to build

### Prerequisites

* docker

### Build

* change directory to where the Dockerfile is.

* build image use :

```
docker build .
```

or you can specify the file with the other names , and tag the image , see

https://docs.docker.com/engine/reference/builder/

### Run

#### redis-master

use below command to run a container for redis-master:

```
docker run --name redis-master -it -d -v path_to_redis-master_on_host:/config image:tag
```

/config used to store the redis.conf for container

#### config for redis-master

```
cp redis.conf path_to_redis-master_on_host
```

modify redis.conf , such as below param:

* bind (use container name as domain to replace it)
* daemonize (yes)

enter into redis-master container , and:

```
redis-server /config/redis.conf
```

#### redis-slave

use below command to run a container for redis-slave:

```
docker run --name redis-slave -it -d --link redis-master:master -v path_to_redis-slave_on_host:/config image:tag
```

#### config for redis-slave

```
cp redis.conf path_to_redis-slave_on_host
```

modify redis.conf , such as below param

* bind (use container name as domain to replace it)
* daemonize (yes)
* slaveof master 6379

enter into redis-master container , and:

```
redis-server /config/redis.conf
```

### test

enter redis-master container and :

```
redis-cli -h domain -p 6379
set guwenbo cool
```

enter redis-slave container , and :

```
redis-cli
get guwenbo
```

the result is cool.
