# GCE上的yum-cron

阿里云上默认并没有自动的update docker



GCE上默认docker-ce和docker-ce-cli会被自动update，如果某个container没有设定为autorestart，docker update之后是不会自动重启container的！嗯，这就是服务跑了一段时间自已挂掉的原因。

yum-cron的配置：

```
/etc/yum.conf
/etc/yum/yum.conf
/etc/yum.repos.d/yum.conf
```



禁止yum-cron自动去update

```
# 命令
yum check-update | grep -i kernel
yum -x kernel* update
yum -x 'php*' -x 'kernel*' update

yum --exclude php update
yum --exclude httpd update
yum --exclude kernel update

yum -exclude php*,httpd*,kernel* update

# 或者，改配置文件/etc/yum.conf file等
[base]
exclude = kernel* owncloud* php* httpd*
exclude=php* httpd* kernel*
exclude=docker-ce*

# vi /etc/yum.repos.d/mongodb.repo
exclude=mongo*

#  if you want yum to ignore that exclude list
yum --disableexcludes=all update

# repolist
yum repolist
```

