# environment tips



## 地址映射的安全性

安全起见，container expose出来是不应该到 0.0.0.0，这样会将MYSQL/REDIS等服务暴露到IENTERNET上；但是例如紧急DEBUG线上故障等等情况，又需要快速临时从外网访问这些后台服务。

如果是阿里云等大的云服务商，可以expose到0.0.0.0，需要的时候临时开放安全组，完成后立刻移除相应的安全组，这种方式既能快速保证安全，也方便偶而的临时需要；

如果是一些小型的云服务商，没有在控制面板提供安全组功能，那就只能用系统自带的工具来处理，例如iptables开放/封禁端口；或者，技术短缺的情况，就不要expose到0.0.0.0，而是expose到内网地址，通过跳板机来访问，或者用iptable临时NAT进去内网。 

redis本身默认不加密码控制，开放公网的端口访问非常危险；即使加了密码限制，REDIS每秒能提供过万（甚至每秒十万次以上）的密码验证尝试，被暴力攻破的风险是比较高的。



## 端口映射

container都用默认端口。

同一类型的服务expose到不同的端口。

例如多个mysql实例，分别映射到HOST的3306, 3307, 3308, ...



## 环境变量

既可以用 -e 直接一个一个设定环境变量，也可以用 --env-file，从文件里读取

```
# 直接设定
docker run -d -t -i -e REDIS_NAMESPACE='staging' \ 
-e POSTGRES_ENV_POSTGRES_PASSWORD='foo' \
-e POSTGRES_ENV_POSTGRES_USER='bar' \
-e POSTGRES_ENV_DB_NAME='mysite_staging' \
-e POSTGRES_PORT_5432_TCP_ADDR='docker-db-1.hidden.us-east-1.rds.amazonaws.com' \
-e SITE_URL='staging.mysite.com' \
-p 80:80 \
--link redis:redis \  
--name container_name dockerhub_id/image_name

# 从文件读取
docker run --env-file ./env.list ubuntu bash
```

