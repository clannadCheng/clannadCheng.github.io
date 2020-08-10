



## 搜索镜像

docker search name

### 语法

```
docker search [OPTIONS] TERM
```

OPTIONS说明：

- **--automated :**只列出 automated build类型的镜像；
- **--no-trunc :**显示完整的镜像描述；
- **-s :**列出收藏数不小于指定值的镜像。

### 参数说明：

- **NAME:** 镜像仓库源的名称
- **DESCRIPTION:** 镜像的描述
- **OFFICIAL:** 是否 docker 官方发布
- **stars:** 类似 Github 里面的 star，表示点赞、喜欢的意思。
- **AUTOMATED:** 自动构建。

## 拉取官方的镜像

docker pull name

OPTIONS说明：

- **-a :**拉取所有 tagged 镜像

  

- **--disable-content-trust :**忽略镜像的校验,默认开启

## 查看images

docker images

## 删除 images

docker rmi <id>

### 删除全部的images

docker rmi $(docker images -q)

## 查看所有容器状态

docker ps -a

## 停止容器

docker stop  <id>

## 删除容器

docker rm <id>

### 删除mysql开头的容器 -f 强制

docker rm -f $(docker ps -a |  grep "mysql*"  | awk '{print $1}')

## 进入容器

docker exec -it mysql_ndocker bash

## 启动或者停止容器与重启

```shell
docker start mysql_ndocker
docker stop mysql_ndocker
docker restart mysql_ndocker
```

## 设置容器开机启动

docker update --restart=always 0e55ca509abb



## 安装容器

## 安装mysql
1.查看mysql镜像
	docker search mysql
2.我们拉取官方的镜像,标签为5.7
	docker pull mysql:5.7
3.查看mysql镜像
	docker images |grep mysql
4.创建目录mysql,用于存放后面的相关东西
	mkdir -p ~/mysql/data ~/mysql/logs ~/mysql/conf
	data目录将映射为mysql容器配置的数据文件存放路径
	logs目录将映射为mysql容器的日志目录
	conf目录里的配置文件将映射为mysql容器的配置文件
5.创建容器并启动
docker run -p 13306:3306 --name mysql_ndocker -e MYSQL_ROOT_PASSWORD=123456  -d mysql:5.7
	命令说明：
	        -p 23306:3306：将容器的3306端口映射到主机的23306端口
	        -v ~/mysql/conf/my.cnf:/etc/mysql/my.cnf：将主机~/mysql/conf/my.cnf挂载到容器				的/etc/mysql/my.cnf (这里不额外加配置可以不用配置,我这边没有配置)
	        -v ~/mysql/logs:/logs：将主机~/mysql/logs目录挂载到容器的/logs
	        -v ~/mysql/data:/mysql_data：将主机~/mysql/data目录挂载到容器的/mysql_data
	        -e MYSQL_ROOT_PASSWORD=123456：初始化root用户的密码
6.进入容器
docker exec -it mysql_ndocker bash

7.启动或者停止容器
docker start mysql_ndocker
docker stop mysql_ndocker	

### 安装nginx

``` shell
docker search nginx	
docker pull nginx --拉取镜像
mkdir -p ./nginx/home ./nginx/logs ./nginx/conf --创建挂载路径
docker run --name nginx-run -p 80:80 -d nginx  --创建容器
docker cp b0358e4dc467:/etc/nginx/nginx.conf /home/nginx/conf --cp 容器文件
docker cp -r b0358e4dc467:/usr/share/nginx/html /home/nginx/home --cp 容器文件
docker rm b0358e4dc467 -- 删除容器
docker run -d -p 80:80 --name nginx-run -v 	     	   /home/nginx/home:/usr/share/nginx/ -v /home/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -v /home/nginx/logs:/var/log/nginx nginx  --创建容器与挂载
```

### 安装postgres

直接执行

docker run --name postgres -e POSTGRES_PASSWORD=password -p 54321:5432 -d postgres:11.4

语法说明

run: 创建并运行一个容器；
--name: 指定创建的容器的名字；
-e POSTGRES_PASSWORD=password: 设置环境变量，指定数据库的登录口令为password；
-p 54321:5432: 端口映射将容器的5432端口映射到外部机器的54321端口；
-d postgres:11.4: 指定使用postgres:11.4作为镜像。

注意：
postgres镜像默认的用户名为postgres，
登陆口令为创建容器是指定的值。

