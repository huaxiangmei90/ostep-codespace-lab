# OSTEP Ch.4 Homework Answers

## Q1
- Prediction / 预测:
```
Time   PID: 0     PID: 1     CPU     IOs
  1     RUN:cpu    READY      1
  2     RUN:cpu    READY      1
  3     RUN:cpu    READY      1
  4     RUN:cpu    READY      1
  5     RUN:cpu    READY      1
  6     DONE       RUN:cpu    1
  7     DONE       RUN:cpu    1
  8     DONE       RUN:cpu    1
  9     DONE       RUN:cpu    1
 10     DONE       RUN:cpu    1
```
- Reasoning / 理由:
```
程序命令-l 5:100,5:100 表示创建两个进程, 每个进程各有 5 条指令, 且每条指令为 CPU 指令的概率是 100%
也就是两个进程, 进程0执行5个cpu指令, 进程1再执行5个cpu指令, 一共10个tick, 每个tick都在执行cpu指令 
```
- Verified result / 验证结果:
- Analysis / 分析:
```
1. 缺少总时间、CPU利用率
Stats: Total Time 10
Stats: CPU Busy 10 (100.00%)
Stats: IO Busy  0 (0.00%)
```

## Q2
- Prediction / 预测:
```
Time   PID: 0     PID: 1        CPU     IOs
  1    RUN:cpu    READY          1
  2    RUN:cpu    READY          1
  3    RUN:cpu    READY          1
  4    RUN:cpu    READY          1
  5    DONE       RUN:io         1
  6    DONE       BLOCKED               1
  7    DONE       BLOCKED               1
  8    DONE       BLOCKED               1
  9    DONE       BLOCKED               1
  10   DONE       BLOCKED               1
  11   DONE       RUN:io_done    1
```
- Reasoning / 理由:
```
程序命令-l 4:100,1:0
进程0先执行4个时间单位的cpu指令; 之后进程1先执行调用cpu发起I/O, 再执行I/O, 导致cpu阻塞, 最后调用cpu结束I/O 
```
- Verified result / 验证结果:
- Analysis / 分析:
```
1. 缺少总时间、CPU利用率
Stats: Total Time 11
Stats: CPU Busy 6 (54.55%)
Stats: IO Busy  5 (45.45%)
```

## Q3
- Prediction / 预测:
```
Time   PID: 0     PID: 1        CPU     IOs
  1    DONE       RUN:io         1
  2    DONE       BLOCKED               1
  3    DONE       BLOCKED               1
  4    DONE       BLOCKED               1
  5    DONE       BLOCKED               1
  6    DONE       BLOCKED               1
  7    DONE       RUN:io_done    1
  8    RUN:cpu    READY          1
  9    RUN:cpu    READY          1
  10   RUN:cpu    READY          1
  11   RUN:cpu    READY          1
```
- Reasoning / 理由:
```
程序命令: -l 1:0,4:100
不重要, 只是交换了进程的执行顺序, 其他相同
```
- Verified result / 验证结果:
- Analysis / 分析:
```
1. 缺少总时间、CPU利用率
Stats: Total Time 7
Stats: CPU Busy 6 (85.71%)
Stats: IO Busy  5 (71.43%)
2. 对于指令运行顺序理解错误, 应该是先执行I/O指令, 再执行cpu指令
```

## Q4
- Prediction / 预测:
```
Time   PID: 0        PID: 1    CPU     IOs
  1    RUN:io        READY     1          
  2    BLOCKED       READY             1
  3    BLOCKED       READY             1
  4    BLOCKED       READY             1
  5    BLOCKED       READY             1
  6    BLOCKED       READY             1
  7*   RUN:io_done   READY     1 
  8    DONE          RUN:cpu   1 
  9    DONE          RUN:cpu   1 
 10    DONE          RUN:cpu   1 
 11    DONE          RUN:cpu   1 
```
- Reasoning / 理由:
```
加上 -S SWITCH_ON_END 后, 进程0发起I/O时不会切换到进程1, 而是等进程0整个结束后才让进程1运行.
```
- Verified result / 验证结果:
- Analysis / 分析:
```
1. 缺少总时间、CPU利用率
Stats: Total Time 11
Stats: CPU Busy 6 (54.55%)
Stats: IO Busy  5 (45.45%)
```

