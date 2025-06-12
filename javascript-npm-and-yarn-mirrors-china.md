# 如何配置JavaScript的国内npm/yarn/electron镜像源

npm默认从[国外](https://registry.npmjs.org/)下载安装包，一般国内访问非常慢，将其改为国内镜像源会快很多。

国内各大云厂商、某些重点高校都维护了自己的镜像源，以[淘宝npm镜像源](https://registry.npmmirror.com/)为例，可以通过如下命令修改镜像源：

```sh
~$ npm config get registry
https://registry.npmjs.org/
~$ npm config set registry https://registry.npmmirror.com/
~$ cat .npmrc
registry=https://registry.npmmirror.com/
~$ npm config get registry
https://registry.npmmirror.com/
~$ 
```
electron的镜像需要单独设置：
```sh
~$ npm config set electron_mirror "https://npmmirror.com/mirrors/electron/"
```

yarn的命令类似：
```sh
~$ yarn config set registry https://registry.npmmirror.com
~$ cat .yarnrc
# yarn lockfile v1

registry "https://registry.npmmirror.com"
~$ yarn config get registry
https://registry.npmmirror.com/
~$ 
```
electron的镜像需要单独设置：
```sh
~$ yarn config set electron_mirror "https://npmmirror.com/mirrors/electron/"
```
注意带上最后的反斜杠。

一般npm的配置会写到~/.npmrc文件中，yarn配置会写到~/.yarnrc文件中。

除了上述[淘宝npm镜像源](https://registry.npmmirror.com/)外，还可以使用如下国内云厂商的镜像源：

- 华为云pip镜像源 - https://mirrors.huaweicloud.com/repository/npm/
- 腾讯云pip镜像源 - http://mirrors.cloud.tencent.com/npm/
