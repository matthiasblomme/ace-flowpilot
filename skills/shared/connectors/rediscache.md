# Redis

This file is a compatibility stub. The canonical guidance for the Redis connector (`applicationConnectorType="rediscache"`) is [`redis.md`](redis.md).

The earlier copy here lacked four operations that `redis.md` lists (delete hash field, delete set member, delete list element, delete sorted set member) and used a different example policy name. Note that the Redis policy uses `policyType="RedisConnection"`, unlike the other connector policies.
