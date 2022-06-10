# git问题

## git clone 报错

- OpenSSL SSL_read: Connection was reset, errno 10054
  - 原因：
  - 解决方案：在GitBash打开窗口执行

```bash
git config --global http.sslVerify "false"
```

若修改配置后仍提示错误，可能是网络原因
