# 如何配置pip的国内镜像源

pip默认从[国外](https://files.pythonhosted.org/)下载安装包，一般非常慢，将其改为国内镜像源会快很多。

国内各大云厂商、某些重点高校都维护了自己的镜像源，以[清华大学镜像源](https://pypi.tuna.tsinghua.edu.cn/simple)为例，可以通过如下命令修改镜像源：

```sh
(myvenv)$ pip install -U pip  # 将pip升级到最新版本(>=10.0.0)
(myvenv)$ pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

一般pip的配置会写到~/.config/pip/pip.conf(centos)或~/.pip/pip.conf(ubuntu)文件中，内容如下：

```sh
(myvenv)$ cat ~/.config/pip/pip.conf
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
(myvenv)$
```

上述升级pip的命令连接到[默认源](https://files.pythonhosted.org/)下载最新pip，如果这个链接访问非常慢，甚至无法访问，可以使用[清华大学镜像源](https://pypi.tuna.tsinghua.edu.cn/simple)来升级pip:

```sh
(myvenv)$ pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pip -U
```

除了上述[清华大学镜像源](https://pypi.tuna.tsinghua.edu.cn/simple)外，还可以使用如下国内云厂商的镜像源：

- 华为云pip镜像源 - https://repo.huaweicloud.com/repository/pypi/simple
- 阿里云pip镜像源 - http://mirrors.aliyuncs.com/pypi/simple/
- 腾讯云pip镜像源 - https://mirrors.cloud.tencent.com/pypi/simple
