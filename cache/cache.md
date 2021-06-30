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
* 