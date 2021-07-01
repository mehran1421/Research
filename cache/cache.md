### What is cache and the reasons for using it?
Cache is a buffering technique that stores frequently received data from a database in a cache.
This reduces the pressure on the database and the time it takes to receive this information 
###### Benefits of caching
1. Performance improvements:
When the required data is available via cache, the pressure on the database is much less
2. Scalability:
Dividing the request load between the cache system and the database, increases the scalability of the system
3. Improved access:
If the database crashes,the cache system can until return the database system, read information and show to users 
###### Do we have to save everything in cache?
no, For these reasons:
1. Cache hardware is very expensive
2. If a lot of information is cached, it may reduce speed reading and writing on it Relative to the database
###### Disadvantages of improper use of cache:
1. Extra Call:
Due to incorrect implementation of the cache system, the information stored in it is not enough and it is forced to search the database.
2. consistency traps:
not update cashing system after update database and give for us Previous data
3. Trashing traps:
Use from keys that have equal value in caching system for example
```
"user":{"name":"mehran","family":"kamrani",...}
```  
the above example, If the user wants to see the profile, show it to another user

### cache in django
*  use Memcached for caching system:
The fastest type of cache in Django, a program for doing cache on dynamic website servers.
this program use server ram for store information and if Fill the ram space, automatic Empties the space of Ram
One drawback is that if the server crashes, all stored information will be lost
this cache run In the form of deamon and Takes a certain amount of memory
all data store in ram and There is no extra load on the database.
we can store for keys **200 KB** and for value **1 MB**  
for use Memcached in django first install tools with `pip install django-memcached`
then write in settings.py files:
```
# settings.py
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.memcached.MemcacheCache',
        'LOCATION': '127.0.0.1:11211',
    }
}
```
* Database caching:
create table inside the database. It is very useful if we have a fast database
and Data is not lost 
**the advantage of database cache** is that we no longer have to search for data in different tables with millions of pieces of information. 
Instead, we put all that information in a table and we can also use indexing for more speed
```
# settings.py
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.db.DatabaseCache',
        'LOCATION': 'my_cache_table',
    }
}
# command line for create table in the LOCATION
python manage.py createcachetable
```
* Filesystem caching:
cache data in a file. It has little security, It is better to put information that is not important in this.
It has a low speed
```
# settings.py
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.filebased.FileBasedCache',
        'LOCATION': '/var/tmp/django_cache', # 'c:/foo/bar' for widows
    }
}
```
### cache with Redis
Is a no-sql database, Its main advantage is that it keeps the data in RAM and can also write the data to disk
this program use server ram for store information and if Fill the ram space, automatic Empties the space of Ram
One drawback is that if the server crashes
we can store for keys **500 MB** and for value **500 MB**.
for use redis in django first install tools with `pip install django-redis` and `pip install redis`
then write in settings.py files:
```
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": 'redis://127.0.0.1:6379/',
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    },
}
```
# Redis VS Memcached:
1. Documentation: Redis is much more comprehensively documented than Memcached ==> Redis > Memcached
2. Database Model: Redis can be a variety of data structures which enable storing of complex objects and provide a rich set of operations over them but Memcached is a plain key value store which only supports binary strings as value.
3. Data Structures: As mentioned above, Redis offers multiple data structure types allowing it to be extremely flexible to use, including Strings, Hashes, Lists, Sets, Sorted Sets, Bitmaps, Bitfields, HyperLogLog, Geospatial indexes, and Streams.
but Memcached only supports plain binary strings which are great for read-only data.
4. Database Rank & Popularity:
```
1. Redis
2. Amazone DynamoDB
3. Microsoft Azure cosmos DB
4. Memcached
5. Hazelcast
```
5. Architecture: Redis and Memcached both follow client-server architecture. Clients populate the data in the server in the form of key-value.
Redis is single threaded where on the other hand Memcached has a multithreaded architecture. Memcached scales better on a system with more cores that can handle more operations if compute capacity is scaled. However, more than one Redis instance can be initiated on the same system to utilize additional cores.
6. Ease of Use: Redis, it is easy to write code as it simplifies complex tasks. Redis has advanced data structures and is not limited to simple string values. For instance, if your application stores data in sets and you want to keep track of sets in a list you can do this easily in Redis.
Memcached, on the other hand, only stores plain string values. So, the application is left to deal with the data structure complexity.
7. Data Partitioning: Redis, data partitioning can be implemented in three different ways:
* a. Client-side partitioning
* b. Proxy-assisted partitioning (example: twemproxy)
* c. Memcached also supports data partitioning across multiple nodes
8. Supported Languages:
```
# Memcached
.Net             Erlang          OCaml        Ruby
C                Java            Perl
C++              Lisp            PHP
ColdFusion       Lua             Python

# Redis
C                Fancy           Objective-C  Rebol 
C#               Go              OCaml        Ruby
C++              Haskell         Pascal       Rust
Clojure          Haxe            Perl         Scala
Crystal          Java            PHP          Scheme
D                JavaScript      Prolog       Smalltalk
Dart             Lisp            Pure Data    Swift
Elixir           Lua             Python       Tcl
Erlang           MatLab          R            Visual Basic
```
9. Transactions: 
Redis “transactions” are executed with the three below guarantees:

