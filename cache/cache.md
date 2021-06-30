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