## Q5
- Prediction / 预测:
```
Time   PID: 0        PID: 1        CPU     IOs
  1    RUN:io        READY         1          
  2    BLOCKED       RUN:cpu       1       1
  3    BLOCKED       RUN:cpu       1       1
  4    BLOCKED       RUN:cpu       1       1
  5    BLOCKED       RUN:cpu       1       1
  6    BLOCKED       DONE                  1
  7*   RUN:io_done   DONE          1  
  ```
- Reasoning / 理由:
```
当cpu在进程0执行完发起I/O指令后, 转而执行进程1的cpu指令, 执行完成后再执行进程0的I/O终止指令
```
- Verified result / 验证结果:
- Analysis / 分析:
```
1. 缺少总时间、CPU利用率
Stats: Total Time 7
Stats: CPU Busy 6 (85.71%)
Stats: IO Busy  5 (71.43%)
```

## Q6
- Prediction / 预测:
```
Time   PID: 0        PID: 1        PID: 2        PID: 3        CPU     IOs
  1    RUN:io        READY         READY         READY         1          
  2    BLOCKED       RUN:cpu       READY         READY         1       1
  3    BLOCKED       RUN:cpu       READY         READY         1       1
  4    BLOCKED       RUN:cpu       READY         READY         1       1
  5    BLOCKED       RUN:cpu       READY         READY         1       1
  6    BLOCKED       RUN:cpu       READY         READY         1       1
  7*   READY         DONE          RUN:cpu       READY         1          
  8    READY         DONE          RUN:cpu       READY         1          
  9    READY         DONE          RUN:cpu       READY         1          
 10    READY         DONE          RUN:cpu       READY         1          
 11    READY         DONE          RUN:cpu       READY         1          
 12    READY         DONE          DONE          RUN:cpu       1          
 13    READY         DONE          DONE          RUN:cpu       1          
 14    READY         DONE          DONE          RUN:cpu       1          
 15    READY         DONE          DONE          RUN:cpu       1          
 16    READY         DONE          DONE          RUN:cpu       1          
 17    RUN:io_done   DONE          DONE          DONE          1          
 18    RUN:io        DONE          DONE          DONE          1          
 19    BLOCKED       DONE          DONE          DONE                  1
 20    BLOCKED       DONE          DONE          DONE                  1
 21    BLOCKED       DONE          DONE          DONE                  1
 22    BLOCKED       DONE          DONE          DONE                  1
 23    BLOCKED       DONE          DONE          DONE                  1
 24*   RUN:io_done   DONE          DONE          DONE          1          
 25    RUN:io        DONE          DONE          DONE          1          
 26    BLOCKED       DONE          DONE          DONE                  1
 27    BLOCKED       DONE          DONE          DONE                  1
 28    BLOCKED       DONE          DONE          DONE                  1
 29    BLOCKED       DONE          DONE          DONE                  1
 30    BLOCKED       DONE          DONE          DONE                  1
 31*   RUN:io_done   DONE          DONE          DONE          1
```
- Reasoning / 理由:
```
进程0在执行I/O指令后, cpu执行进程1,进程2,进程3的指令, 执行完成后才继续执行进程0的I/O指令
```
- Verified result / 验证结果:
- Analysis / 分析:
```
1. 缺少总时间、CPU利用率
Stats: Total Time 31
Stats: CPU Busy 21 (67.74%)
Stats: IO Busy  15 (48.39%)
```

