<a href='https://travis-ci.org/shinken-monitoring/mod-retention-redis'><img src='https://api.travis-ci.org/shinken-monitoring/mod-retention-redis.svg?branch=master' alt='Travis Build'></a>
mod-retention-redis
===================

Shinken module for saving retention data from schedulers to a redis server

Enhancement
===========
* add redis `key prefix`, so if we use multiple Shinken setups with single 
Redis server, then we can make sure that all keys from different Shinken 
setups can be absolutely unique by using different prefixes.
  * We can only make sure that only one `host_name + service_description` can 
  exist in a single Shinken setup. If we have many Shinken setups, we can 
  not make sure all `host_name + service_description` be unique.
 
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