# linux系统安装libgphoto2遇到的问题
我们在[gphoto官网](http://gphoto.org/)可以下载到`libgthoto`的源码，得到一个`libgphoto2-2.5.29.tar.bz2`包，解压发现里面没有`Makefile`文件，只有`makefile.am`和`makefile.in`文件，这需要我们执行`configure`来生成`Makefile`文件，执行后报缺少`libltdl`的错误，于是我们使用yum安装
```
yum -y install libltdl
上次元数据过期检查：3:10:12 前，执行于 2022年03月18日 星期五 11时20分23秒。
未找到匹配的参数: libltdl
错误：没有任何匹配: libltdl

```
可见`libltdl`这个名称和yum源里名称不匹配，我们需要搜索yum源里真实名称
```
[root@localhost libgphoto2-2.5.29]# dnf search all *ltdl*
上次元数据过期检查：3:11:48 前，执行于 2022年03月18日 星期五 11时20分23秒。
=========================================================================================== 名称 和 描述 匹配：*ltdl* ===========================================================================================
libtool-ltdl.x86_64 : Runtime libraries for GNU Libtool Dynamic Module Loader
libtool-ltdl.i686 : Runtime libraries for GNU Libtool Dynamic Module Loader
libtool-ltdl-devel.x86_64 : Tools needed for development using the GNU Libtool Dynamic Module Loader
libtool-ltdl-devel.i686 : Tools needed for development using the GNU Libtool Dynamic Module Loader
=============================================================================================== 描述 匹配：*ltdl* ===============================================================================================
libtool.x86_64 : The GNU Portable Library Tool
```
这里`dnf`是`yum`的一个现代化的分支，它保留了大部分`yum`的接口，可见我们需要安装的是`libtool-ltdl`和`libtool-ltdl-devel`，由于我们系统是64位，所以
```
dnf -y install libtool-ltdl.x86_64
dnf -y install libtool-ltdl-devel.x86_64
```
安装完毕后执行`configure`，这次非常顺利，可以看到`You may run "make" and "make install" now."`的提示，目录下也生成了`Makefile`文件，至此我们可以使用`make`命令安装
```
make && make install
```