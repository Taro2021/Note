# Docker

[Home - Docker](https://www.docker.com/)

1. image : 镜像
2. container : 容器
3. repository: 仓库

# Docker 安装

```shell
# 卸载旧版本
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine

# 安装工具包
sudo yum install -y yum-utils

# 设置aliyun镜像仓库
sudo yum-config-manager \
     --add-repo \
     http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
     
# 安装 docker 引擎
sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin

# 查看 docker 版本
docker version

# 启动 docker
sudo systemctl start docker

# 测试
sudo docker run hello-world

# 查看镜像
docker images
```

开启 aliyun docker 镜像加速

```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://xxx.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

![image-20220927205839461](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220927205839461.png)



# docker 常用命令

![image-20220930094827815](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220930094827815.png)

## 帮助命令

---

```shell
docker [xxx] --help  #查看所有命令
docker info
docker version
```



## 镜像命令

---

```shell
#搜索镜像
docker search xxx
#搜索过滤器
docker search xxx --filter=STARS=3000 #STARS大于等于 3000
#拉取镜像
docker pull xxx[:tag] #不写 tag 默认 tag = latest
#删除镜像
docker rmi -f xxx [xxx ,...]
docker rmi -f $(docker images -aq) #删除所有的镜像
```



## 容器命令

---

docker 需要镜像才能创建容器

```shell
docker pull centos #centos镜像来测试
```

### 新建容器并启动

```shell
docker run [参数] image_name /bin/bash
# 参数
--name="NAME" #设定启动容器名，用来区分容器
-d #后台运行
-it #交互运行
-p #指定端口 1.[ip:]主机端口:容器端口 主机映射到容器 2.容器端口
-P #随机端口

exit # 停止并退出交互的容器 Ctrl + P + Q 退出不停止容器
docker ps #查看运行的容器
# ps 参数
-a # 列出所有运行/运行过的容器
-n=? # 运行过最近 n 个容器
-q # 只显示容器编号

docker logs container_id # 查看
docker top container_id # 查看容器内部进程
docker inspect container_id # 查看容器镜像元数据
```

### 容器删除

```shell
docker rm container_id  #删除指定容器
docker rm -f $(docker ps -aq) #删除所有容器 -f 强制删除，可以删除运行中容器
```

### 容器启停

```shell
docker start container_id
docker restart container_id
docker stop container_id
docker kill container_id
```

### 常用命令

```shell
#后台启动容器
docker run -d image_name /bin/bash
#这里的坑：docker 容器的后台运行就必须有一个前台进程，docker 发现没有应用，就会自动停止
docker run -dit image_name /bin/bash
#容器中运行一段脚本
docker run -d image_name /bin/sh -c "while true;do echo taro;sleep 1;done"
#查看日志
docker logs -tf --tail 10 container_id
-tf # 显示日志
--tail number # 要显示日志条数
```

### 进入后台正在运行的容器

```shell
#方式一
docker exec -it container_id /bin/bash #进入容器并开启一个新的终端
#方式二
docker attach container_id #进入容器正在执行的一个终端
```

### 拷贝容器内文件到主机上

```shell
docker cp container_id:container_filePath hostPath
```



### 容器测试用即删

```shell
docker run -it --rm tomcat:9.0
```





# 可视化

## portainer

```shell
docker run -d -p 8088:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
```

![image-20220930110902617](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220930110902617.png)



# 镜像提交

修改容器后提交至本地仓库为一个新的镜像（类似 git）

```shell
docker commit -a="taro" -m="add webapps application" a3f4610dfab0 tomcat1:1.0
docker commit -a="taro" -m="add webapps application" container_id tomcat1:[tag]
```

![image-20220930122815338](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220930122815338.png)



# 

# 容器数据卷



# DockerFile



# Docker 网络





























