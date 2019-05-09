# php5-apache

docker hub已经搜不到php5-apache的官方image。但是直接pull还可以。

```
docker run -d --name orig-php5          \
        -p 0.0.0.0:80:80                \
        --mount type=bind,src=/root/docker-op/php5-apache/php_src,dst=/var/www/html \
        php:5-apache 
```

直接这么跑起来（当然还要自已加一些必要的extension，例如redis等）不合适，至少各种密码不要硬编码到代码里，放环境变量里会好一点。

（THINKPHP被爆破的时候，全部源代码直接被暴露，那些微信、支付宝的KEY。。。好杯具。）

