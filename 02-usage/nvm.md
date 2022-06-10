# nvm的使用

## windows系统

[nvm安装](../01-install/nvm.md)完毕后，在安装目录下打开cmd窗口，执行nvm命令，得到以下提示

```dos
D:\04-software\Node.js\nvm>nvm

Running version 1.1.9.

Usage:

  nvm arch                     : Show if node is running in 32 or 64 bit mode.
  nvm current                  : Display active version.
  nvm install <version> [arch] : The version can be a specific version, "latest" for the latest current version, or "lts" for the
                                 most recent LTS version. Optionally specify whether to install the 32 or 64 bit version (defaults
                                 to system arch). Set [arch] to "all" to install 32 AND 64 bit versions.
                                 Add --insecure to the end of this command to bypass SSL validation of the remote download server.
  nvm list [available]         : List the node.js installations. Type "available" at the end to see what can be installed. Aliased as ls.
  nvm on                       : Enable node.js version management.
  nvm off                      : Disable node.js version management.
  nvm proxy [url]              : Set a proxy to use for downloads. Leave [url] blank to see the current proxy.
                                 Set [url] to "none" to remove the proxy.
  nvm node_mirror [url]        : Set the node mirror. Defaults to https://nodejs.org/dist/. Leave [url] blank to use default url.
  nvm npm_mirror [url]         : Set the npm mirror. Defaults to https://github.com/npm/cli/archive/. Leave [url] blank to default url.
  nvm uninstall <version>      : The version must be a specific version.
  nvm use [version] [arch]     : Switch to use the specified version. Optionally use "latest", "lts", or "newest".
                                 "newest" is the latest installed version. Optionally specify 32/64bit architecture.
                                 nvm use <arch> will continue using the selected version, but switch to 32/64 bit mode.
  nvm root [path]              : Set the directory where nvm should store different versions of node.js.
                                 If <path> is not set, the current root will be displayed.
  nvm version                  : Displays the current running version of nvm for Windows. Aliased as v.
```

根据提示可知nvm有以下使用命令：

- `nvm arch`：查看当前操作系统是否为32位或64位，显示结果：

```dos
D:\04-software\Node.js\nvm>nvm arch
System Default: 64-bit.
Currently Configured: 64-bit.
```

- `nvm current`：查看当前使用的node版本

```dos
D:\04-software\Node.js\nvm>nvm current
v12.19.0
```

- `nvm install <version> [arch]`：安装某版本的node
  这里version可以是具体的，比如12.19.0，

```dos
D:\04-software\Node.js\nvm>nvm install 12.19.0
Downloading node.js version 12.19.0 (64-bit)...
```

  也可以是抽象的，比如latest或lts代表最新版本，

```dos
D:\04-software\Node.js\nvm>nvm install lts
Downloading node.js version 16.14.0 (64-bit)...
```

12代表以12开始的最高版本，

```dos
D:\04-software\Node.js\nvm>nvm install 12
Downloading node.js version 12.22.10 (64-bit)...
```

arch可以为空，默认按系统位数来安装，也可以输入数字指定32位或64位，输入all则代表都安装

- `nvm list [available]`：查看通过nvm安装的node版本，list可简写为ls

```dos
D:\04-software\Node.js\nvm>nvm list

    16.14.0
  * 12.19.0 (Currently using 64-bit executable)
```

  list后输入available查看可安装列表，

  ```dos
  D:\04-software\Node.js\nvm>nvm ls available

|   CURRENT    |     LTS      |  OLD STABLE  | OLD UNSTABLE |
|--------------|--------------|--------------|--------------|
|    17.6.0    |   16.14.0    |   0.12.18    |   0.11.16    |
|    17.5.0    |   16.13.2    |   0.12.17    |   0.11.15    |
|    17.4.0    |   16.13.1    |   0.12.16    |   0.11.14    |
|    17.3.1    |   16.13.0    |   0.12.15    |   0.11.13    |
|    17.3.0    |   14.19.0    |   0.12.14    |   0.11.12    |
|    17.2.0    |   14.18.3    |   0.12.13    |   0.11.11    |
|    17.1.0    |   14.18.2    |   0.12.12    |   0.11.10    |
|    17.0.1    |   14.18.1    |   0.12.11    |    0.11.9    |
|    17.0.0    |   14.18.0    |   0.12.10    |    0.11.8    |
|   16.12.0    |   14.17.6    |    0.12.9    |    0.11.7    |
|   16.11.1    |   14.17.5    |    0.12.8    |    0.11.6    |
|   16.11.0    |   14.17.4    |    0.12.7    |    0.11.5    |
|   16.10.0    |   14.17.3    |    0.12.6    |    0.11.4    |
|    16.9.1    |   14.17.2    |    0.12.5    |    0.11.3    |
|    16.9.0    |   14.17.1    |    0.12.4    |    0.11.2    |
|    16.8.0    |   14.17.0    |    0.12.3    |    0.11.1    |
|    16.7.0    |   14.16.1    |    0.12.2    |    0.11.0    |
|    16.6.2    |   14.16.0    |    0.12.1    |    0.9.12    |
|    16.6.1    |   14.15.5    |    0.12.0    |    0.9.11    |
|    16.6.0    |   14.15.4    |   0.10.48    |    0.9.10    |

This is a partial list. For a complete list, visit https://nodejs.org/en/download/releases
  ```

  但展示的只是部分列表，全部列表可在官网<https://nodejs.org/en/download/releases>查看

- `nvm on`：启用nvm，这里可能出现乱码的提示，需要临时修改cmd窗口的编码格式为UTF-8

```dos
D:\04-software\Node.js\nvm>chcp 65001
Active code page: 65001
```

再次执行命令出现下面正常提示

```dos
D:\04-software\Node.js\nvm>nvm on
nvm enabled
exit status 145: The directory is not empty.

exit status 145: The directory is not empty.
```

- `nvm off`：禁用nvm
- `nvm proxy [url]`：查看当前代理，输入url则使用该url地址的代理
- `nvm node_mirror [url]`：使用url对应地址作为node镜像地址，不输入则使用默认的地址<https://nodejs.org/dist/>
- `nvm npm_mirror [url]`：使用url对应地址作为npm镜像地址，不输入则使用默认的地址<https://github.com/npm/cli/archive/>
- `nvm uninstall <version>`：卸载某版本node，具体参见 `nvm install`
- `nvm use [version] [arch]`：使用某版本node，同`nvm install`
- `nvm root [path]`：设置nvm根目录

```dos
D:\04-software\Node.js\nvm>nvm root

Current Root: D:\04-software\Node.js\nvm
```

不输入路径则使用当前目录路径

- `nvm version`：查看nvm版本

```dos
D:\04-software\Node.js\nvm>nvm version
1.1.9
```
