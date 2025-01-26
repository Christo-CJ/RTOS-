Before calling os_sys_init then before calling the function iniialize the init parameters.  
Once started it will not coming back to main function.  
After creating idle task it create task 1.  

Suppose task 1 is created address of task 1 is given to kernel.Kernel will create task 1 with given priority.    
Every task has unique priority.  
While calling this function we doesn't have option to set priorty so kernel will create task 1 and give priority 1.  
which task is given in os_sys_init get priority level1.  
Later can change priority using priority function.  

Suppose give different priority `os_sys_init_prio(task1,prio_level); ` 
1 to 254(low to high)  
prio_level is a integer value 1 to 254.    
we cannot use both os_sys_init and os_sys_init_prio at same time.  

## os_tsk_create

This function is used to create a new task to running RTOS and adds it to ready state.  

**prototype:**

`OS_TID os_tsk_create(void(*task)(void),u8 prio);`

prio 1-255
`void(*task)(void) - task address`

## Return value

on success: Task ID (TID)  ->file descriptor as same in fopen  
on failure: 0  

with help of TID we can do task activities like change prio,delet task,sync,etc..  


## setting up a project in kel ide

keil for RTX.

1.create a new project and a startup code into source group  
2.select "RTX_kernel" option from target settings.  
   Right click on target->Options for target-->Operating system -->RTX kernel.  
3.Add configuration file into source group  
  Name of config file: RTX_conf_LPC21xx.c  
  path: C:keil_v5\ARM\RL\RTX\config  
4.Startup code setting  
  +comment out line 259   
  +add below line at line number 257 
       IMPORT SWI_Handler  
(before writing IMPORT SWI_Handler use a tab space)  
5.Write a main.c an ass it to source group.  
  

**Why RTX_conf_LPC21xx.c?** 
RTOS settings are available here
   - Time-slice setting
   - Round robin time slice setting
   - Timer selection
   - Number of concurrent tasks
   - idle tasks is defined here
  
we can change the file inorder to modify these setings.

`IMPORT` at time of context switching it is necessary.
  
Header file where all functtion defenitions are included  
`#include <RTL.H>`

**How to define task in RTXRTOS?**  
```c
__task void task_name(void)
{
   for(;;)
    { 
     ...              //infinite execution 
    }
}
```
for,while,do while any loop

or
```c
__task void task_name(void)
{
...                   //for one time execution  
...
os_tsk_delete_self();
}
```
so function will delete itself


## Understanding Time_slice inRTX RTOS

Time-slice is called as system tick is 10ms  

`Robin_timeout`  is called Round_robin_time_slice is 50ms   

If tasks are execuring in RR then RTX RTOS will use 50ms for round robin task.
t1 t2 t3  each task gets 50ms `time_slice` 

These settings can be changed in conf file.

## os_tsk_self

`os_tsk_self();` return TID of currently running task.
`tid1=os_tsk_self`
prototype:  `S_TID os_tsk_self(void)`

**Return:**
On success: TID of current task  
This function will never fail.  
  
  
Suppose when create task2 with priority 2 task 2 high priority running in infinite loop only task 2 will run because task 2 is not ending and also has high priority.
Task1 will starve for cpu time.  

Though they are executed in timeslice but we get an illusion of parallel execution.  
Debug --> system and thread viewer --> display all the options and information get displayed.
