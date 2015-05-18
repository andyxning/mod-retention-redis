<a href='https://travis-ci.org/shinken-monitoring/mod-retention-redis'><img src='https://api.travis-ci.org/shinken-monitoring/mod-retention-redis.svg?branch=master' alt='Travis Build'></a>
mod-retention-redis
===================

Shinken module for saving retention data from schedulers to a redis server 
using [redis-py](https://github.com/andymccurdy/redis-py).

Enhancement
===========
* add redis `key prefix`, so if we use multiple Shinken setups with single 
Redis server, then we can make sure that all keys from different Shinken 
setups can be absolutely unique by using different prefixes.
  * We can only make sure that only one `host_name + service_description` can 
  exist in a single Shinken setup. If we have many Shinken setups, we can 
  not make sure all `host_name + service_description` be unique.
 
* redis `expire time`
  * In case we change the configuration of Shinken, some service
  or host retention info will be deleted and then become useless. We can
  then add an expire time to each host or service info to make the useful
  retention persistent long by updating the expire time every time we save
  the retention info and the useless ones expired sometime and deleted
  automatically by Redis.
 
* add redis `port` and `password`, this is usefull if your Redis server has 
a password and run in a different port instead the default 6379.
  * If you do not specify `server`, it will connect to Redis instance 
  running at `127.0.0.1` with default port `6379` with no password
  * If you do not specify `port` and `password`, it will connect to Redis 
  instance running at `server` with default port `6379` with no password
  * If you specify `port` but not `password`, it will connect to Redis instance
  running at `server` with port `port` with no password
  * If you specify `port` and `password`, it will connect to Redis instance 
  running at `server` with port `port` and password `password`
  * If you specify `key_prefix`, it will add the `key_prefix` to the 
  beginning of the keys to be stored in Redis, Otherwise, Nothing will 
  prefix the keys.
  
Installation
============
Assuming Shinken is installed under standard directory
* install [redis-py](https://github.com/andymccurdy/redis-py) first
* copy files under `module` directory to 
`/var/lib/shinken/modules/redis-retention`(you should create 
directory `redis-retention` first)
* copy files under `etc/module` directory to `/etc/shinken/modules/`
* to all files in `/etc/shinken/schedulers/*.cfg` append `modules` with 
`redis-retention`