docker搭建多台虚拟机



### 使用docker 基于ubuntu 搭建hadoop集群

- https://www.cnblogs.com/huangqingshi/p/12531717.html

- 50070端口访问失败: https://blog.csdn.net/kou_bi/article/details/111804382

- hadoop 国内镜像下载: wget https://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/common/hadoop-2.10.2/hadoop-2.10.2.tar.gz

  ```sh
  tar -zxvf hadoop-2.10.2.tar.gz -C /usr/local
  cd /usr/local
  mv hadoop-2.10.2 hadoop
  
  
  ```

### 关于docker基于centos7 搭建hadoop的尝试

##### 拉取centos7 镜像: 

- docker pull centos:centos7

##### 查看本地镜像: 

- docker images

##### 运行容器, 通过exec命令进入centos容器

- docker run -itd --name docker-hadoop-1 --privileged centos:centos7
- Docker exec -it centos-test /bin/bash

##### 检查是否安装成功

- Docker ps

##### 删除容器

- Docker rm {container_id}
- Docker rm -f {container_id}

##### 修改容器tag

- docker commit container_id new_tag

##### docker 容器授权

- docker run -tdi --privileged centos init 

##### docker 容器service 命令使用失败

- yum inatsll initscripts

##### 解决sshd开启报错问题

- 因为1号进程是bash，不是systemd，所以通过 systemd 启动 sshd 服务不行；可以看看sshd.service 这里是什么命令参数，直接后台运行 sshd 这个二进制程序就行

- ```shell
  yum install openssh-server -y
  /usr/sbin/sshd-keygen
  /usr/sbin/sshd -D &
  passwd root
  ```

##### 安装openssh

- Yum install opens-server



##### 自定义网络

- Yum -y install net-tools.x86_64

- docker network create --subnet=172.172.0.0/24 net-bro

##### docker-compose 方式实现多个centos7容器挂载

