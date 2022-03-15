# VS在Windows系统安装问题

## 下载进度一直为0
- 问题描述：当我们在[微软官网](https://visualstudio.microsoft.com/)下载了VS安装文件后，双击安装，在弹出的界面一直显示下载进度为0
- 问题排查：查看安装日志，日志目录为C:\Users\Administrator\AppData\Local\Temp，文件名为dd_bootstrapper_xxx.log，其中xxx为最近的时间戳，可以看到以下错误
```
VisualStudio Bootstrapper:2022/3/15 14:23:41: WebClient failed in 'https://aka.ms/vs/17/release/installer' with '无法连接到远程服务器' - 'https://aka.ms/vs/17/release/installer'.
VisualStudio Bootstrapper:2022/3/15 14:23:41: WebClient failed attempting to access https://aka.ms/vs/17/release/installer via 127.0.0.1
VisualStudio Bootstrapper:2022/3/15 14:23:41: Download failed using WebClient engine. System.Net.WebException: 无法连接到远程服务器 ---> System.Net.Sockets.SocketException: 由于目标计算机积极拒绝，无法连接。 127.0.0.1:443
```
说明安装程序要去<https://aka.ms/vs/17/release/installer>这个地址去下载文件，但是连接有问题，浏览器打开此地址，发现显示“无法访问此网站”，cmd窗口中ping这个域名，结果如下
```
C:\Users\Administrator>ping aka.ms

正在 Ping aka.ms [127.0.0.1] 具有 32 字节的数据:
来自 127.0.0.1 的回复: 字节=32 时间<1ms TTL=128
来自 127.0.0.1 的回复: 字节=32 时间<1ms TTL=128
来自 127.0.0.1 的回复: 字节=32 时间<1ms TTL=128
来自 127.0.0.1 的回复: 字节=32 时间<1ms TTL=128

127.0.0.1 的 Ping 统计信息:
    数据包: 已发送 = 4，已接收 = 4，丢失 = 0 (0% 丢失)，
往返行程的估计时间(以毫秒为单位):
    最短 = 0ms，最长 = 0ms，平均 = 0ms
```
可见本地服务器将域名"aka.ms"解析为127.0.0.1，因此无法下载
- 解决方案：修改本地hosts文件，使DNS将域名解析为正确的ip
  - 查询域名对应IP：访问<https://ipaddress.com/website/aka.ms>得到本地服务器对应aka.ms域名的ip（每台电脑不一样，一定要访问网址查询），比如我本地得到IP为23.204.9.31
  - 修改hosts文件：进入C:\Windows\System32\drivers\etc目录，用文本编辑器编辑hosts文件（若不能编辑，可以将该文件复制到桌面修改再覆盖），在最后增加一行，注意ip一定要是上一步查到的IP
  ```
  23.204.9.31  aka.ms
  ```
- 验证：修改保存hosts文件后，重新ping域名，得到正确结果
```
C:\Users\Administrator>ping aka.ms

正在 Ping aka.ms [23.204.9.31] 具有 32 字节的数据:
来自 23.204.9.31 的回复: 字节=32 时间=229ms TTL=46
来自 23.204.9.31 的回复: 字节=32 时间=230ms TTL=46
来自 23.204.9.31 的回复: 字节=32 时间=222ms TTL=46
来自 23.204.9.31 的回复: 字节=32 时间=225ms TTL=46

23.204.9.31 的 Ping 统计信息:
    数据包: 已发送 = 4，已接收 = 4，丢失 = 0 (0% 丢失)，
往返行程的估计时间(以毫秒为单位):
    最短 = 222ms，最长 = 230ms，平均 = 226ms
```
若仍然显示IP为127.0.0.1，执行`ipconfig /flushdns`命令以刷新DNS缓存
