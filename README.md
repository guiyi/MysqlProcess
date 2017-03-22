
# Mysql压力测试需求分析

# 目录
## 一 背景（前言） 	2
## 二 Mysql 压力测试体系及包括的执行参数 	2
2.1压力测试 Process.py脚本 	2
2.2单逻辑	3
2.3全部操作	3
2. 4方式	3
2. 5开启进程数	4
## 三 执行命令及解释 	4
## 四 执行展示 	4



  
版本号	公司	组别	日期
Process.py 1.0	51job	System	2013.01.15
			
			





### 一、	背景（前言）
摘要： “前程无忧”(Nasdaq:JOBS) 

关键字 ：Mysql，数据库，压力测试，多进程，CPU利用率，随机数

### 二、	Mysql 压力测试体系及包括的执行参数

2.1压力测试 Process.py脚本
该脚本从单逻辑（含单个select操作，insert操作，update操作，delete操作）和全部操作（select 占70%操作，insert 占15%操作，update 占10%操作，delete 5%操作）两种逻辑来实现对Linux服务器上的Mysql数据库可选择方式（含 S：次数，T：时间（秒））和开启进程数（默认开启当前空闲最大的CPU，使用 –n –num 值可控开启进程数）来测试当前数据库执行的效率。 

可参考：图一 Mysql压力测试流程

 
图一 Mysql压力测试流程

2.2单逻辑
执行脚本时，可参考 A. Mysql压力测试执行参数
选择逻辑       -a, --all  为single 时；
选择单逻辑操作 -o, --operation 时有 ：
select操作；
insert操作；
update操作；
delete操作；
均可供选择；


2.3全部操作
执行脚本时，可参考 A. Mysql压力测试执行参数
选择逻辑       -a, --all  为all 时；
选择全部操作 -o, --operation 时 ，无需赋值；

用select统计随机数与数据库表ID匹配个数。（约占70%）；
用insert统计随机数与数据库表ID匹配个数。（约占15%）；
用update统计随机数与数据库表ID匹配个数。（约占10%）；
用delete统计随机数与数据库表ID匹配个数。（约占5%）；

2.4方式
单逻辑 有两种方式来测试mysql的执行效率 ；分别从次数 S 或 时间 T（秒）；
全部操作  仅从时间 T（角度） 来测试；



2.5开启进程数
该脚本，默认获取当前服务器最大空闲的CPU进程；
也可以从 -n, --num 来开启当前执行进程；

A. Mysql压力测试执行参数
python Process.py --help
usage: Process.py [-h] [-a one] [-o two] [-w three] [-v four] [-n five]

optional arguments:
1.	  -h, --help            show this help message and exit
2.	  -a one, --all one     all, single
3.	  -o two, --operation two
                        The pressure test operation,Have:select or update or
                        delete
4.	  -w three, --way three
                        The pressure test way,S|s means According to the
                        number of execution ; T|t According to the time/second
                        of execution
5.	  -v four, --values four
                        The pressure test way value
6.	  -n five, --num five   The number of opening process,The default read the
                        current maximum idle process



### 三、	执行命令及解释
python Process.py  -a single -o select -w S -v 5000
python Process.py  - a single -o select -w T -v 2 -n 6
python Process.py  -a single -o select -w T -v 2 -n 8
python Process.py  -a all  -w T -v 1 -n 2
python Process.py  -a all  -w T -v 1

### 四、	执行展示
1.执行 脚本 选择 单逻辑 select操作；按 次数 S  5000 个随机数；开启6个进程

 [zouhd@Mslave Fans]$ python Process.py -a single -o select -w S -v 5000 -n 6
Process ID: 13529  Time consuming: 0.13  Treatment number : 833 
Process ID: 13531  Time consuming: 0.13  Treatment number : 833 
Process ID: 13528  Time consuming: 0.18  Treatment number : 833 
Process ID: 13532  Time consuming: 0.16  Treatment number : 833 
Process ID: 13533  Time consuming: 0.16  Treatment number : 833 
Process ID: 13530  Time consuming: 0.16  Treatment number : 833 
结果可看到：开启6个进程，消耗时间，及执行次数；


2.执行 脚本 选择 单逻辑 select操作；按 时间 T  2秒 ；开启8个进程

