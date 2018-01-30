---
layout: post
title: Linux常用shell命令汇总
date: 2018-01-30
categories: blog
tags: [Linux,shell]
subtitle: Linux常用shell命令汇总
---

## 系统 ##


```shell
#查看系统版本
cat /etc/issue  
#查看操作系统版本
head -n 1 /etc/issue
# 查看内核
cat /proc/version      
# 查看内核/操作系统/CPU信息
uname -a 
# 查看CPU信息
cat /proc/cpuinfo
# 查看计算机名
hostname
# 列出所有PCI设备
lspci -tv 
# 列出所有USB设备
lsusb -tv            
# 列出加载的内核模块
lsmod
# 查看环境变量
env 
# 查看系统安装时间  如果/root/install.log没删除，也可以看
ls -l /var/sadm/system/logs/install_log    
# 用来显示当前的各种系统对用户使用资源的限制
ulimit -a  
```



## 资源 ##


```shell
# 查看内存使用量和交换区使用量
free -m 
# 查看各分区使用情况
df -h
# 查看指定目录的大小
du -sh <目录名>  
# 查看内存总量
grep MemTotal /proc/meminfo
# 查看空闲内存量
grep MemFree /proc/meminfo
# 查看系统运行时间、用户数、负载
uptime
# 系统资源使用情况
top 
# 系统资源使用情况，按1显示每个CPU核心数，P按CPU使用排序，M按内存使用排序
vmstat  1 
```

## CPU ##

```shell
# 查看cup核数
grep 'model name' /proc/cpuinfo | wc -l  
# 查看系统负载
cat /proc/loadavg 
```


## 磁盘和分区 ##

```shell
# 查看挂接的分区状态
mount | column -t  
# 查看所有分区
fdisk -l 
# 查看所有交换分区
swapon -s 
# 查看磁盘参数(仅适用于IDE设备)
hdparm -i /dev/hda
# 查看启动时IDE设备检测状况
dmesg | grep IDE 
# 查看IO状态
iostat 
```

## 网络 ##

```shell
# 查看所有网络接口的属性
ifconfig
# 查看防火墙设置
iptables -L -n -v
# 查看路由表
route -n
# 查看所有监听端口
netstat -lntp
# 查看所有已经建立的连接
netstat -antp
# 查看网络统计信息
netstat -s
# 统计当前各种状态的连接的数量的命令
netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'
```

## 进程 ##

```shell
ll /proc/PID
ps -eo PID， lstart，etime | grep PID
#查看进程启动目录（lsof -p PID|grep cwd）
pwdx  PID
pwdx  11224
```

## 实时显示进程状态 ##

```shell
top  
top -bn 1 -i -c
#查看僵尸进程
ps aux | grep -e '^[Zz]'
```

## 时间 ##

```shell
# ntpdate命令，网络时间同步命令
ntpdate -u 210.72.145.44
# date命令，查看当前时间
date
# 设置当前时间
date -s 09:38:40
```

## 权限 ##

```shell
# 给文件添加执行权限
chown jiangpeng startup.sh
chmod +x startup.sh
```

## 用户 ##

```shell
# 查看活动用户
w
# 查看指定用户信息
id <用户名> 
# 查看用户登录日志
last
# 查看系统所有用户
cut -d: -f1 /etc/passwd
# 查看系统所有组
cut -d: -f1 /etc/group
# 查看当前用户的计划任务
crontab -l
```

## 服务 ##

```shell
# 列出所有系统服务
chkconfig --list
# 列出所有启动的系统服务
chkconfig --list | grep on
```

## 程序 ##

```shell
# 查看所有安装的软件包
rpm -qa 
# 强制卸载
rpm -e --nodeps
```

## grep ## 

```shell
# 如果你想在当前目录下 查找"hello,world!"字符串,可以这样:
grep -rn "MTO" *
# 在某文件中查找某字符串
cat  ams-node.json | grep MTO
```

## find ##

```shell
# 在/home目录下查找以.txt结尾的文件名 
find /home -name "*.txt" 
# 同上，但忽略大小写
find /home -iname "*.txt" 
# 当前目录及子目录下查找所有以.txt和.pdf结尾的文件 
find . \( -name "*.txt" -o -name "*.pdf" \) 
# 或 
find . -name "*.txt" -o -name "*.pdf" 
# 匹配文件路径或者文件
find /usr/ -path "*local*" 
# 基于正则表达式匹配文件路径 
find . -regex ".*\(\.txt\|\.pdf\)$"
# 同上，但忽略大小写 
find . -iregex ".*\(\.txt\|\.pdf\)$"
```

## who ##  

前有那些用户登入系统

## du ##

```shell
du -h --max-depth=1 |grep [TG] |sort   #查找上G和T的目录并排序
du -sh    #统计当前目录的大小，以直观方式展现
du -h --max-depth=1 |grep 'G' |sort   #查看上G目录并排序
du -sh --max-depth=1  #查看当前目录下所有一级子目录文件夹大小
du -h --max-depth=1 |sort    #查看当前目录下所有一级子目录文件夹大小 并排序
du -h --max-depth=1 |grep [TG] |sort -nr   #倒序排
```

