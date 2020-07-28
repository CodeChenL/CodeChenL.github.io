---
title: 编译openwrt
date: 2020-07-28 16:26:37
tags:
 -linux
 -openwrt
 -make
---
# *如何编译openwrt(红米ac2100为例)*

## 本文会介绍一些源码文档没说到的细节,如开启某些插件
## *注意编译固件全程需要特殊的网络环境,否则同步源码很慢,而且会大概率编译出错*
## 1.先更新一下软件清单
```
sudo apt update
```

## 2.安装编译openwrt时需要用到的的依赖
```
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3.5 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf wget swig rsync
```

## 3.开始克隆openwrt的源码仓库
### 这里比较推荐lean大佬的仓库,因为成功率比较高,也有一些官方仓库没有的插件.懂的都懂-_-
```
git clone https://github.com/coolsnowwolf/lede 
```
### *注意要使用普通用户,不要使用root,不然可能会编译失败*

## 4.添加插件地址
### 如果不添加问题也不大,不过会失去某些不可描述的插件
### 进入刚刚同步的源码文件夹,我这里已在同步时设置为RM2100
```
cd ./RM2100
```
### 正式添加插件地址,可使用你熟悉的编辑器编辑源码文件夹下的feeds.conf.default文件,把#注释去掉即可
```
vim ./feeds.conf.default
```
### 改成下面这样
```
src-git packages https://github.com/coolsnowwolf/packages
src-git luci https://github.com/coolsnowwolf/luci
src-git routing https://git.openwrt.org/feed/routing.git
src-git telephony https://git.openwrt.org/feed/telephony.git
src-git freifunk https://github.com/freifunk/openwrt-packages.git
src-git video https://github.com/openwrt/video.git
src-git targets https://github.com/openwrt/targets.git
src-git management https://github.com/openwrt-management/packages.git
src-git oldpackages http://git.openwrt.org/packages.git
src-link custom /usr/src/openwrt/custom-feed
src-git helloworld https://github.com/fw876/helloworld
```

## 5.修改编译配置文件
### 进入配置界面,进去后可以看到是比较方便的可视化界面
```
make menuconfig
```
### 配置界面的逻辑是回车进入,空格勾选,下面的配置选择是基于我的红米ac2100,请根据自己的情况进行选择
```
Target System是处理器的架构,我这里选择MediaTek Ralink MIPS

Subtarget是处理器的型号,我这里选择MT7621 based boards

Target Profile是机型,我这里选择Xiaomi Redmi Router AC2100
```
### 一般配置到这里就可以进行编译,编译以后就是一个openwrt的基础纯净包,以后的文章我会发如何添加插件和一些我自己经常会编译的一些插件(疯狂暗示还不快收藏本网站^_^)

## 6.预下载编译要用到的源码
### 注意需要使用特殊的上网环境,懂的都动-_-
```
make download -j8 V=s
```
## 7.开始正式编译
```
make -j$(nproc) || make -j1 V=s
```
### "||"代表前面的命令如果失败则使用后面的命令
### "-j $(nproc)"代表使用多线程,线程数量为"$(nproc)","$(nproc)"实际数字为cpu的最大线程数
### 之所以会用到"make -j1 V=s",是因为如果多线程编译出错,单线程编译可能会成功,"V=s"是指输出详细的编译提示

## ------本文部分引用<a href="https://github.com/coolsnowwolf/lede">lean的源码仓库的说明文档</a>





















