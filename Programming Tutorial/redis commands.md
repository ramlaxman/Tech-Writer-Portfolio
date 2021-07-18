--- String ---
- strlen <key> can be used to get the length of a key’s value; 

- getrange <key> <start> <end> returns the specified range of a value; 

- append <key> <value> appends the value to the existing value (or creates it if it doesn’t exist already)


--- Lists ---
redis>	LPUSH mylist "-Two" "-One" "Zero" "one" "two" "three"					
						
Index		0		1	2	3	   4	5
			Three  Two	One	Zero -One -Two
Rev Index	-6	   -5	-4	-3	  -2   -1

127.0.0.1:6379> LPUSH mylist "-Two" "-One" "Zero" "one" "two" "three"
(integer) 6

127.0.0.1:6379> LRANGE mylist -100 100
1) "three"
2) "two"
3) "one"
4) "Zero"
5) "-One"
6) "-Two"
127.0.0.1:6379> LRANGE mylist 0 5
1) "three"
2) "two"
3) "one"
4) "Zero"
5) "-One"
6) "-Two"
127.0.0.1:6379> LRANGE mylist 0 4
1) "three"
2) "two"
3) "one"
4) "Zero"
5) "-One"


--- Hash  ---

HSET users:dragon-z:goku powerlevel 9000
HGET users:dragon-z:goku powerlevel

For setting multiple field at once,
           key    k    v      k   v 
HMSET users:dragon-z:goku race saiyan age 737  	#multiple k-v pairs
HMGET users:dragon-z:goku race powerlevel		# 
HGETALL users:dragon-z:goku
HKEYS users:dragon-z:goku
HVALS users:dragon-z:goku
HDEL users:dragon-z:goku age

--- Sets ---
Sets are used to store unique values and provide a number of set-based operations, like unions. Sets aren’t ordered but they provide efficient value-based operations.
=========
One key with multiple values.
=========
A friend’s list is the classic example of using a set:

SADD friends:leto ghanima paul chani jessica
SADD friends:duncan paul jessica alia

Regardless of how many friends a user has, we can efficiently tell (O(1)) whether userX is a friend of userY or not:

SISMEMBER friends:leto jessica
SISMEMBER friends:leto vladimir

Furthermore we can see whether two or more people share the same friends:

SINTER friends:leto friends:duncan

Even store the result at a new key:

SINTERSTORE friends:leto_duncan friends:leto friends:duncan
SMEMBERS friends:leto

--- Sorted Sets ---

The last and most powerful data structure are sorted sets. If hashes are like strings but with fields, then sorted sets are like sets but with a score. The score provides sorting and ranking capabilities. If we wanted a ranked list of friends, we might do:

ZADD friends:duncan 70 ghanima 95 paul 95 chani 75 jessica 1 vladimir

Want to find out how many friends duncan has with a score of 90 or over?

ZCOUNT friends:duncan 90 100

How about figuring out chani’s rank?

ZREVRANK friends:duncan chani

We use zrevrank instead of zrank since Redis’ default sort is from low to high (but in this case we are ranking from high to low). 
The most obvious use-case for sorted sets is a leaderboard system. 
In reality though, anything you want sorted by some integer, and be able to efficiently manipulate based on that score, might be a good fit for a sorted set.

================================================================================
> set mylist-tickets 100 NX # NX - Only set the key if it does not already exist.
> set mylist-tickets "Sold Out" NX # Since key is unchanged so is value bcoz of NX.
> set mylist-tickets 0 XX # Only set the key if it already exist.
> get mylist-tickets

