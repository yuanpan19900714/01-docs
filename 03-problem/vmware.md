# VMware Workstation Pro 启动虚拟机报错
## Hyper-V冲突

- 问题描述：您的主机不满足在启用 Hyper-V 或 Device/Credential Guard 的情况下运行 VMware Workstation 的最低要求
- 问题原因：windows系统安装了docker，必须开启Hyper-V
- 解决方案：

1. 关闭Hyper-V功能：控制面板-->程序和功能-->启用或关闭Windows功能-->去掉Hyper-V的勾选，选择暂不重启
  
2. 关闭Hyper-V服务：在cmd窗口执行以下命令
```
bcdedit /set hypervisorlaunchtype off
```
3. 重启
- 总结：windows系统目前docker与VMware似乎是无法兼容的，不能同时启动，需要使用vmware时按上述方案操作，需要使用docker时需要重新启用Hyper-V并重启电脑，命令为
```
bcdedit /set hypervisorlaunchtype auto
```