[zouhd@Mslave Fans]$ python Process.py -a single -o select -w T -v 2 -n 8
Process ID: 15009  Time consuming: 0.45  Treatment number : 2676 
Process ID: 15007  Time consuming: 0.44  Treatment number : 2782 
Process ID: 15008  Time consuming: 0.49  Treatment number : 2436 
Process ID: 15011  Time consuming: 0.49  Treatment number : 2412 
Process ID: 15013  Time consuming: 0.43  Treatment number : 2657 
Process ID: 15010  Time consuming: 0.53  Treatment number : 2580 
Process ID: 15012  Time consuming: 0.55  Treatment number : 2447 
Process ID: 15006  Time consuming: 0.47  Treatment number : 2603 
结果可看到：开启8个进程，消耗时间，及执行次数；


3. 执行 脚本 选择 全部操作；按 时间 T  1秒 ；开启默认进程

[zouhd@Mslave Fans]$ python Process.py -a all  -w T -v 1 
Process ID: 16441  Time consuming: 0.1  Select number : 636  Update number : 22  Insert number : 61  Delete number : 21 
Process ID: 16447  Time consuming: 0.09  Select number : 591  Update number : 19  Insert number : 45  Delete number : 19 
Process ID: 16458  Time consuming: 0.08  Select number : 561  Update number : 23  Insert number : 44  Delete number : 26 
Process ID: 16443  Time consuming: 0.09  Select number : 544  Update number : 30  Insert number : 45  Delete number : 21 
Process ID: 16439  Time consuming: 0.08  Select number : 626  Update number : 20  Insert number : 40  Delete number : 26 
Process ID: 16451  Time consuming: 0.09  Select number : 621  Update number : 22  Insert number : 48  Delete number : 21 
Process ID: 16449  Time consuming: 0.09  Select number : 526  Update number : 22  Insert number : 34  Delete number : 30 
Process ID: 16445  Time consuming: 0.09  Select number : 545  Update number : 24  Insert number : 30  Delete number : 25 
Process ID: 16457  Time consuming: 0.08  Select number : 595  Update number : 27  Insert number : 37  Delete number : 17 
Process ID: 16460  Time consuming: 0.11  Select number : 590  Update number : 19  Insert number : 47  Delete number : 20 
Process ID: 16452  Time consuming: 0.08  Select number : 545  Update number : 24  Insert number : 48  Delete number : 21 
Process ID: 16444  Time consuming: 0.09  Select number : 695  Update number : 16  Insert number : 46  Delete number : 21 
Process ID: 16461  Time consuming: 0.08  Select number : 622  Update number : 12  Insert number : 40  Delete number : 24 
Process ID: 16446  Time consuming: 0.08  Select number : 603  Update number : 11  Insert number : 54  Delete number : 18 
Process ID: 16455  Time consuming: 0.08  Select number : 596  Update number : 14  Insert number : 47  Delete number : 19 
Process ID: 16442  Time consuming: 0.09  Select number : 552  Update number : 24  Insert number : 32  Delete number : 30 
Process ID: 16453  Time consuming: 0.1  Select number : 616  Update number : 19  Insert number : 41  Delete number : 20 
Process ID: 16454  Time consuming: 0.07  Select number : 641  Update number : 19  Insert number : 43  Delete number : 15 
Process ID: 16440  Time consuming: 0.06  Select number : 567  Update number : 18  Insert number : 47  Delete number : 20 
Process ID: 16450  Time consuming: 0.08  Select number : 576  Update number : 24  Insert number : 48  Delete number : 20 
Process ID: 16456  Time consuming: 0.09  Select number : 566  Update number : 17  Insert number : 31  Delete number : 20 
Process ID: 16448  Time consuming: 0.09  Select number : 591  Update number : 16  Insert number : 33  Delete number : 22 
Process ID: 16438  Time consuming: 0.09  Select number : 594  Update number : 23  Insert number : 37  Delete number : 20 
Process ID: 16459  Time consuming: 0.09  Select number : 567  Update number : 21  Insert number : 42  Delete number : 16

结果可看到：开启24个进程，消耗时间，及Select，Update，Insert，Delete 各执行次数；




                                                                                        Adair.zou.2013.02.21
