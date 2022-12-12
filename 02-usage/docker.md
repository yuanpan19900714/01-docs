# docker使用
## 启动
- 关闭防火墙

docker应用会使用到很多端口，一个一个去改防火墙设置太麻烦，可以直接关闭防火墙
```sh
#临时关闭
systemctl stop firewalld
#禁止开机启动
systemctl disable firewalld
#查看防火墙状态
systemctl status firewalld
```
显示` Active: inactive (dead)` ，表示符合要求

- 启动docker
```sh
#启动
systemctl start docker
#关闭
systemctl stop docker
#重启
systemctl restart docker
#查看状态
systemctl status docker
```
显示` Active: active (running)` ，表示启动成功
## 确认版本
```sh
docker -v
#显示以下内容
Docker version 20.10.17, build 100c701
```
## 配置镜像加速
docker官方镜像仓库网速较差，我们需要设置国内镜像服务：
```sh
vim /etc/docker/daemon.json
#在打开的文件中写入以下内容，保存退出
{
    "registry-mirrors":["https://akchsmlh.mirror.aliyuncs.com"]
}
#重新加载文件
systemctl daemon-reload
#重启docker
systemctl restart docker
```
## 常用命令
```sh
#查看镜像
docker images
#拉取镜像，镜像名XXX后可加版本号，不加则默认最新版本
docker pull redis
docker pull redis:latest
#保存镜像，在不同服务器间共用
docker save -o redis.tar redis:latest
```