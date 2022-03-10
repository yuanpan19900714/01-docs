## gitbook init报错

- 前提：win10系统，安装了nodejs
- 问题：打开cmd窗口，使用`npm install -g gitbook-cli`命令安装gitbook插件，在指定目录执行`gitbook init`命令会提示以下错误
```
D:\08-programdata\GitBook\我的文档>gitbook init
Installing GitBook 3.2.3
C:\Users\Administrator\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js:287
      if (cb) cb.apply(this, arguments)
                 ^

TypeError: cb.apply is not a function
    at C:\Users\Administrator\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js:287:18
    at FSReqCallback.oncomplete (fs.js:169:5)
```
- 问题原因：高版本的node不再需要某些为了适配低版本node的js方法
- 使用`node --version`命令查看node版本为`v12.19.0`，如果降低本地node版本，可避免此问题，命令为
```
nvm install 10.24.1
nvm use 10.24.1
```
若出现`'nvm' 不是内部或外部命令，也不是可运行的程序或批处理文件。`的提示，则需要先[安装nvm](../01-install/nvm.md)
- 这里我们并不想使用低版本node，所以为解决此问题，需要修改提示中的`polyfills.js`文件，在js中找到下面这个方法
```
function statFix (orig) {
  if (!orig) return orig
  // Older versions of Node erroneously returned signed integers for
  // uid + gid.
  return function (target, cb) {
    return orig.call(fs, target, function (er, stats) {
      if (!stats) return cb.apply(this, arguments)
      if (stats.uid < 0) stats.uid += 0x100000000
      if (stats.gid < 0) stats.gid += 0x100000000
      if (cb) cb.apply(this, arguments)
    })
  }
}
```
搜索发现该方法在js文件的62-64行被调用
```
fs.stat = statFix(fs.stat)
fs.fstat = statFix(fs.fstat)
fs.lstat = statFix(fs.lstat)
```
注释掉这3行即可解决问题