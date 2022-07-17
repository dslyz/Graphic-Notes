# 搜索查找类

## 1、find指令

find指令将从指定目录向下递归地遍历其各个子目录，将满足条件的文件或者目录显示在终端。

**基本语法：**

find  [搜索范围]  [选项]

**选项说明:**

![image-20220228180938865](day07.assets/image-20220228180938865.png)

**应用实例：**

案例1：按文件名：根据名称查找/home 目录下的hello.txt 文件

```
find /home -name hello.txt
```

案例2:按拥有者：查找/opt目录下，用户名称为nobody的文件

```
find /opt -user nobody
```

案例3：查找整个Linux系统下大于200M的文件(+n 大于n        -n 小于n     n 等于n, 单位有k,M,G)

```
find / -size +200M
```



## 2、locate指令

locat指令可以快速定位文件路径。locate指令利用事先建立的系统中所有文件名称及路径的locate数据库实现快速定位给定的文件。locate指令无需遍历整个文件系统，查询速度较快。为了保证查询结果的准确度，管理员必须定期更新locate时刻。

**基本语法：**

locate 搜索文件

**特别说明：**

由于locate指令基于数据库进行查询，所以在第一次运行前，必须使用updatedb指令创建locate数据库

**应用实例：**

案例：请使用locate指令快速定位hello.txt文件所在目录

```
updatedb
locate hello.txt
```

**which指令**：可以查看某个指令在哪个目录下，比如ls指令在哪个目录

```
which ls           #查看ls指令在哪个目录下
which man          #查看man指令在哪个目录下
```



## 3、grep指令和管道符号 |

grep 过滤查找，管道符 ”|“，表示将前一个命令的处理结果输出传递给后面的命令处理。

**基本语法：**

grep [选项] 查找内容 源文件

**常用选项：**

![image-20220228182601055](day07.assets/image-20220228182601055.png)

**应用实例：**

案例1：请在hello.txt文件中，查找"yes" 所在行，并且显示行号

```
cat /home/hello.txt | grep -n "yes"
grep -n "yes" /home/hello.txt
```



# 压缩和解压类

## 1、gzip/gunzip指令

gzip用于压缩文件，gunzip用于解压文件

**基本语法：**

gzip  文件           （功能描述：压缩文件，只能将文件压缩为*.gz文件）

gunzip 文件.gz     (功能描述：解压缩文件命令)

**应用实例：**

案例1：gzip压缩，将/home下的hello.txt文件进行压缩

```
gzip /home/hello.txt
```

案例2：gunzip解压缩，将/home下的hello.txt.gz文件进行解压缩

```
gunzip /home/hello.txt.gz
```



## 2、zip和unzip指令

zip 用于压缩文件， unzip 用于解压文件，这个在项目打包发布中很有用。

**基本语法：**

zip  [选项]  XXX.zip 将要压缩的内容                (功能描述：压缩文件和目录的命令)

unzip  [选项]  要解压的路径  XXX.zip              (功能描述：解压缩文件)

**zip常用选项：**

-r : 递归压缩，即压缩目录

**unzip常用选项**

-d <目录> ： 指定解压后文件的存放目录

**应用实例：**

案例1： 将/home 下的所有文件/文件夹 进行压缩成 myhome.zip

```
zip -r myhome.zip /home/        #将home目录及其包含的文件和子文件夹都压缩
```

案例2：将 myhome.zip 解压到/opt/tmp目录下

```
mkdir /opt/tmp
unzip -d /opt/tmp /home/myhome.zip
```





## 3、tar指令

**基本语法：**

tar [选项] XXX.tar.gz  打包的内容            （功能描述：打包目录，压缩后的文件格式.tar.gz）

**选项说明：**

![image-20220228184739573](day07.assets/image-20220228184739573.png)

**应用实例：**

案例1：压缩多个文件，将/home/pig.txt 和 /home/cat.txt 压缩成 pc.tar.gz

```
tar -zcvf pc.tar.gz /home/pig.txt /home/cat.txt
```

案例2：将/home的文件夹压缩成 myhome.tar.gz

```
tar -zcvf myhome.tar.gz /home/
```

案例3：将pc.tar.gz 加压到当前目录

```
tar -zxvf pc.tar.gz
```

案例4：将myhome.tar.gz 解压到 /opt/tmp2 目录下

```
mkdir /opt/tmp2
tar -zxvf /home/myhome.tar.gz -C /opt/tmp2      # -C代表要解压到的文件路径
```