## Q7
- Prediction / 预测:
```
Time   PID: 0        PID: 1        PID: 2        PID: 3        CPU     IOs
  1    RUN:io        READY         READY         READY         1          
  2    BLOCKED       RUN:cpu       READY         READY         1       1
  3    BLOCKED       RUN:cpu       READY         READY         1       1
  4    BLOCKED       RUN:cpu       READY         READY         1       1
  5    BLOCKED       RUN:cpu       READY         READY         1       1
  6    BLOCKED       RUN:cpu       READY         READY         1       1
  7*   RUN:io_done   DONE          READY         READY         1
  8    RUN:io        DONE          READY         READY         1
  9    BLOCKED       DONE          RUN:cpu       READY         1       1
 10    BLOCKED       DONE          RUN:cpu       READY         1       1
 11    BLOCKED       DONE          RUN:cpu       READY         1       1
 12    BLOCKED       DONE          RUN:cpu       READY         1       1
 13    BLOCKED       DONE          RUN:cpu       READY         1       1
 14*   RUN:io_done   DONE          DONE          READY         1
 15    RUN:io        DONE          DONE          READY         1
 16    BLOCKED       DONE          DONE          RUN:cpu       1       1
 17    BLOCKED       DONE          DONE          RUN:cpu       1       1
 18    BLOCKED       DONE          DONE          RUN:cpu       1       1
 19    BLOCKED       DONE          DONE          RUN:cpu       1       1
 20    BLOCKED       DONE          DONE          RUN:cpu       1       1
 21*   RUN:io_done   DONE          DONE          DONE          1 
```
- Reasoning / 理由:
```
区别是进程0中的I/O指令在完成一个后, 就立即进行下一个, 而进程1,进程2,进程3则在I/O指令运行的间隙执行cpu指令
这样可以充分利用I/O指令执行时的等待时间, 提高整体的效率
```
- Verified result / 验证结果:
- Analysis / 分析:
```
1. 缺少总时间、CPU利用率
Stats: Total Time 21
Stats: CPU Busy 21 (100.00%)
Stats: IO Busy  15 (71.43%)
```

