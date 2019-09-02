# redis-server-client



```
REDIS_CONF_FILE=/root/docker-op/redis4/conf/redis.conf
CONTAINER_NAME="redis-6379"

docker run                                                                              \
        -v ${REDIS_CONF_FILE}:/usr/local/etc/redis/redis.conf                           \
        -d                                                                              \
        -p 0.0.0.0:6379:6379                                                            \
        --name ${CONTAINER_NAME}                                                        \
        redis:4-alpine                                                                  \
        redis-server /usr/local/etc/redis/redis.conf


# 配置文件里设定密码登录：requirepass its987654321```

