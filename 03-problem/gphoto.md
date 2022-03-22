# linux系统安装gphoto遇到的问题
## pkg-config缺少libgphoto2
- 问题描述：在[gphoto官网](http://gphoto.org/)下载`gphoto`源码后解压，执行`configure`命令生成`Makefile`文件，报`pkg-config`缺少`libgphoto2`的错误，但实际上我们已经先安装了`libgphoto2`
- 问题验证：查看`pkg-config`中是否存在`libgphoto2`
```
[root@localhost libgphoto2-2.5.29]# pkg-config --list-all |grep libgphoto
```
可以看到没有结果，那为什么明明已经安装了`libgphoto2`，却找不到呢？这是因为`pkg-config`只会在指定的目录下扫描`.pc`文件，查看`pkg-config`默认扫描目录
```
[root@localhost libgphoto2-2.5.29]# pkg-config --variable pc_path pkg-config
/usr/lib64/pkgconfig:/usr/share/pkgconfig
```
但实际上`libgphoto2`对应的`.pc`文件不在其中
```
[root@localhost libgphoto2-2.5.29]# locate libgphoto|grep -v softwares|grep .pc
/usr/lib64/libgphoto2/2.5.16/pccam300.so
/usr/lib64/libgphoto2/2.5.16/pccam600.so
/usr/lib64/libgphoto2/2.5.16/spca50x.so
/usr/local/lib/pkgconfig/libgphoto2.pc
/usr/local/lib/pkgconfig/libgphoto2_port.pc
/usr/local/share/doc/libgphoto2/camlibs/README.pccam300
/usr/local/share/doc/libgphoto2/camlibs/README.pccam600
/usr/local/share/doc/libgphoto2/camlibs/README.spca50x

```
其中`softwares`目录是我的软件源码目录，排除干扰，可以看到`libgphoto2.pc`和`libgphoto2_port.pc`文件在`/usr/local/lib/pkgconfig`这个目录下，那如何使`pkg-config`能扫描到这个目录呢，我们需要增加`PKG_CONFIG_PATH`的环境变量，将自定义目录加进去
- 解决方案：增加`PKG_CONFIG_PATH`的环境变量，在root用户根目录下修改`.bash_profile`文件,
```
[root@localhost libgphoto2-2.5.29]# cd
[root@localhost ~]# vi .bash_profile 
```
在打开的文件中增加以下内容保存退出
```
export PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig
```
然后执行`source`命令使环境变量生效
```
[root@localhost ~]# source .bash_profile
```
- 验证： 重新查看pkg-config中是否存在libgphoto2
```
[root@localhost libgphoto2-2.5.29]# pkg-config --list-all |grep libgphoto
libgphoto2_port                libgphoto2_port - Device-independent access to serial, USB, and other ports
libgphoto2                     libgphoto2 - Library for easy access to digital cameras

```
说明配置生效了
## 缺少libexif
- 问题描述：解决`pkg-config缺少libgphoto2`的问题后，继续执行`configure`命令，报了一个缺少`libexif`的错误，实际上我们也安装了`libexif`
- 问题验证：一开始我们想到解决`pkg-config缺少libgphoto2`的问题思路，但是发现系统中根本没有`libexif`的`.pc`文件
```
[root@localhost libgphoto2-2.5.29]# locate libexif
/usr/lib64/libexif.so.12
/usr/lib64/libexif.so.12.3.4
/usr/share/doc/libexif
/usr/share/doc/libexif/COPYING
/usr/share/doc/libexif/NEWS
/usr/share/doc/libexif/README
/usr/share/locale/be/LC_MESSAGES/libexif-12.mo
/usr/share/locale/bs/LC_MESSAGES/libexif-12.mo
/usr/share/locale/cs/LC_MESSAGES/libexif-12.mo
/usr/share/locale/da/LC_MESSAGES/libexif-12.mo
/usr/share/locale/de/LC_MESSAGES/libexif-12.mo
/usr/share/locale/en_AU/LC_MESSAGES/libexif-12.mo
/usr/share/locale/en_CA/LC_MESSAGES/libexif-12.mo
/usr/share/locale/en_GB/LC_MESSAGES/libexif-12.mo
/usr/share/locale/es/LC_MESSAGES/libexif-12.mo
/usr/share/locale/fr/LC_MESSAGES/libexif-12.mo
/usr/share/locale/it/LC_MESSAGES/libexif-12.mo
/usr/share/locale/ja/LC_MESSAGES/libexif-12.mo
/usr/share/locale/ms/LC_MESSAGES/libexif-12.mo
/usr/share/locale/nl/LC_MESSAGES/libexif-12.mo
/usr/share/locale/pl/LC_MESSAGES/libexif-12.mo
/usr/share/locale/pt/LC_MESSAGES/libexif-12.mo
/usr/share/locale/pt_BR/LC_MESSAGES/libexif-12.mo
/usr/share/locale/ru/LC_MESSAGES/libexif-12.mo
/usr/share/locale/sk/LC_MESSAGES/libexif-12.mo
/usr/share/locale/sq/LC_MESSAGES/libexif-12.mo
/usr/share/locale/sr/LC_MESSAGES/libexif-12.mo
/usr/share/locale/sv/LC_MESSAGES/libexif-12.mo
/usr/share/locale/tr/LC_MESSAGES/libexif-12.mo
/usr/share/locale/uk/LC_MESSAGES/libexif-12.mo
/usr/share/locale/vi/LC_MESSAGES/libexif-12.mo
/usr/share/locale/zh_CN/LC_MESSAGES/libexif-12.mo
```
再看`configure`命令的提示，告诉我们配置`LIBEXIF_LIBS`环境变量，看上面结果，也只有`/usr/lib64`这个目录稍微像一些，临时改一下
```
[root@localhost libgphoto2-2.5.29]# export LIBEXIF_LIBS=/usr/lib64
```
再执行`configure`命令，竟然不报错了，说明有效
- 解决方案：增加`LIBEXIF_LIBS`的环境变量，在root用户根目录下修改`.bash_profile`文件,
```
[root@localhost libgphoto2-2.5.29]# cd
[root@localhost ~]# vi .bash_profile 
```
在打开的文件中增加以下内容保存退出
```
export LIBEXIF_LIBS=/usr/lib64
```
然后执行`source`命令使环境变量生效
```
[root@localhost ~]# source .bash_profile
```