# TortoiseSVN创建SVN服务器

前提是安装TortoiseSVN的时候，选择了`command line client tools`

## 1.创建目录

新建一个空目录D:\08-programdata\SVNRepository作为SVN仓库，右键点击，选择`Create repository here`，自动创建目录结构。

## 2.配置svnserver.conf

在conf目录下，修改svnserver.conf文件

```text
# anon-access = read
# auth-access = write
# password-db = passwd
# authz-db = authz
```

这几处删掉前面的`#`号和空格，至于

```text
# realm = My First Repository
```

若有多个仓库可以设置，若只有一个则不修改。

## 3.配置passwd

在conf目录下，修改passwd文件，增加一个用户

```plain
[users]
# harry = harryssecret
# sally = sallyssecret
yuanpan = 123456
```

## 4.配置authz

在conf目录下，修改authz文件，配置新用户所属组及读写权限

```plain
[aliases]
# joe = /C=XZ/ST=Dessert/L=Snake City/O=Snake Oil, Ltd./OU=Research Institute/CN=Joe Average

[groups]
# harry_and_sally = harry,sally
# harry_sally_and_joe = harry,sally,&joe
admin = yuanpan

# [/foo/bar]
# harry = rw
# &joe = r
# * =

# [repository:/baz/fuz]
# @harry_and_sally = rw
# * = r

[/]
@admin = rw
```

## 5.创建服务器

将SVN服务器程序配置成系统服务，并设置自启动:
在cmd窗口执行

```bash
sc create "SVNServerService" binPath= "D:\04-software\TortoiseSVN\bin\svnserve.exe --service -r D:\08-programdata\SVNRepository" DisplayName= "SVNServerService" depend= Tcpip start= auto
```

## 6.启动服务

在服务中找到SVNServerService启动

## 7.客户端访问

在SVN仓库浏览器中访问svn://127.0.0.1，输入账户和密码
