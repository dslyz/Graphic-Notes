# 开机、重启和用户注销登录

## 一、关机&重启命令

### 1、基本介绍

```
1. shutdown -h now              立刻进行关机
2. shutdown -h 1                一分钟后关机
3. shutdown -r now              现在重新启动计算机
4. halt                         关机
5. reboot                       现在重新启动计算机
6. sync                         把内存中的数据同步到磁盘
```

 

### 2、注意细节

1、不管是重启系统还是关闭系统，首先要运行的sync命令，把内存中的数据写道磁盘中

2、目前的shutdown/reboot/halt 等命令均已经在关机前进行了sync，但最好还是执行一次sync，小心驶得万年船。

## 二、用户登录和注销

### 1、基本介绍

1、登录时尽量少用root账号登录，因为它是管理员账号，最大的权限，为避免操作失误，可以使用普通用户登录，登录后再使用“su - 用户名”命令来切换成系统管理员。

```
su - root            切换到root用户
```

2、在提示符下输入logout即可注销用户



### 2、使用细节

1、logout注销指令在图形运行级别无效，在**运行级别3以下有效**。

2、运行级别概念

![img](day03.assets/images2018.cnblogs.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg)