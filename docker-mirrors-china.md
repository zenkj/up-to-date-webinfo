# 如何配置docker的国内镜像源

docker国内镜像源很多都不稳定，目前看起来如下配置可用：

```sh
~$ cat /etc/docker/daemon.json
{
    "registry-mirrors": [
        "https://docker.m.daocloud.io",
        "https://dockerproxy.com",
        "https://docker.mirrors.ustc.edu.cn",
        "https://docker.nju.edu.cn"
    ]
}
~$ sudo systemctl restart docker
```
