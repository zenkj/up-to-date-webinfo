# 如何编译nodejs原生扩展（native addon）

nodejs原生扩展在经历一段痛苦的野蛮发展后，已经逐渐演变为基于[Node-API](https://nodejs.org/dist/latest/docs/api/n-api.html)（以前称为N-API）进行开发。Node-API是由Node核心开发组维护的跨Node版本向后兼容的一套C API，该API有自己的发布节奏和版本号，不依赖底层的V8 js引擎、libuv异步库以及openssl/zlib等第三方库的版本变更。为任一支持Node-API的nodejs版本开发的原生扩展，可以保证在以后的nodejs版本中进行加载使用，无需重新编译。

## 编译工具
原生扩展基本使用C/C++进行开发，因此需要安装C/C++编译器和相关工具，安装nodejs时会有Install Additional Tools for Node.js，直接执行即可安装，在Windows上还可以[手动安装](https://github.com/nodejs/node-gyp#on-windows)。

## binding.gyp
nodejs默认使用node-gyp生成在各个平台的C/C++编译工程，mac上使用XCode，windows上使用VisualStudio，linux上可以生成Makefile。
node-gyp从工程根目录下查找binding.gyp文件，读取文件内容，生成各个平台的编译工程。bingding.gyp文件内容实际上就是python的dict数据结构，通过python的eval进行解析。所以没有json格式严格，但比json文件好写，比如可以写#开头的注释，列表和字典最后一项后面可以有逗号等。一个基本的binding.gyp文件长这个样子：

```python
{
    'targets': [
        {
            'target_name': 'fry_sqlite3', # 这里需要是合法的C/C++标识符
            'sources': [  # 指定了要编译的源文件
                'src/fry_sqlite3.c',
                'src/sqlite3.c',
                'src/database.c',
                'src/statement.c', # 注意这里可以有逗号
            ],
        }，
    ]
}
```
需要注意的是，在C/C++代码中，注册模块时，经常会使用宏NODE_GYP_MODULE_NAME来作为模块的名字，这个宏的内容就是来自target_name。这个宏会展开成C/C++的标识符，更具体点是会展开成该原生模块注册函数名的一部分：

```c
#define NAPI_MODULE_X(modname, regfunc, priv, flags)                           \
  EXTERN_C_START                                                               \
  static napi_module _module = {                                               \
      NAPI_MODULE_VERSION,                                                     \
      flags,                                                                   \
      __FILE__,                                                                \
      regfunc,                                                                 \
      #modname,                                                                \
      priv,                                                                    \
      {0},                                                                     \
  };                                                                           \
  NAPI_C_CTOR(_register_##modname) { napi_module_register(&_module); }         \
  EXTERN_C_END
  ```
  上述代码中的modname就是模块的名字，通过宏展开成为模块注册函数名的一部分，比如fry_sqlite3会展开成为_register_fry_sqlite3，所以target_name中不能有非C/C++标识符的字符，比如不能写成fry-sqlite3（别问我怎么知道的，问就是多次莫名其妙编译错误反复看源码找出来的）
