# 如何配置emacs的国内elpa/melpa镜像源

emacs安装elisp包时一般使用M-x package-install命令，该命令默认到[GNU ELPA](https://elpa.gnu.org/packages/)和[nonGNU ELPA](https://elpa.nongnu.org/nongnu/)上下载安装包，这两个网站国内访问很慢，并且有些包在这两个网站也没有，需要到[MELPA](https://melpa.org/packages/)下载，同样的，这个网站国内访问也很慢，所以有必要使用国内的镜像源，比如[清华ELPA镜像源](http://mirrors.tuna.tsinghua.edu.cn/elpa/gnu/)和[MELPA镜像源](http://mirrors.tuna.tsinghua.edu.cn/elpa/melpa/)

```sh
$ vi ~/.emacs.d/init.el
# 添加如下两行：
(setq package-archives '(("gnu"    . "http://mirrors.tuna.tsinghua.edu.cn/elpa/gnu/")
                         ("nongnu" . "http://mirrors.tuna.tsinghua.edu.cn/elpa/nongnu/")
                         ("melpa"  . "http://mirrors.tuna.tsinghua.edu.cn/elpa/melpa/")))
```

保存重启emacs一般就好了
