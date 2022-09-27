# 如何编译nodejs原生扩展（native addon）

nodejs原生扩展在经历一段痛苦的野蛮发展后，已经逐渐演变为基于[Node-API](https://nodejs.org/dist/latest/docs/api/n-api.html)（以前称为N-API）进行开发。Node-API是由Node核心开发组维护的跨Node版本向后兼容的一套C API，该API有自己的发布节奏和版本号，不依赖底层的V8 js引擎、libuv异步库以及openssl/zlib等第三方库的版本变更。为任一支持Node-API的nodejs版本开发的原生扩展，可以保证在以后的nodejs版本中进行加载使用，无需重新编译。

## 编译工具
原生扩展基本使用C/C++进行开发，因此需要安装C/C++编译器和相关工具，安装nodejs时会有Install Additional Tools for Node.js，直接执行即可安装，在Windows上还可以[手动安装](https://github.com/nodejs/node-gyp#on-windows)。

## 