## Q8
- Prediction / 预测:
```
python3 process-run.py -s 1 -l 3:50,3:50
Time   PID: 0        PID: 1        CPU     IOs
  1    RUN:cpu       READY         1          
  2    RUN:io        READY         1          
  3    BLOCKED       RUN:cpu       1       1
  4    BLOCKED       RUN:cpu       1       1
  5    BLOCKED       RUN:cpu       1       1
  6    BLOCKED       DONE                  1
  7    BLOCKED       DONE                  1
  8*   RUN:io_done   DONE          1          
  9    RUN:io        DONE          1          
 10    BLOCKED       DONE                  1
 11    BLOCKED       DONE                  1
 12    BLOCKED       DONE                  1
 13    BLOCKED       DONE                  1
 14    BLOCKED       DONE                  1
 15*   RUN:io_done   DONE          1 

python3 process-run.py -s 1 -l 3:50,3:50 -I IO_RUN_IMMEDIATE
Time   PID: 0        PID: 1        CPU     IOs
  1    RUN:cpu       READY         1          
  2    RUN:io        READY         1          
  3    BLOCKED       RUN:cpu       1       1
  4    BLOCKED       RUN:cpu       1       1
  5    BLOCKED       RUN:cpu       1       1
  6    BLOCKED       DONE                  1
  7    BLOCKED       DONE                  1
  8*   RUN:io_done   DONE          1          
  9    RUN:io        DONE          1          
 10    BLOCKED       DONE                  1
 11    BLOCKED       DONE                  1
 12    BLOCKED       DONE                  1
 13    BLOCKED       DONE                  1
 14    BLOCKED       DONE                  1
 15*   RUN:io_done   DONE          1 

 python3 process-run.py -s 1 -l 3:50,3:50 -S SWITCH_ON_END
 Time   PID: 0        PID: 1        CPU     IOs
   1    RUN:cpu       READY         1          
   2    RUN:io        READY         1          
   3    BLOCKED       READY                 1
   4    BLOCKED       READY                 1
   5    BLOCKED       READY                 1
   6    BLOCKED       READY                 1
   7    BLOCKED       READY                 1
   8*   RUN:io_done   READY         1          
   9    RUN:io        READY         1          
  10    BLOCKED       READY                 1
  11    BLOCKED       READY                 1
  12    BLOCKED       READY                 1
  13    BLOCKED       READY                 1
  14    BLOCKED       READY                 1
  15*   RUN:io_done   READY         1          
  16    DONE          RUN:cpu       1          
  17    DONE          RUN:cpu       1          
  18    DONE          RUN:cpu       1

python3 process-run.py -s 2 -l 3:50,3:50
Time   PID: 0        PID: 1        CPU     IOs
  1    RUN:io        READY         1          
  2    BLOCKED       RUN:cpu       1       1
  3    BLOCKED       RUN:io        1       1
  4    BLOCKED       BLOCKED               2
  5    BLOCKED       BLOCKED               2
  6    BLOCKED       BLOCKED               2
  7*   RUN:io_done   BLOCKED       1       1
  8    RUN:io        BLOCKED       1       1
  9*   BLOCKED       RUN:io_done   1       1
 10    BLOCKED       RUN:io        1       1
 11    BLOCKED       BLOCKED               2
 12    BLOCKED       BLOCKED               2
 13    BLOCKED       BLOCKED               2
 14*   RUN:io_done   BLOCKED       1       1
 15    RUN:cpu       BLOCKED       1       1
 16*   DONE          RUN:io_done   1

python3 process-run.py -s 2 -l 3:50,3:50 -I IO_RUN_IMMEDIATE
Time   PID: 0        PID: 1        CPU     IOs
  1    RUN:io        READY         1          
  2    BLOCKED       RUN:cpu       1      1
  3    BLOCKED       RUN:io        1      1
  4    BLOCKED       BLOCKED              2
  5    BLOCKED       BLOCKED              2
  6    BLOCKED       BLOCKED              2
  7*   RUN:io_done   BLOCKED       1      1
  8    RUN:io        BLOCKED       1      1
  9*   BLOCKED       RUN:io_done   1      1
 10    BLOCKED       RUN:io        1      1
 11    BLOCKED       BLOCKED              2
 12    BLOCKED       BLOCKED              2
 13    BLOCKED       BLOCKED              2
 14*   RUN:io_done   BLOCKED       1      1
 15    RUN:cpu       BLOCKED       1      1
 16*   DONE          RUN:io_done   1

python3 process-run.py -s 2 -l 3:50,3:50 -S SWITCH_ON_END
Time   PID: 0        PID: 1        CPU     IOs
  1    RUN:io        READY         1          
  2    BLOCKED       READY                 1
  3    BLOCKED       READY                 1
  4    BLOCKED       READY                 1
  5    BLOCKED       READY                 1
  6    BLOCKED       READY                 1
  7*   RUN:io_done   READY         1          
  8    RUN:io        READY         1          
  9    BLOCKED       READY                 1
 10    BLOCKED       READY                 1
 11    BLOCKED       READY                 1
 12    BLOCKED       READY                 1
 13    BLOCKED       READY                 1
 14*   RUN:io_done   READY         1          
 15    RUN:cpu       READY         1          
 16    DONE          RUN:cpu       1          
 17    DONE          RUN:io        1          
 18    DONE          BLOCKED               1
 19    DONE          BLOCKED               1
 20    DONE          BLOCKED               1
 21    DONE          BLOCKED               1
 22    DONE          BLOCKED               1
 23*   DONE          RUN:io_done   1          
 24    DONE          RUN:io        1          
 25    DONE          BLOCKED               1
 26    DONE          BLOCKED               1
 27    DONE          BLOCKED               1
 28    DONE          BLOCKED               1
 29    DONE          BLOCKED               1
 30*   DONE          RUN:io_done   1

python3 process-run.py -s 3 -l 3:50,3:50
Time   PID: 0        PID: 1        CPU     IOs
  1    RUN:cpu       READY         1          
  2    RUN:io        READY         1          
  3    BLOCKED       RUN:io        1       1
  4    BLOCKED       BLOCKED               2
  5    BLOCKED       BLOCKED               2
  6    BLOCKED       BLOCKED               2
  7    BLOCKED       BLOCKED               2
  8*   RUN:io_done   BLOCKED       1       1
  9*   RUN:cpu       READY         1          
 10    DONE          RUN:io_done   1          
 11    DONE          RUN:io        1          
 12    DONE          BLOCKED               1
 13    DONE          BLOCKED               1
 14    DONE          BLOCKED               1
 15    DONE          BLOCKED               1
 16    DONE          BLOCKED               1
 17*   DONE          RUN:io_done           1          
 18    DONE          RUN:cpu       1

python3 process-run.py -s 3 -l 3:50,3:50 -I IO_RUN_IMMEDIATE
Time   PID: 0        PID: 1        CPU     IOs
  1   RUN:cpu        READY         1          
  2   RUN:io         READY         1          
  3   BLOCKED        RUN:io        1       1
  4   BLOCKED        BLOCKED               2
  5   BLOCKED        BLOCKED               2
  6   BLOCKED        BLOCKED               2
  7   BLOCKED        BLOCKED               2
  8*  RUN:io_done    BLOCKED       1       1
  9*  READY          RUN:io_done   1          
 10   READY          RUN:io        1          
 11   RUN:cpu        BLOCKED       1       1
 12   DONE           BLOCKED               1
 13   DONE           BLOCKED               1
 14   DONE           BLOCKED               1
 15   DONE           BLOCKED               1
 16*  DONE           RUN:io_done   1          
 17   DONE           RUN:cpu       1

python3 process-run.py -s 3 -l 3:50,3:50 -S SWITCH_ON_END
Time   PID: 0        PID: 1        CPU     IOs
  1   RUN:cpu        READY         1          
  2   RUN:io         READY         1          
  3   BLOCKED        READY                 1
  4   BLOCKED        READY                 1
  5   BLOCKED        READY                 1
  6   BLOCKED        READY                 1
  7   BLOCKED        READY                 1
  8*  RUN:io_done    READY         1          
  9   RUN:cpu        READY         1          
 10   DONE           RUN:io        1          
 11   DONE           BLOCKED                 1
 12   DONE           BLOCKED                 1
 13   DONE           BLOCKED                 1
 14   DONE           BLOCKED                 1
 15   DONE           BLOCKED                 1
 16*  DONE           RUN:io_done   1          
 17   DONE           RUN:io        1          
 18   DONE           BLOCKED                 1
 19   DONE           BLOCKED                 1
 20   DONE           BLOCKED                 1
 21   DONE           BLOCKED                 1
 22   DONE           BLOCKED                 1
 23*  DONE           RUN:io_done   1          
 24   DONE           RUN:cpu       1 
```
- Reasoning / 理由:
```
使用-I IO_RUN_IMMEDIATE时: I/O完成后, 立即切换回发起请求的进程, 从而使其他进程可以在I/O等待时调用cpu, 提高整体效率
使用-S SWITCH_ON_END时: 当前进程执行完毕后, 才切换到下一个进程, 从而可能导致cpu空闲
```
- Verified result / 验证结果:
- Analysis / 分析:
```
1. 缺少总时间、CPU利用率
1.1. python3 process-run.py -s 1 -l 3:50,3:50
Stats: Total Time 15
Stats: CPU Busy 8 (53.33%)
Stats: IO Busy  10 (66.67%)

1.2. python3 process-run.py -s 1 -l 3:50,3:50 -I IO_RUN_IMMEDIATE
Stats: Total Time 15
Stats: CPU Busy 8 (53.33%)
Stats: IO Busy  10 (66.67%)

1.3. python3 process-run.py -s 1 -l 3:50,3:50 -S SWITCH_ON_END
Stats: Total Time 18
Stats: CPU Busy 8 (44.44%)
Stats: IO Busy  10 (55.56%)

1.4. python3 process-run.py -s 2 -l 3:50,3:50
Stats: Total Time 16
Stats: CPU Busy 10 (62.50%)
Stats: IO Busy  14 (87.50%)

1.5. python3 process-run.py -s 2 -l 3:50,3:50 -I IO_RUN_IMMEDIATE
Stats: Total Time 16
Stats: CPU Busy 10 (62.50%)
Stats: IO Busy  14 (87.50%)

1.6. python3 process-run.py -s 2 -l 3:50,3:50 -S SWITCH_ON_END
Stats: Total Time 30
Stats: CPU Busy 10 (33.33%)
Stats: IO Busy  20 (66.67%)

1.7. python3 process-run.py -s 3 -l 3:50,3:50
Stats: Total Time 18
Stats: CPU Busy 9 (50.00%)
Stats: IO Busy  11 (61.11%)

1.8. python3 process-run.py -s 3 -l 3:50,3:50 -I IO_RUN_IMMEDIATE
Stats: Total Time 17
Stats: CPU Busy 9 (52.94%)
Stats: IO Busy  11 (64.71%)

1.9. python3 process-run.py -s 3 -l 3:50,3:50 -S SWITCH_ON_END
Stats: Total Time 24
Stats: CPU Busy 9 (37.50%)
Stats: IO Busy  15 (62.50%)
```
