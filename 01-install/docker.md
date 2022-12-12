# docker 安装
## Windows系统安装
在[官网](https://www.docker.com/)上下载Windows版本的Docker Desktop安装包安装即可，需要注意docker本质上使用了虚拟机技术，与低版本的Vmaware会冲突
## Linux系统安装
### 检查是否已安装
```sh
yum list installed|grep docker
```
若已安装旧版本，可以先卸载
```sh
yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine
```
### 设置yum仓库
官方网站docker的yum镜像下载非常慢，我们可以使用国内aliyun的镜像仓库

先升级yum工具
```sh
yum install -y yum-utils
```
配置仓库
```sh
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```
### 安装docker
查看可以安装的docker
```sh
 yum list|grep docker
```
安装
```sh
yum -y install docker-ce
```
等待安装成功

验证版本
```sh
docker version
```
注意，安装时可能会报 `问题: 软件包 docker-ce-3:20.10.17-3.el8.x86_64 需要 containerd.io >= 1.4.1，但没有提供者可以被安装 - 软件包 containerd.io-1.4.10-3.1.el8.x86_64 与 runc（由 runc-1.0.2-1.module_el8.5.0+911+f19012f9.x86_64 提供）冲突` 这种错误，这时我们需要先卸载runc
```sh
yum erase runc
```