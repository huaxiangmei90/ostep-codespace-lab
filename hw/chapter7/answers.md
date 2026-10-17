# OSTEP Ch.7 Homework Answers

## Q1
- Prediction / 预测:
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
- Reasoning / 理由:
```
FIFO： 先进先出调度
SJF： 最短任务优先调度
因为3个作业的运行时长相同， 所以两种调度方式的响应时间和周转时间一致
```
- Verified result / 验证结果:
```
验证结果和预测相同
```
- Analysis / 分析:
```
分析结果和理由相同
```

## Q2
- Prediction / 预测:
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
- Reasoning / 理由:
```
FIFO： 先进先出调度
SJF： 最短任务优先调度
因为3个作业的排序方式就是按照最短任务优先的方式， 所以两种调度方式的响应时间和周转时间一致;
但如果修改作业排序为300,200,100, FIFO调度的响应时间和周转时间相比SJF调度花费更多时间.
```
- Verified result / 验证结果:
```
验证结果和预测相同
```
- Analysis / 分析:
```
分析结果和理由相同
```


## Q3
- Prediction / 预测:
```
python3 ./ext/ostep-homework/cpu-sched/scheduler.py -l 100,200,300 -p RR -q 1 
RR：
  响应时间（Response Time） ：（ 0 + 1 + 2 ）/ 3 = 1 
  周转时间（Turnaround Time） ： （ 300 + 500 + 600 ）/ 3 ≈ 466.66
```
- Reasoning / 理由:
```
RR: 轮转调度
每隔1单位时间, CPU就转到下一个作业运行, 所以响应时间分别为1,2,3; 而周转时间为300,500,600
```
- Verified result / 验证结果:
```
验证结果和预测相同
```
- Analysis / 分析:
```
分析结果和理由相同
```


## Q4
- Prediction / 预测:
```
对于每一个作业运行相同的时间, 所有的作业同时到达, 或作业先后顺序本身就是按照工作时间从小到大排序的工作负载
```
- Reasoning / 理由:
```
因为FIFO调度和SJF调度的区别就是SJF调度会将同时到达的作业按照工作时间从小到大排序执行, 如果FIFO调度中作业先后顺序本身就是按照工作时间从小到大排序的工作负载, 呢其实就和SJF调度一样了
```
- Verified result / 验证结果:
```
验证结果和预测相同
```
- Analysis / 分析:
```
分析结果和理由相同
```

## Q5
- Prediction / 预测:
```
RR的时间片长度大于等于所有作业中最长的运行时间，且作业按运行时间从小到大依次到达。
```
- Reasoning / 理由:
```
当RR的时间片足够大时，不会发生抢占。且作业按运行时间递增顺序到达时，RR的执行顺序与SJF一致。
```
- Verified result / 验证结果:
```
验证结果和预测相同
```
- Analysis / 分析:
```
分析结果和理由相同
```

## Q6
- Prediction / 预测:
```
python3 ./ext/ostep-homework/cpu-sched/scheduler.py -l 100,200,300 -p SJF
SJF：
  响应时间（Response Time） ：（ 0 + 100 + 300 ）/ 3 ≈ 133.33 
  周转时间（Turnaround Time） ： （ 100 + 300 + 600 ）/ 3 ≈ 333.33
python3 ./ext/ostep-homework/cpu-sched/scheduler.py -l 200,300,400 -p SJF
SJF：
  响应时间（Response Time） ：（ 0 + 200 + 500 ）/ 3 ≈ 233.33 
  周转时间（Turnaround Time） ： （ 200 + 500 + 900 ）/ 3 ≈ 533.33
python3 ./ext/ostep-homework/cpu-sched/scheduler.py -l 300,400,500 -p SJF
SJF：
  响应时间（Response Time） ：（ 0 + 300 + 700 ）/ 3 ≈ 333.33 
  周转时间（Turnaround Time） ： （ 300 + 700 + 1200 ）/ 3 ≈ 733.33

随着工作长度的增加，SJF调度的响应时间会也会随着工作长度的增长线性增长. 
```
- Reasoning / 理由:
```
SJF调度是非抢占式调度：一旦一个作业开始运行，就会一直跑到结束。
如果所有作业都在同一时间到达，SJF调度会按工作时间从小到大执行。最短作业响应时间通常是0，第二个作业要等第一个跑完，第三个要等前两个跑完，所以越靠后的作业，响应时间越大。
```
- Verified result / 验证结果:
```
验证结果和预测相同
```
- Analysis / 分析:
```
分析结果和理由相同
```

## Q7
- Prediction / 预测:
```
随着量子长度的增加，RR调度的响应时间会随着量子长度的增长而增长.
假设N个作业同时到达且都需至少一个时间片时，
N：就绪队列中的作业数, Q：时间片长度
最坏响应时间可近似为 R = (N − 1) × Q
```
- Reasoning / 理由:
```
如果所有作业在时刻0同时到达,每个作业至少需要运行一个时间片
则最坏情况是排在队列最后一个的作业：
例如 N = 5、Q = 10：
R_max = (5 − 1) × 10 = 40
也就是说，最后一个作业要等前面 4 个作业各跑一个时间片，才能第一次获得 CPU。
```
- Verified result / 验证结果:
```
验证结果和预测相同
```
- Analysis / 分析:
```
分析结果和理由相同
```