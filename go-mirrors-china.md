# 如何配置Go的国内镜像

在 Windows 上用 `go install` 安装模块时连不上 `github.com`，通常是网络或代理问题。最常见的解决办法是**配置 Go 模块代理（镜像）**，让它通过国内或更稳定的镜像下载。

如下命令设置国内镜像：

```bash
go env -w GOPROXY=https://goproxy.cn,direct
```

或者：

```bash
go env -w GOPROXY=https://mirrors.aliyun.com/goproxy/,direct
```
