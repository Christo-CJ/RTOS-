# Understanding state diagram of RTOS  

New ready running waiting inactive (almost same as linux)  
Instead of exit state of linux we have inactive.  

To write rtos we have to useinbuilt library functions.  

I'm going to use `rtx rtos`.

Library functions we get a function to create a task(create_task) function name may differ.  

While creating task we have to assign priority to this task.  
Priority measured in number (1 to 254)  1 low  254 high  priority level rise from 1 to 254
in linux priority is reverse order.  

In every rtos library funtions will be there.  

We are creating 3 tasks t1 t2 t3  

First creation, task will go to new state.  
From new to ready state movement is called admit.  
We have to call function or create task then the scheduler admit this task to ready state.  
Lets assume priority level t1 is 1 t2 also 1 t3 also 1
as soon as task 1 comes then from ready state to running is called `dispatch`  
t1 running on processor task 1 stay in ready state till time slice is not over in rtos typically will be 10ms.
Suppose t1 take more time then t1 will be moved back to ready state then t2 comes to running from ready then t2 use processor time
then as follows t3.  
then again after t3 t1 will come to running.  
Here t1 t2 t3 each task cpu use processor time 10ms  
10ms is the context switch time (very quick)  
All task same time also context switch time. scheduling policy used is Round Robin.  
- in rtos all task having same priority then scheduler will use round robin policy to execute the task.  
  or   
- same priority tasks are executed in the round robin fashion.
`Scheduler` is responsible for dispatching task  
First scheduler check priority table is all has same priority .  
Idle task is the predefined task  
t1 t2 t3 is user defined  
All has same priority then round robin fashion.  
Before dispatching always check priority table. 
When creating new task for t2 having priority level 2 then before dispaching scheduler check priority table.  
so first dispatch t2.  
If t1 already running and t2 come scheduler hen get t1 to ready and t2 go to running state.  
If only 5ms used by t1 then also t2 is dispatched after execution of t2 low priority will come 
If t2 has more time required then each 10 ms it goes to ready state then scheduler check priorityy table then again t2 dispatched 
Scheduler dispatch high priority task.  
t1 and t3 get time only after t2 finished  
or t2 priority changed.  
All the deleted task goes to inactive task.  
Suppose at run time t2 priority to 1 then scheduler execute in round robin fashion.  
Suppose t2 goes to waiting state t1 and t2 gets time for running.  

- waiting state:  
waiting for any 
  - IO event 
  - semaphore event
  - Mutex event
  - Mailbox event
  
If goes in waiting state all tasks run in `round robin`.
  
Suppose event is occured then t2 will goes to ready state
Immediately high priority task gets dispatched.  

Priority is assigned with different then scheduler will use priority based scheduling policy.  

## Idle task

Idle task available in ready state all the time but will not go to running.  
Idle task predefined task of our RTOS.  
Idle task created by RTOS kernel.  
Priority is 0(zero)  
Idle task execute only if t1 t2 t3 goes to waiting or if all the tasks are deleted.  
Then only idle task get chance to execute.  
Idle task remeins in ready state only.  




## INTRODUCTION to RTX RTOS

REAL TIME EXECUTIVE RTOS
- Designed by keil its royalty free RTOS.
- It is determnistic RTOS designed for ARM and cortex-M devices.
- (we using LPC2148 ARM7)
- RTX is a keil's small footprint RTOS ,designed for ARM based controllers(size of RTOS is small)


## FEATURES of RTX RTOS

1. RTX is royalty free,deterministic RTOS with source code.   
2. Flexible scheduling  round robina and priority based.  
3. High speed real time operations with low interupt latency. 
4. Small footprint for resource constrained systems(only occupy less space,MC with less inbuilt memory).   
5. Unlimited number of tasks each with 254 priority level.  
6. Unlimited number of mutex,semaphore and mailboxes.  
7. Supports user timers/software timers(alarm sysytem call).   


## RL-ARM LIBRARY of RTX RTOS

Real time ARM library  

Take eg: of linux OS we have glibc where all our functions available in user space (printf,scanf)  
In rtl has RL-ARM library using this we can communicate with kernel space.  
Application in user space need to communicate wity kernel through RL-ARM library.  

. Its middleware library are now part of MDK-professional(keil ide) and are not available seperately

## RL-ARM library functions

- os_sys_init
- os_sys_init_prio
- os_tsk_create
- os_tsk_self
- os_tsk_delete
- os_tsk_delete_self
- os_tsk_prio
- os_tsk_prio_self
- os_dly_wait

## os_sys_init

- This function initializes and starts the RTX kernel(every initialization)
- This fucntion launches RTX onlys tarts the first task running.

`syntax :  void os_sys_init(void(*tsk1)(void));`

or        `void os_sys_init(addr_of_task1)` 

```c
task1()
{
...(other tasks (eg:task2 task3))
}
task2()
{
...
}
task3()
{
...
}
main()
{
os_sys_init(task1);
}
```
In main after os init any code written will not execute then create tasks from task 1  
After this function kernel will start ,so from task 1 we have to created task2 and task3  
  
Bootup process of RTOS:    
After reset --> startup code will execute --> main -->start kernel --> init RTOS -->create a idle task -->create task1 --> task 1 will create other tasks and they execute in round robin  
  
Note: After starting the kernel, only rtos tasks will run on the processor.Main function will not execute again.  
