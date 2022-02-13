# 如何简化GitHub提交的配置

默认情况下，GitHub支持通过HTTPS、SSH以及GitHub CLI三种方式处理源代码的上传下载。以前习惯直接使用HTTPS，因为相对于SSH，HTTPS有如下优点：
- HTTPS的443端口基本不会被墙，访问起来问题不大，而SSH使用的22端口会被很多防火墙禁止访问（我就用不了）
- git clone时直接从浏览器拷贝地址即可，简单方便

不过HTTPS也有不方便的地方，就是每次提交代码时，需要输入一次GitHub的用户名和密码，相对于经常clone、很少push的现状，这个问题也不是很大。

但自从[2021年8月13日](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/)，GitHub不再支持git push时使用用户名/密码，要么使用HTTPS+token，要么转到SSH。

使用HTTPS+token的方式时，需要首先在GitHub网站上[申请token](https://github.com/settings/tokens)，然后每次提交代码时都要包含这个token，非常麻烦。而使用SSH的话，可以将自己的[公钥(SSH Keys)放到GitHub账户中](https://github.com/settings/keys)，后续git push时就不用输入用户名密码了，很方便。唯一的问题就是需要解决SSH端口访问不了的问题。

幸好，GitHub也意识到22端口经常被墙的问题，提供了[通过HTTPS端口提供SSH访问的办法](https://docs.github.com/en/authentication/troubleshooting-ssh/using-ssh-over-the-https-port)，通过**ssh.github.com:443**来进行SSH方式的提交，一般都没有问题。来验证下（记得首先上传自己的公钥到GitHub账户）：
```sh
$ ssh -T -p 443 git@ssh.github.com
Hi zenkj! You've successfully authenticated, but GitHub does not provide shell access.
$
```

很好，我的防火墙认可了通过443端口进行SSH访问，检查本项目SSH访问地址: git@github.com:zenkj/up-to-date-webinfo.git，改为如下方式访问:
```sh
$ git clone ssh://git@ssh.github.com:443/zenkj/up-to-date-webinfo.git
Cloning into 'up-to-date-webinfo'...
remote: Enumerating objects: 7, done.
remote: Counting objects: 100% (7/7), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 7 (delta 1), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (7/7), done.
Resolving deltas: 100% (1/1), done.
Checking connectivity... done.
$
```

这一长串信息输入还是很麻烦，幸好ssh提供了很方便的配置，编辑~/.ssh/config，在文件尾部添加如下信息：
```sh
Host github.com
Hostname ssh.github.com
Port 443
User git
```

可以通过man ssh_config来查看参数详细说明，简单来说配置文件中通过Host github.com建了一个新的配置分段，后面的Hostname/Port/User都是这个针对这个分段内部的配置。配置好后，再来看看：
```sh
~$ git clone github.com:zenkj/up-to-date-webinfo
Cloning into 'up-to-date-webinfo'...
remote: Enumerating objects: 7, done.
remote: Counting objects: 100% (7/7), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 7 (delta 1), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (7/7), done.
Resolving deltas: 100% (1/1), done.
~$ cd up-to-date-webinfo/
~/up-to-date-webinfo$ ls
LICENSE  README.md
~/up-to-date-webinfo$ git push origin main
Everything up-to-date
~/up-to-date-webinfo$
```
