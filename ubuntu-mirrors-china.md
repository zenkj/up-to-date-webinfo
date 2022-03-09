# 如何配置ubuntu的国内apt镜像源

apt默认从[Ubuntu官方镜像源](http://archive.ubuntu.com/ubuntu)下载安装包，一般国内访问非常慢，将其改为国内镜像源会快很多。

Ubuntu 的软件源配置文件是 /etc/apt/sources.list。修改该文件中的地址为国内镜像源地址，即可使用国内的软件源。

国内各大云厂商、某些重点高校都维护了自己的镜像源，以[清华大学ubuntu镜像源](https://mirrors.tuna.tsinghua.edu.cn/ubuntu/)为例，将系统自带的`/etc/apt/sources.list`做个备份，将该文件替换为下面内容(针对20.04 LTS版本)，即可使用 清华大学 TUNA 的软件源镜像:

```sh
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
```

更换好源后，执行如下命令：

```sh
zenkj ~$ sudo apt update
```

此后即可使用新源。

也可以使用阿里云、网易、中科大等镜像源：

阿里云源：
```sh
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
```
网易源：
```sh
    deb http://mirrors.163.com/ubuntu/ focal main restricted universe multiverse
    deb http://mirrors.163.com/ubuntu/ focal-security main restricted universe multiverse
    deb http://mirrors.163.com/ubuntu/ focal-updates main restricted universe multiverse
    deb http://mirrors.163.com/ubuntu/ focal-proposed main restricted universe multiverse
    deb http://mirrors.163.com/ubuntu/ focal-backports main restricted universe multiverse
    deb-src http://mirrors.163.com/ubuntu/ focal main restricted universe multiverse
    deb-src http://mirrors.163.com/ubuntu/ focal-security main restricted universe multiverse
    deb-src http://mirrors.163.com/ubuntu/ focal-updates main restricted universe multiverse
    deb-src http://mirrors.163.com/ubuntu/ focal-proposed main restricted universe multiverse
    deb-src http://mirrors.163.com/ubuntu/ focal-backports main restricted universe multiverse
```

中科大源：
```sh
    deb https://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse
    deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal main restricted universe multiverse
    deb https://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
    deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
    deb https://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
    deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
    deb https://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse
    deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted universe multiverse
    deb https://mirrors.ustc.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
    deb-src https://mirrors.ustc.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```
