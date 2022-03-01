# 如何为单页面应用配置nginx缓存

随着web应用的用户交互越来越复杂，单页面应用(SPA, single page application)的需求越来越多。SPA的本质是第一步先请求下来前端静态资源（包括index.html首页和相关的js/css前端逻辑和样式），后续所有的页面路由都在前端处理，需要时前端向后端发送ajax/fetch请求获取必要的数据，这样可以做出交互复杂、类客户端应用效果的web应用，用户体验更好。

这种情况下，前端静态资源的缓存将变得非常重要，缓存配置得好，SPA响应飞快，同时在静态资源重新上线部署后在浏览器能够立刻生效。如果配置不好，要么会出现静态资源每次都重新拉取，消耗带宽，用户体验变差，要么出现新版本更新后浏览器没有即时生效，导致用户端出错。

静态资源缓存的总体原则如下：

- 首页(index.html)不做缓存，每次都要重新获取，在浏览器、负载均衡、反向代理处都不能做任何缓存；
- 首页直接或间接引用的其他静态资源(js/css)文件名中都需要带有版本信息，或哈希值；
- 除首页外的其他静态资源，在浏览器、负载均衡、反向代理处都要配置缓存，缓存时间尽可能长（比如一年）。

SPA应用的所有页面url实际上都指向首页index.html，而首页应尽可能简单短小，SPA应用每次发布新版本时，首页都会更新其中对其他静态资源的链接，链接中带有静态资源的版本或哈希信息，这样除了首页之外，旧版本静态资源不会覆盖新版本静态资源，只会变更一个新的名字。只要首页更新后，所有变更的新静态资源都会刷新。所有的旧版本资源都会正常缓存，自然过期。

在这种总体原则下，nginx.conf需要做如下配置：

    location /app1 {
        alias /home/ubuntu/app1/;
        try_files $uri $uri/ /index.html;
        add_header Cache-Control "no-store, no-cache, must-revalidate";
    }

    #for app1 static files
    location /app1/static {
        alias /home/ubuntu/app1/static/;
        expires 1y;
        add_header Cache-Control "public";
        access_log off;
    }

Cache-Control响应头中各参数含义：
- no-store - 不要在浏览器或缓存服务器缓存该请求的任何响应；
- no-cache - 浏览器或缓存服务器可以缓存响应，但在使用这个响应前需要先去后端服务器校验；
- must-revalidate - 浏览器或缓存服务器在本地缓存没有过期前可使用本地缓存，如果本地缓存过期后，必须向后端服务器请求新数据;
- public - 该内容可以被任何缓存（浏览器或缓存服务器）缓存。
