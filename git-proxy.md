# 如何为Git配置代理

大部分linux应用配置代理时，只要设置环境变量HTTP_PROXY/HTTPS_PROXY或http_proxy/https_proxy就好，
git处理方式比较特殊，其配置在~/.gitconfig文件中进行设置：

```
[http]
    proxy = http://127.0.0.1:7890
[https]
    proxy = http://127.0.0.1:7890
```

如果懒得编辑文件，也可以直接使用如下命令设置：

```sh
git config --global http.proxy http://127.0.0.1:7890
git config --global https.proxy http://127.0.0.1:7890
```

注意，这个配置是全局的，所以配置完成后，所有的git下载都会经过这个代理。
