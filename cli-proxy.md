# 如何为不同系统的命令行配置代理
假定代理http和https的代理地址都是http://127.0.0.1:7890

## linux
开启代理：
```sh
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890
export no_proxy=127.0.0.1,localhost
export HTTP_PROXY=http://127.0.0.1:7890
export HTTPS_PROXY=http://127.0.0.1:7890
export NO_PROXY=127.0.0.1,localhost
```
关闭代理：
```sh
unset http_proxy
unset https_proxy
unset no_proxy
unset HTTP_PROXY
unset HTTPS_PROXY
unset NO_PROXY
```

## windows
开启代理：
```cmd
set http_proxy=http://127.0.0.1:7890
set https_proxy=http://127.0.0.1:7890
```

关闭代理：
```cmd
set http_proxy=
set https_proxy=
```
