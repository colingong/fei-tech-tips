# mysql-sever-client-container

start a mysql server instance

简单粗暴的搭建一个开发环境时，可以直接指定IP，然后每次从IP来访问

需要注意的是这么干，要有一套习惯的规则，例如

```
172.17.8.8			# mysql server
172.17.9.8			# apache httpd
172.17.10.8			# nginx
172.17.11.8			# redis server
172.17.12.8			# python 3.x
......
```

然后 172.17.8.7往下的IP，给临时跑个mysql client来用

(或者，各种临时起的客户端，都172.17.108.x，避免和服务端冲突)

172.17.11.7往下的IP，给临时路个redis-cli用

172.17.12.7往下，各种不同版本或环境的python用



mysql server:

```
# data directory on host: /root/docker-op/mysql56/mount_mysql_data

docker run --name=mysql1                                                                \
--net docker-net1                                                                       \
--ip 172.17.8.8                                                                         \
-d                                                                                      \
-p 0.0.0.0:3306:3306                                                                    \
--name mysql-shanpai                                                                    \
-e MYSQL_ROOT_PASSWORD=xxx                                               			   \
--mount type=bind,src=/root/docker-op/mysql56/conf/my.cnf.d,dst=/etc/my.cnf.d           \
--mount type=bind,src=/root/docker-op/mysql56/conf/my.cnf,dst=/etc/my.cnf               \
--mount type=bind,src=/root/docker-op/mysql56/mount_mysql_data,dst=/var/lib/mysql       \
mysql:5.6
```



```
docker run --name=mysql1                                                                \
--net docker-net1                                                                       \
--ip 172.17.8.18                                                                        \
-d                                                                                      \
-p 0.0.0.0:3307:3306                                                                    \
--name mysql-baidu                                                                      \
-e MYSQL_ROOT_PASSWORD=xxx                                               \
--mount type=bind,src=/root/docker-op/mysql56/conf/my.cnf.d,dst=/etc/my.cnf.d           \
--mount type=bind,src=/root/docker-op/mysql56/conf/my.cnf,dst=/etc/my.cnf               \
--mount type=bind,src=/root/docker-op/mysql56/mount_mysql_baidu,dst=/var/lib/mysql      \
mysql:5.6
```



mysql client:

```
echo "host_ip, username"
docker run                                      \
--net docker-net1                               \
--ip 172.17.8.108                               \
-it --rm mysql:5.6                              \
 mysql -h$1 -u$2 -p
```

