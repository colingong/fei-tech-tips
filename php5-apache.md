# php5-apache



```
docker run                                                      \
        --name php5-apache                                      \
        -d                                                      \
        -p 0.0.0.0:88:80                                        \
        -v /root/docker-op/httpd2.4/content:/var/www/html       \
        php:5-apache
```

