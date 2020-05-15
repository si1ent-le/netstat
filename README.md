# netstat
```
Author:si1ent
Date:5/14
```
# 介绍

# DDoS中常用命令
## 统计当前链接IP数量
```
如需针对某个端口的统计在netstat之后进行grep来过过滤
netstat -ntu | grep -i ":80" | .....
```
```
netstat -ntu|awk '{print $5}'|cut -d: -f1 -s|sort|uniq -c|sort -nk1 -r
```
![](media/15894431509248/15895090720886.jpg)

## 统计以/16 (xxx.xxx.0.0)显示
```
netstat -ntu|awk '{print $5}'|cut -d: -f1 -s |cut -f1,2 -d'.'|sed 's/$/.0.0/'|sort|uniq -c|sort -nk1 -r
```
![](media/15894431509248/15895090907560.jpg)

## iptables添加指定端口进行封堵
通过以上获取/16网段并通过iptables进行添加，不允许访问到80服务。
！！！！！注意：
在执行iptables前需确定IP地址的归属地，不然导致部分IP无法访问.
```
iptables -A INPUT -p tcp --dport 80 -j DROP -s 192.168.3.0/16
```
![](media/15894431509248/15894443983387.jpg)

## 统计以/24 (xxx.xxx.xxx.0) 显示
```
netstat -ntu|awk '{print $5}'|cut -d: -f1 -s |cut -f1,2,3 -d'.'|sed 's/$/.0/'|sort|uniq -c|sort -nk1 -r
```
![](media/15894431509248/15895091436138.jpg)


## 只统计80端口实时信息
```
netstat -ntu|grep -i ':80' |awk '{print $5}'|cut -d: -f1 -s |cut -f1,2 -d'.'|sed 's/$/.0.0/'|sort|uniq -c|sort -nk1 -r | awk '{if($1 >= 1) {print $2}}'
```
```
统计数量修改获取，iptables可直接按照上面来进行添加。
```
![](media/15894431509248/15895091620296.jpg)

## 

