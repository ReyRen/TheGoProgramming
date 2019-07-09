**为什么要选择学习Go**

从我听到这个名字到现在，go已经基本成为了各大厂对高性能服务器，kubernates, etcd, terraform等等，都是用go去架构或者正在重构. 可想而知, go的天生优势是有多么的强. 所以这也是我学习的主要原因.

**二进制包下载**

[官方二进制包](https://golang.orgig/dl/)

**安装**

注意: 如果要是从旧的版本升级，必须要先卸载旧的版本. 首先删除的是go目录，一般情况下在/usr/local/go. 其次是删除go的bin目录从你的PATH中, 在linux和FreeBSD下一般是需要编辑/etc/profile或者$HOME/.profile文件，如果是在macOS下有可能在/etc/paths.d/go文件.

将下载的二进制解压缩到/usr/local下并且创建/usr/local/go目录:
```
tar -C /usr/local -xzf go$VERSION.$OS-$ARCH.tar.gz
```

这里需要引入go命令和go工具需要的重要的两个环境变量, GOROOT和GOPATH：
GOROOT就是go的安装环境(/usr/local/go), 所以在~/.bash_profile中:
```
GOROOT=/usr/local/go
export GOROOT
```
当然, 要全盘可以执行go命令和工具，那就得加入到$PATH中, 在~/.bash_profile下:
```$xslt
export $PATH:$GOROOT/bin
```
GOPATH是go install, go get和go的工具都会用到的环境变量. GOPATH是作为编译后二进制的存放目的地，和import时的搜索路径. (其实也是你的工作目录, 可以在src下创建自己的go文件然后开始工作).
GOPATH下主要包含三个文件: src(主要存放源文件), pkg(存放编译好的库文件, 主要是*.a文件), bin(主要存放可执行文件).
你可以自己在任何目录下创建一个GOPATH目录：
```$xslt
cd ~
mkdir gopath
GOPATH=/Users/username/gopath /* added into .bash_profile中*/
```
将GOPATH/bin也得放到$PATH下，否则自己下载的第三方库不能做到全局使用了:
```$xslt
export $PATH:$GOPATH/bin /* in .bash_profile*/
```
这个GOPATH/bin是需要我们go install src/YOUR_PACKAGE_NAME, 这样我们就可以为所欲为了.

**跨平台编译**

`go env`下有两个变量GOOS, GOARCH. 一共支持10中os和9种处理器. 如果我们要生成不同平台架构的可执行程序，只要改变这两个环境变量就可以了，比如要生成linux 64位的程序，命令如下:
```$xslt
GOOS=linux GOARCH=amd64 go build YOUR_SOURCE_PACKAGE
```

**远程包安装**

go提供了一个获取远程包的工具go get,他需要一个完整的包名作为参数，只要这个完成的包名是可访问的，就可以被获取到，比如我们获取一个CLI的开源库:
```$xslt
go get -v github.com/spf13/cobra/cobra
```
就可以下载这个库到我们$GOPATH/src目录下了，这样我们就可以像导入其他包一样import了. 
如果我们使用的远程包有更新，我们可以使用如下命令进行更新,多了一个-u标识:
```$xslt
go get -u -v github.com/spf13/cobra/cobra
```
