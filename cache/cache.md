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
1. 