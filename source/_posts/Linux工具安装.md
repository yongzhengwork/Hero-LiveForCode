---
title: Linux工具安装
categories:
  - Linux
tags:
  - Linux
abbrlink: 90504101
date: 2023-08-31 15:48:37
---

<a name="Z8ZQ6"></a>

## 1、lrzsz工具（上传下载）

```shell
#Ubuntu下载安装包
sudo apt-get install -y lrzsz
#CentOS下载安装包
yum install -y lrzsz

#上传文件
rz
#下载文件
sz 文件名
```

<a name="E4rBf"></a>

## 2、sftp工具（上传下载）

```shell
#Xshell的sftp工具
#查看服务器的位置
pwd

#查看本机的位置
lpwd

#固定本机的位置
lcd

#上传文件 或直接put 使用文件弹出框上传
#将本机lcd默认路径下的abc.txt 上传到服务器现在的位置
put abc.txt

#上传多个文件
mput *.txt

#下载文件
#将服务器现在位置的abc.txt文件，下载到lcd默认的本机的位置
get abc.txt 

#下载多个
mget *.txt
```

<a name="IguYR"></a>

## 3、openssh-server工具（ssh远程）

```shell
# Xshell无法SSH连接Ubuntu 
#下载ssh服务
sudo apt-get install openssh-server
# 查看Ubuntu是否开启22端口
netstat -ntlp | grep 22
#检测端口是否开启
telnet 192.168.3.244 22
```

<a name="2sGuJ"></a>

## 4、sshpass工具（ssh远程）

```shell
# 安装软件包
sudo apt-get install sshpass

# 直接远程Linux主机
# sshpass -p password ssh -p port username@IP   默认22端口
sshpass -p xxx ssh root@192.168.11.11

#从密码文件读取文件内容作为密码去远程连接主机
sshpass -f xxx.txt  ssh root@192.168.11.11

#从远程主机上拉取文件到本地
sshpass -p {密码} scp {用户名}@{主机IP}:${远程主机目录} ${本地主机目录}

#将主机目录文件拷贝至远程主机目录
sshpass -p {密码} scp ${本地主机目录} {用户名}@{主机IP}:${远程主机目录} 

#远程执行命令
sshpass -p password ssh username@host <cmd>



sshpass：用于非交互的ssh 密码验证
使用 -p 参数指定明文密码，然后直接登录远程服务器。 它支持密码从命令行,文件,环境变量中读取
1、从命令行方式传递密码
sshpass -p user_password ssh user_name@192.168.1.2  【登录远程机器】
sshpass -p user_password scp -P22 root@192.168.1.2:/home/test  ./ 【远程机器/home/test 复制到本机当前目录】
还可以加参数 -q 【去掉进度显示】

2、从文件读取密码
echo "user_password" > user.passwd
sshpass -f user.passwd ssh user_name@192.168.1.2

3、从环境变量获取密码
export SSHPASS="user_password"
sshpass -e ssh user_name@192.168.1.2 

4、sshpass -p user_password ssh  -o StrictHostKeyChecking=no  user_name@192.168.1.2 
【-o StrictHostKeyChecking=no 表示远程连接时不提示是否输入yes/no】

5、使用sshpass远程免密，在远程主机上执行shell命令，如下远程执行命令：touch /opt/file.txt
sshpass -p user_password ssh  -o StrictHostKeyChecking=no  user_name@192.168.1.2  touch /opt/file.txt
[注：shell命令要和sshpass命令写在一行]
```

<a name="ypt1r"></a>

## 5、ufw防火墙

```shell
#安装防火墙
sudo apt-get install ufw
#防火墙开启
sudo ufw enable
#防火墙重启
sudo ufw reload
#关闭防火墙
sudo ufw disable
#开放22端口
sudo ufw allow 22
#禁用22端口
sudo ufw delete allow 22
#查看端口开启状态
sudo ufw status
#允许此IP访问所有的本机端口
sudo ufw allow from 192.168.3.135
#禁止外部访问SMTP服务
sudo ufw deny smtp
#删除上面建立的某条规则
sudo ufw delete allow smtp 

#推荐使用
sudo apt-get install ufw
sudo ufw enable
sudo ufw default deny 
```

6.定时任务

```shell
#安装定时工具
yum install cronie

#启动服务
service crond start 
#重启服务
service crond restart 
#关闭服务
service crond stop 
#重新加载服务
service crond reload 
#查看状态
service crond status 
0 0 6 * * ? true > /var/log/nginx/access.log
0 0 6 * * ? true > /var/log/nginx/error.log
:wq #保存

# 编辑定时命令 出发vim编辑器
crontab -e

#查看当前所有定时任务
crontab -l

#删除当前所有定时任务
crontab -r
```
