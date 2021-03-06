### 中断处理程序

1. 为了处理中断，内核会执行中断单处理函数，处理其次是工作在中断上下文模式；
2. 中断处理函数必须快速执行完毕，所以这类函数中不能休眠；
3. 中断处理程序只处理最紧急的与硬件相关的操作，如果还有多余的工作，应该交由下半部执行。

### 中断控制

- 禁止和激活中断  
`local_irq_disable()`和`local_irq_enable()`分别用于禁止和激活本地中断（所有的中断）；  
上面的函数不建议使用，因为`local_irq_enable()`会无条件激活中断。  
`local_irq_save()`和`local_irq_restore()`分别用于禁止中断并保存中断系统的状态及恢复状态，这两个函数必须在同一个函数中使用。

- 禁止和激活指定中断线  
`diaable_irq(unsigned int irq)`和`enable_irq(unsigned int irq)`分别用于禁止和激活指定中断线。

### 下半部

- 软中断  
    静态编译期间分配，不能动态注册注销，系统最多有32个软中断；  
    软中断由分配索引（linux/interrupt.h中声明）、注册处理函数（`open_soft_irq(index, func)`)、触发(`raise_softirq(index)`)三部完成；  
    相同的软中断在多个处理器上可以同时处理，需要注意同步。  

- tasklet

- 工作队列