- Transactions are serialized and executed sequentially
- Either all of the commands, or none, are processed (atomic transactions)
- Optimistic locking offers an extra guarantee using check-and-set
but Memcached, on the other hand, does not provide transaction management
10. Snapshots/Persistence(ماندگاری/ ذخیره سازی در دیسک)
Redis supports snapshots, and by default, Redis saves snapshots of the dataset on disk in a binary file called dump.rdb. You can manually call a snapshot, or customize the frequency or change threshold for running the operation.
Here are the two persistence options Redis supports:
(RDB persistence, 
AOF persistence)
###### RDB stands for “Redis Database Backup”. It is a compact, point-in-time snapshot of the database at a specific time. It takes up less space, maximizes Redis performance, and is good for disaster recovery.

###### AOF stands for “Append Only File”. AOF keeps track of all the commands that are executed, and in a disastrous situation, it re-execute the commands to get the data back. This method takes more space as all the commands are executed again, and is not a very durable method of snapshotting.
Memcached on the other hand does not support on disk persistence.

11. Scalability: There are two techniques to horizontally scale your Redis database:
(Adding shards in Redis Clusters, 
Adding nodes to a Redis HA (master/replica) setup).
The Memcached server doesn’t provide a mechanism to distribute data across nodes (sharding)

12. Communication Protocol: Redis uses TCP as a network protocol and does not support UDP.
Memcached supports both the TCP and UDP communication protocols
13. Supported Cache Eviction Policies:
```
noeviction: In “noeviction” an error is returned when memory reaches it bound.
allkeys-lru: Lru stands for “least recent used”. This policy removes the least recently used data.
allkeys-lfu: Lfu stands for “least frequently used”. This policy removes the least frequently used data.
allkeys-random: This policy removes the data randomly.
volatile-lru: Volatile data is with expiration data set. This policy removes the least recently used volatile data.
volatile-lfu: Volatile data is with expiration data set. This policy removes the least frequently used volatile data.
volatile-random: This policy removes the volatile data randomly.
volatile-ttl: “TTL” stands for time to live. This policy removes the data that have the shortest time to live.
```
Memcached uses LRU algorithm to evict data when space is required. It first searches for the already expired data to delete if expired data is not available the LRU algorithm is used.
###### LRU: This algorithm is the least used data Is deleted
14. Geospatial Support:
Redis has a data structure called Geospatial indexes that stores the longitude and latitude data of a location. You can perform different operations on the geospatial data, like calculating the distance between two points or finding nearby places.(like Postgresql)
 but Memcached does not have any special data structures to handle geospatial data.
15. Speed Write Operation:
```
||||||||||||             Number of Record
============================================================
Database   |    1000    |   10000   |   100000  |   1000000     
============================================================
Redis      |    34(ms)  |   214(ms) |  1666(ms) |  14638(ms)
------------------------------------------------------------
Memcached  |    23(ms)  |   100(ms) |   276(ms) |   2813(ms)
```
16. Read Operation:
```
||||||||||||             Number of Record
============================================================
Database   |    1000    |   10000   |   100000  |   1000000     
============================================================
Redis      |    8(ms)   |   6(ms)   |    8(ms)  |    8(ms)
------------------------------------------------------------
Memcached  |    9(ms)   |   14(ms)  |   14(ms)  |    30(ms)
```
17. Memory Use:
- for write operations:
```
||||||||||||             Number of Record
============================================================
Database   |    1000    |   10000   |   100000  |   1000000     
============================================================
Redis      |    2.5(MB) |   3.8(MB) |    4.3(MB)|   62.7(MB)
------------------------------------------------------------
Memcached  |    5.3(MB) |   27.2(MB)|   211(MB) |   264.9(MB)
```
- for delete operations:
```
||||||||||||             Number of Record
============================================================
Database   |    1000    |   10000   |   100000  |   1000000     
============================================================
Redis      |    0(MB)   |   0(MB)   |    0(MB)  |   0(MB)
------------------------------------------------------------
Memcached  |    2.2(MB) |   2.1(MB) |   2.2(MB) |   2.2(MB)
```
# Method for Cache:
#### set():
Using it, we can put values ​​into the cache
```
from django.core.cache import cache
cache.set('my_key', 'hello, world!', 30)
```
set 'hello, world!' with 'my_key' key for 30 second into cache
#### get():
we can read and get value if there are in cache
```
cache.get('my_key')
```
after timeout that's mean 30 second :
```
cache.get('my_key')
# None
```
#### delete():
delete key with value in cache:
```
cache.delete('my_key')
# True
```
