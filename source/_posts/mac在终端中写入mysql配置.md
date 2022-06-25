---
layout: port
title: mac在终端中写入mysql配置
date: 2022-04-07 17:29:35
tags: 计算机知识
---



mac 配置mysql 环境变量
解决：安装mysql后，在终端输入mysql提示 Mac -bash: mysql: command not found问题

下载安装mysql
mysql v8.0.12 https://dev.mysql.com/downloads/mysql/
配置mysql时使用user legacy password encryption （兼容性好些）

配置环境变量
打开终端，输入：
sudo vim /etc/profile
注：(同JDK环境变量配置目录)
在profile文件最后写入：
export PATH=$PATH:/usr/local/mysql/bin

退出vim并保存 :wq!
输入 source /etc/profile 更新配置
这样环境变量就配置好了，下面是进入 mysql：
确定mysql已经开启：


输入 mysql -u root -p
输入之前配置的 mysql 密码

