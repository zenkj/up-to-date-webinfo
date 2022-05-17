# 如何查找某个文件在哪个apt安装包里

使用apt-file

```sh
~$ sudo apt-file update
~$ apt-file search libz.so
lib32z1: /usr/lib32/libz.so.1             
lib32z1: /usr/lib32/libz.so.1.2.11
lib32z1-dev: /usr/lib32/libz.so
libx32z1: /usr/libx32/libz.so.1
libx32z1: /usr/libx32/libz.so.1.2.11
libx32z1-dev: /usr/libx32/libz.so
libzadc-dev: /usr/lib/x86_64-linux-gnu/genwqe/libz.so
libzadc4: /usr/lib/x86_64-linux-gnu/genwqe/libz.so.1
zlib1g: /lib/x86_64-linux-gnu/libz.so.1
zlib1g: /lib/x86_64-linux-gnu/libz.so.1.2.11
zlib1g-dev: /usr/lib/x86_64-linux-gnu/libz.so
~$ # ^ you probably need this last one when compiling emacs
~$
```

