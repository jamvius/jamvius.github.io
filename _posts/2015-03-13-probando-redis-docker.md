docker run -d -p 6379:6379 redis:2.8.17
redis-cli -h $(boot2docker ip): conectar a un redis en docker (si se ha mapeado el puerto del redis a fuera)

En redis las databases se identifican por numeros. Se seleccciona con "SELECT 1". Por defecto tiene 16 bd (0-15)

Tutorial REDIS
SET server:name "fido"
GET server:name  => fido
  SET connections 10
    INCR connections => 11
    INCR connections => 12
    DEL connections
    INCR connections => 1
    
EXPIRE server:name 120: fija tiempo de vida variable
(integer) 1
redis 192.168.59.103:6379> TTL server:name: muestra tiempo restante

TTL resource:lock
(integer) -1
Si no esta definido devuelve -1

RPUSH friends "Alice"
(integer) 1
redis 192.168.59.103:6379> RPUSH friends "Bob"
 LPUSH friends "Sam"
 
 RPUSH puts the new value at the end of the list.
 
     RPUSH friends "Alice"
     RPUSH friends "Bob"
 
 LPUSH puts the new value at the start of the list.
 
 
     LPUSH friends "Sam"


 LRANGE friends 0 -1 => 1) "Sam", 2) "Alice", 3) "Bob"
    LRANGE friends 0 1 => 1) "Sam", 2) "Alice"
    LRANGE friends 1 2 => 1) "Alice", 2) "Bob"
    

    LLEN friends => 3

LPOP removes the first element from the list and returns it.


    LPOP friends => "Sam"

RPOP removes the last element from the list and returns it.


    RPOP friends => "Bob"

    SADD adds the given value to the set.
    
    
        SADD superpowers "flight"
        SADD superpowers "x-ray vision"
        SADD superpowers "reflexes"
    
    SREM removes the given value from the set.
    
    
        SREM superpowers "reflexes"

SISMEMBER tests if the given value is in the set. It returns 1 if the value is there and 0 if it is not.


    SISMEMBER superpowers "flight" => 1
    SISMEMBER superpowers "reflexes" => 0

SMEMBERS returns a list of all the members of this set.


    SMEMBERS superpowers => 1) "flight", 2) "x-ray vision"

SUNION combines two or more sets and returns the list of all elements.


    SADD birdpowers "pecking"
    SADD birdpowers "flight"
    SUNION superpowers birdpowers => 1) "pecking", 2) "x-ray vision", 3) "flight"

Sets are a very handy data type, but as they are unsorted they don't work well for a number of problems. This is why Redis 1.2 introduced Sorted Sets.

A sorted set is similar to a regular set, but now each value has an associated score. This score is used to sort the elements in the set.


    ZADD hackers 1940 "Alan Kay"
    ZADD hackers 1906 "Grace Hopper"
    ZADD hackers 1953 "Richard Stallman"
    ZADD hackers 1965 "Yukihiro Matsumoto"
    ZADD hackers 1916 "Claude Shannon"
    ZADD hackers 1969 "Linus Torvalds"
    ZADD hackers 1957 "Sophie Wilson"
    ZADD hackers 1912 "Alan Turing"


    HSET user:1000 name "John Smith"
    HSET user:1000 email "john.smith@example.com"
    HSET user:1000 password "s3cret"

To get back the saved data use HGETALL:


    HGETALL user:1000

You can also set multiple fields at once:


    HMSET user:1001 name "Mary Jones" password "hidden" email "mjones@example.com"

If you only need a single field value that is possible as well:


    HGET user:1001 name => "Mary Jones"
