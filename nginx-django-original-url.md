# 如何配置nginx和django，获取到原始url

nginx在通过proxy_pass将请求反向代理到django时，默认会修改两个http头：
- Host头会被修改为被代理服务器的地址（$proxy_host）；
- Connection会被设置为close

这样在后台django处理请求时将无法拿到原始域名。

为此，在配置proxy_pass时做如下配置修改：
```
location / {
    proxy_set_header Host $host;
    proxy_pass http://127.0.0.1:1234;
}
```

这样后台就能拿到原始http请求头中的Host值了。在python代码中，request.build_absolute_uri()将会返回:
    http://my.domain.name/abc/def

如果你的原始http请求是通过https发起的，将会发现上述构造绝对路径返回的是http，而非https。这是因为在proxy_pass时，我们只设置了Host，scheme从https变成了http。为此，我们需要nginx和django配合做一些设置。

在nginx配置文件中再加一句：
```
location / {
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_pass http://127.0.0.1:1234;
}
```

在django工程的settings.py文件中，添加：

```python
SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')

```

此时，request.build_absolute_uri()将会返回正确的原始地址。