## lsof（list open files） ##

即：列出被进程所打开的文件的信息，而被打开的文件可以是：   
1. 普通文件   
2. 目录  
3. 网络文件系统的文件   
4. 字符或设备文件   
5. (函数)共享库   
6. 管道，命名管道   
7. 符号链接    
8. 网络文件（例如：NFS file、网络socket，unix域名socket）    
9. 还有其它类型的文件，等等    

## iptables ##
iptables缺省具有3个规则表：   
   （1）Filter：用于设置包过滤    
   （2）NAT：用于设置地址转换    
   （3）Mangle：用于设置网络流量整形等应用    
不同的规则表由不同的规则链组成    
   （1） Filter：INPUT、FORWARD、OUTPUT    
   （2）NAT：PREROUTING、POSTROUTING、OUTPUT    
   （3）Mangle：PREROUTING、POSTROUTING、INPUT、OUTPUT和FORWARD    
iptables配置文件与策略设置文件    
    配置文件：/etc/sysconfig/iptables-config    
    策略文件：/etc/sysconfig/iptables    
iptables [-t tables] [-L] [-n]    
参数说明：   
-t：后面接 iptables 的 table ，例如 nat 或 filter ，如果没有 -t table的话，那么预设就是     -t filter 这个 table ！   
-L：列出目前的 table 的规则     
-n：不进行 IP 与 HOSTNAME 的转换，屏幕显示讯息的速度会快很多！     
iptables [-t tables] [-FXZ]     
参数说明：   
-F ：清除所有的已订定的规则；    
-x ：杀掉所有使用者建立的 chain (应该说的是 tables ）    
-Z ：将所有的 chain 的计数与流量统计都归零    
iptables [-t filter] [-AI INPUT,OUTPUT,FORWARD] [-io interface] [-p tcp,udp,icmp,all] [-s IP/network] [--sport ports] [-d IP/network] [--dport ports] -j [ACCEPT,DROP]     
参数说明：    
-A 　：新增加一条规则，该规则增加在最后面，例如原本已经有四条规则，使用 -A 就可以加上第五条规则！    
-I　 ：插入一条规则，如果没有设定规则顺序，预设是插入变成第一条规则，例如原本有四条规则，使用 -I 则该规则变成第一条，而原本四条变成 2~5    

	INPUT　：规则设定为 filter table 的 INPUT 链 
	OUTPUT ：规则设定为 filter table 的 OUTPUT 链
	FORWARD：规则设定为 filter table 的 FORWARD 链 

-i　 ：设定『封包进入』的网络卡接口   
-o　 ：设定『封包流出』的网络卡接口    

	interface ：网络卡接口，例如 ppp0, eth0, eth1.... 

-p 　：请注意，这是小写呦！封包的协定啦！   
 
	tcp ：封包为 TCP 协定的封包；   
	upd ：封包为 UDP 协定的封包；    
	icmp：封包为 ICMP 协定、    
	all ：表示为所有的封包！    

-s     ：来源封包的 IP 或者是 Network ( 网域 )；  
--sport：来源封包的 port 号码，也可以使用 port1:port2 如 21:23 同时通过 21,22,23 的意           思    
-d     ：目标主机的 IP 或者是 Network ( 网域 )；     
--dport：目标主机的 port 号码；    
-j 　　：动作，可以接底下的动作；    
   ACCEPT ：接受该封包      
   DROP　 ：丢弃封包     
   LOG　　：将该封包的信息记录下来 (预设记录到 /var/log/messages 文件)     

## 释放缓存区内存的方法 ##

```shell
# 清理pagecache（页面缓存）	
echo 1 > /proc/sys/vm/drop_caches
# 或者
sysctl -w vm.drop_caches=1
# 清理dentries（目录缓存）和inodes	
echo 2 > /proc/sys/vm/drop_caches
# 或者
sysctl -w vm.drop_caches=2
# 清理pagecache、dentries和inodes
echo 3 > /proc/sys/vm/drop_caches
# 或者
sysctl -w vm.drop_caches=3
#上面三种方式都是临时释放缓存的方法，要想永久释放缓存，需要在`/etc/sysctl.conf`文件中配置：`vm.drop_caches=1/2/3`，然后sysctl -p生效即可！另外，可以使用sync命令来清理文件系统缓存，还会清理僵尸(zombie)对象和它们占用的内存	
sync
#上面操作后若空闲内存大于swap交换区已使用量，可考虑通过`swapoff -a && swapon -a`将交换去数据写回内存，提升系统运行速度
```

## 列出内存、CPU使用排行 ##

```shell
ps -aux | sort -k4nr | head -5 按内存使用排序
ps -aux | sort -k3nr | head -5 按CPU使用排序
```

## 统计输出项条数 ##

```shell
netstat -natp|grep -i '22' |wc -l 
```   

## 删除空文件 ##

```shell
rm -i `find ./ -size 0`   删除指定大小的文件
```