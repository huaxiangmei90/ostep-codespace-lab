# 结果概述
## Q1
- 结果:
```
python3 ./ext/ostep-homework/cpu-sched/scheduler.py -l 200,200,200 -p FIFO
FIFO： 
  响应时间（Response Time） ：（ 0 + 200 + 400 ）/ 3 = 200 
  周转时间（Turnaround Time） ： （ 200 + 400 + 600 ）/ 3 = 400

python3 ./ext/ostep-homework/cpu-sched/scheduler.py -l 200,200,200 -p SJF
SJF：
  响应时间（Response Time） ：（ 0 + 200 + 400 ）/ 3 = 200 
  周转时间（Turnaround Time） ： （ 200 + 400 + 600 ）/ 3 = 400
```

## Q2
- 结果:
```
python3 ./ext/ostep-homework/cpu-sched/scheduler.py -l 100,200,300 -p FIFO
FIFO： 
  响应时间（Response Time） ：（ 0 + 100 + 300 ）/ 3 ≈ 133.3
  周转时间（Turnaround Time） ： （ 100 + 300 + 600 ）/ 3 ≈ 333.3
python3 ./ext/ostep-homework/cpu-sched/scheduler.py -l 300,200,100 -p FIFO
FIFO： 
  响应时间（Response Time） ：（ 0 + 300 + 500 ）/ 3 ≈ 266.66
  周转时间（Turnaround Time） ： （ 300 + 500 + 600 ）/ 3 ≈ 466.66

python3 ./ext/ostep-homework/cpu-sched/scheduler.py -l 100,200,300 -p SJF
SJF：
  响应时间（Response Time） ：（ 0 + 100 + 300 ）/ 3 ≈ 133.3 
  周转时间（Turnaround Time） ： （ 100 + 300 + 600 ）/ 3 ≈ 333.3
python3 ./ext/ostep-homework/cpu-sched/scheduler.py -l 300,200,100 -p SJF
SJF：
  响应时间（Response Time） ：（ 0 + 100 + 300 ）/ 3 ≈ 133.3 
  周转时间（Turnaround Time） ： （ 100 + 300 + 600 ）/ 3 ≈ 333.3
```

## Q3
- 结果:
```
python3 ./ext/ostep-homework/cpu-sched/scheduler.py -l 100,200,300 -p RR -q 1 
RR：
  响应时间（Response Time） ：（ 0 + 1 + 2 ）/ 3 = 1 
  周转时间（Turnaround Time） ： （ 300 + 500 + 600 ）/ 3 ≈ 466.66
```

## Q4
- 结果:
```
对于每一个作业运行相同的时间, 所有的作业同时到达, 或作业先后顺序本身就是按照工作时间从小到大排序的工作负载
```

## Q5
- 结果:
```
RR的时间片长度大于等于所有作业中最长的运行时间，且作业按运行时间从小到大依次到达。
```

## Q6
- 结果:
```
随着工作长度的增加，SJF调度的响应时间会也会随着工作长度的增长线性增长. 
```

## Q7
- 结果:
```
随着量子长度的增加，RR调度的响应时间会随着量子长度的增长而增长.
假设N个作业同时到达且都需至少一个时间片时，
N：就绪队列中的作业数, Q：时间片长度
最坏响应时间可近似为 R = (N − 1) × Q
```
