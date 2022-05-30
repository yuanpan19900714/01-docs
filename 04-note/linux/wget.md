# wget下载只有ftp权限服务器上的文件
```
wget -r ftp://$ip//$path --ftp-user=$user --ftp-password=$passwd
```