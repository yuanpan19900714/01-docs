# gitlab安装
## Linux系统
- 添加yum源
```sh
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.rpm.sh | bash
```
- yum安装
```sh
yum -y install gitlab-ee
```
- 初始化
```sh
gitlab-ctl reconfigure
```
- 启动
```sh
gitlab-ctl start
```