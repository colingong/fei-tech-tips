# redis-server-client



```
docker run                                                                                \
        -v /root/docker-op/redis4/conf/redis.conf:/usr/local/etc/redis/redis.conf         \
        --net docker-net1                                                                 \
        --ip 172.17.8.17                                                                  \
        -d                                                                                \
        -p 0.0.0.0:6379:6379                                                              \
        --name redis-baidu-6379                                                           \
        redis:4-alpine                                                                    \
        redis-server /usr/local/etc/redis/redis.conf

# 配置文件里设定密码登录：requirepass its987654321
```

