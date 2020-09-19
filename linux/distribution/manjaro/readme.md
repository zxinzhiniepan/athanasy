# manjaro

## [切换国内源](https://www.jianshu.com/p/2d096cd9ad61)
### 1. 配置国内源
```shell
pacman-mirrors -i -c China -m rank
```

### 2.设置 archlinuxcn 源,antergos源,arch4edu源:
`vi /etc/pacman.conf`

```txt
[archlinuxcn]
#SigLevel = Optional TrustedOnly
SigLevel = Optional TrustAll
#中科大源
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
#清华源
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch

[antergos]
SigLevel = TrustAll
Server = https://mirrors.tuna.tsinghua.edu.cn/antergos/$repo/$arch

[arch4edu]
SigLevel = TrustAll
Server = https://mirrors.tuna.tsinghua.edu.cn/arch4edu/$arch
```

### 3 更新源列表
```
pacman-mirrors -g
```

```
pacman -S archlinuxcn-keyring
```

#### 更新pacman基本系统
```
pacman -Sy
```

## 安装在vim
```
pacman -S perl
pacman -S vim
```

## 安装输入法
```
pacman -S fcitx fcitx-qt4 fcitx-configtool fcitx-googlepinyin
```
配置输入法
vim ~/.xprofile
```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

## 安装goole-chrome


