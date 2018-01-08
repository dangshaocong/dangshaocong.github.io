---
title: python启动定时任务
date: 2017-10-31 19:36:30
tags: python启动定时任务
---
### python启动定时任务

# 1.time模块
`time.sleep(n)` 
例如下面的例子
```
  def work(n):             - 每隔n 秒 输出 1到10之间的一个数
    for i in range(10):
        print i
        time.sleep(n)
```
上面的实例是阻塞的，在sleep的时间内程序一直堵塞 
详情请参考官方文档-----[time.sleep](https://docs.python.org/2/library/time.html?sleep#time.sleep)
# 2.sched 模块
```
  1.导入sched模块
  import sched
----------------------------------------------------------------------------------
  2.创建scheduler对象
  s = sched.scheduler(time.time, time.sleep)
  - time.time:返回时间戳的函数
  - time.sleep:可以在定时未到达之前阻塞
------------------------------------------------------------------------------------
  3.定义要执行的任务
  def worker(n):
        pass
-------------------------------------------------------------------------------------
  4.将任务添加到scheduler的盒子中
  s.enter(delay,priority,action,arguments)
  - delay:int /float型的表示多少秒后执行这个action任务
  - priority:优先级表示当多个任务同时在一个时刻将执行优先执行那个任务
    0优先级最高，数字越小优先级越高
  - action: 执行的任务在上面的例子中也就是函数名worker
  - arguments:参数列表以元组的形式如：(n,)
    如果没有参数传入直接传空括号()
--------------------------------------------------------------------------------------
  5.运行任务
  s.run()
```
在多线程环境中由于线程全局锁安全，一个任务没结束，就要等待也是阻塞的详细请查看官方库----[sched](https://docs.python.org/2/library/sched.html)

# 3.threading.Timer()
为了解决上面的阻塞问题，再多线程的环境中能够并发执行
```
  1.导入模块
  from threading import Timer
----------------------------------------------------------------------------------------
  2.定义要执行的任务
  def work(arg):
        pass
----------------------------------------------------------------------------------------
  3.启动执行
  Timer(delay, work, (arg)).start()
  - 不需要区分优先级可以同时执行任务delay相同时就同时执行任务
  -  delay:int /float型的表示多少秒后执行这个work任务
  -  work: 执行任务的方法名字
  -  arg:参数列表元祖(arg,)如果没有就是()
```
详情请参考官方文档：[threading.Timer](https://docs.python.org/2/library/sched.html?highlight=threading%20timer)

# 4.更加高级的任务调度框架 apscheduler
   官方文档   [查看](http://apscheduler.readthedocs.io/en/latest/)
``` 
  1.导入模块
   from apscheduler.schedulers.blocking import BlockingScheduler

  2.初始化一个任务实例
   sched = BlockingScheduler()

  3.添加作业任务
  sched.add_job(my_job, 'interval', seconds=5)
 - my_job：作业任务
 -‘ interval ’  ‘cron ’等等

 4.启动任务
   sched.start()

```
