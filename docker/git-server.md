# git-server

git官方好象没有出image，找到的各种自制image都各种麻烦。既然如此，直接简单粗暴的自已做一个出来：

下载centos7.2的IMAGE，然后安装需要的一些依赖就完事了。

注意的就是22端口可能被HOST用掉了，因此expose到2222端口即可。

然后在本地记得把repo的地址上加上端口2222即可。

```

docker run -dit --name git-server -p "0.0.0.0:2222:22" -v git-vol:/home/git/repos  centos:7.2.1511
docker exec -d git-server sh -c "yum -y install openssh-server"
docker exec -d git-server sh -c "yum -y install git"
docker exec -d git-server sh -c "useradd git"
docker exec -d git-server sh -c "chown -R git /home/git"
docker exec -d git-server sh -c "mkdir /home/git/.ssh"

docker cp ./ssh/win10_rsa.pub  git-server:/home/git/.ssh/
docker cp ./ssh/gvm1_rsa.pub  git-server:/home/git/.ssh/
docker exec -d git-server  sh -c "cat /home/git/.ssh/win10_rsa.pub  >> /home/git/.ssh/authorized_keys"
docker exec -d git-server  sh -c "cat /home/git/.ssh/gvm1_rsa.pub  >> /home/git/.ssh/authorized_keys"

docker exec -d git-server sh -c "chown -R git /home/git"
docker exec -d git-server sh -c "chgrp -R git /home/git"
docker exec -d git-server sh -c "ssh-keygen -A"
docker exec -d git-server sh -c "/usr/sbin/sshd -E /tmp/sshd.log"

```

