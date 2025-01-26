**what is RTOS?**
Real time operating system is an operating system intended to serve real time application that process data as it comes in,mostly without buffer delay.

Multi tasking where the task switching context text will be taken care of rtos.
in time slicing if time slice time is 10ms then each task switching,context task all taken care by rtos.

Multitasking is feature given by rtos.
Intertask communication.(ITC)
Scheduler
Dispatcher 
These are available in rtos.
Rtos will be having a few features of gpos.
File management,memory management,network management availbale at gpos which makes rtos small size.

## list of rtos
- RTX(keil)
- Freertos(real time pvt ltd)
- Vxworks(wind river)licensed rtos
- Threadx(microsoft express logic)
- embOS(segger)
- ucos(micrium) etc...

`RTX 65 tiny` exclusively build for 8081.

RTLinux is a hard realtime rtos `microkernel`.  
Indian OS is used first by NOKIA.


## RTX rtos


**GPOS**                                        |               **RTOS**
                                        
- Designed for general purpose computers        | Designed for embeddded purposs.
- Desiged to acieve high throughput             | Designed for perfromance pbot for throughput
- Same cases it will provide unpredcicatble     | Always product predicatabe and quike responce
and slow reposnce                               |  
- slow responce and not quick responce          | Faster responce and quick response comapred to GPO
- Scheduling policy is not priority based always| schedulingppolicy is priority based alwyas
because it has to achieve high throughput       |
- mololithic or hybrid kernels are used in the  | Microkernels are used in the RTOS 
GPOS                                            |  
- context switch time ois more compared to rtos | context switching time is less compared to gpos due to less overhead
- priority inversion                            | no priority inversion  
- windows                                       | rtx

RTOS have not running in backgroud obviously performance will increase

microkernel used in rtos
rtos follow priority based.
3 kernel windows and mac use hybrid kernel linux use monolithic  rtos microkernel.


## Priority inversion

2 processes p2 and p1 and a share resource serial terminal
Any proces can use serial ,rule if any terminal has to use serial terminla process has to lock the resource .so at same time no oter process of os can access it.so thats why lock and unlock .
Who lock hardware resource only they can unlock.if one is in lock other will be in wait.only when unlock can happen next process.
If one process is low priority is running another process of high priority came then also it should wait.
There is process called prioity inheritence inorder to avoid this priority inversion.

## Type of kernels

- Monolithic kernel
- Micro kernel
- Hybrid kernel 


## Monolithic kernel

It is a single large process running entirely in a single address space(ie kernel space)
eg: linux

User space and kernel space  
- user space --applications a.out,bashshell,firefox,..
- kernel space--memory management,file manager ,network manager,scheduler...

This is what monolithic kernel looklike.

uname -r  4.15.0-142-generic   (display kernel version)  

/boot  ls kernel image is there  
If we remove the image os will not start.  

Path of kernel image   /boot


## Microkernel

Small kernel it is a minimal kernel which offers kernel services with minimum over head(extra code).  
eg:RTX,Vx works RTOS,...



## Comparison micro and monolithic

microkernel the scheduler and ITC mech work in kernel space and in user space application and drivers
monolithic  file manager,memory manager,network manager,scheduler,device driver  in kernel scapce in user spcae only application.


## Hybrid kernel
It is a combination of monolithic and micro kernel  
eg:mac


`kernel program + gui program = OS`

`ps -e | grep "X" `
command gives gui program and process id
if kill process gui will stop immideatly screen logoff.
