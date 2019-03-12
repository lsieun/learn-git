# git报错

## RPC failed; curl 18 transfer closed with outstanding read data remaining

错误信息，如下：

```txt
error: RPC failed; curl 18 transfer closed with outstanding read data remaining
fatal: The remote end hung up unexpectedly
fatal: early EOF
fatal: index-pack failed
```

这个错误是因为项目太久，tag资源文件太大

解决方式一， 网上大部分解决措施：命令终端输入

```bash
git config --global http.postBuffer 524288000
```

解决方式二，一般`clone http`方式的容易产生此问题，改成SSH的方式也有效，即`https://`改为`git://`。当然，前提是你配置好了ssh秘钥，配置方法每个git平台都会有教程的。一般来说`https`的方式容易遇到此问题，而`ssh`的方式不会。所以可以这样解决。


