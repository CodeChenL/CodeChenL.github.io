---
title: wine安装教程
date: 2020-03-18 10:02:44
tags: 
 - linux
 - wine
# top: 1
---
# **wine5安装教程**
## 由于篇幅有限下篇讲解通用的wine安装方法:编译安装
## *ubuntu下的安装方法*

### 先更新一下软件清单
```
apt update
```
### 安装wine的依赖
#### 这里先安装依赖的库,
##### 这里推荐使用apt-fast来多线程加速下载具体方法请参考:[apt-fast的安装方法](https://elementzero.gitee.io/blog/bdlguide/#1%EF%BC%8C%E5%AE%89%E8%A3%85apt-fast%E5%8A%A0%E9%80%9F%E4%B8%8B%E8%BD%BD%EF%BC%88%E4%B8%BB%E8%A6%81%E6%98%AF%E4%B8%BAEZ%E4%B8%8B%E8%BD%BD%E5%81%9A%E5%87%86%E5%A4%87%EF%BC%89)
```
add-apt-repository ppa:cybermax-dexter/sdl2-backport
```
#### 开始安装依赖
```
apt-fast install libfaudio0
```
### 正式安装wine
#### 导入wine官方密匙
```
wget -nc https://dl.winehq.org/wine-builds/winehq.key
apt-key add winehq.key
```
#### 添加官方源,并开启32位
##### 这里展示的是ubuntu19的添加方法,其他版本的Ubuntu请把eoan替换为对应的系统代号
```
apt-add-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ eoan main'
apt update
sudo dpkg --add-architecture i386
```
#### 开始安装
```
apt-fast install --install-recommends winehq-devel
```
#### 一切搞定,验证一下
```
wine64 --version
wine --version
```
### 本文参考了
#### [loliboy.com](https://www.loliboy.com/topic/17/%E5%9C%A8ubuntu19%E4%B8%8A%E6%89%93%E5%BC%80elementzero%E7%9A%84%E6%AD%A3%E7%A1%AE%E6%93%8D%E4%BD%9C)