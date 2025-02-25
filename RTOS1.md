# Introduction to Real-time system and Real time operating     

On top of mircrocontroller we have written program like driver and application   
now we are going to run rtos on microcontroller on top of rtos we  are writting drivers and applications.  

What ever aapplication writing over `rtos` is real time applications, driver is also part of application.  

Rtos is small os specially designed for microcontroller(MC)
Rtos can be run on any microcontroller 8051,arm controller,avr,pic,...

OS will provide interface between application and hardware and hardware with application.

## Role of OS is resource management 
Middleware software is called `OS` which will provide graphical user interface.
between software and Hardware.
It can take care of multi tasking.
Like keyboard,mouse,internet,screen... all working parallely because of OS.

OS will take input from hardware to application then from application to software.

when we buy our laptop we dont know keyboard program but it is available in OS so we no need to write.

RTOS is different from GPOS general purpose(windows ,linux)
GPOS display gui.what able to see on software is GPOS gui.
RTOS is not designed for MC,where no gui is used.

If only need parallel execution or multitasking ,no rtos required suppose need to execute parallelly/multitasking then we have to go wtih OS.

RTX-51 tiny RTOS is specially designed for 8051(it will not work for other controller exclusively for 8051)

Realtime system: It is designed to provide a timely response to real-world events.
Eg:airbag system,autopilot system in aeroplane
Designer will asign the time handling.context witch time should be lesser.
when io event is generated it will then context sitch in milli seconds.

Rate of RTOS MC will be higher than that of normal MC.
RTOS doesnt use gui.
Inside airbag airbag should be open.
If driver doent pur seatbelt it will not or the airbag willnot deploy.


## Use of RTOS
- Deterministic OS  means timing behaviour of OS is previously defined.
- Faster and predictable responce 
- Easy to implement real time applications 
   - real time applications come with application programming interface (API)
   - predefined library fuctions.]
- Multitasking support in small memory space
   RTOS size will be in kb.
- ITC Inter Task Communcation mechanism suport(sync)
   event handling ,semaphore event handling,mutex...
    there is no process there are only task so that task communication is depicted.
- Small footprint 
   you can set or adjust in small size and is costumizable so called small footprint
- Open source we can modify os according to our requirement
- Customisable for eg: amazon build an os on freertos
- Events and interupts are handled in a defined time
- Task scheduler gives illusion of executing number of tasks simultaneously(there is no actual parallel execution in parallel its time slice method is used)
...

2 type of realtime
- Hard realtime 
- Soft realtime

Packet exchanging is main reason big sharks use freertos.

## Hardreal time system
- Meeting a deadline is mandatory
- Missing a deadline is a total system failure (if airbag not openend its failure)
- If the value of result after a deadline is "zero" .(if airbag opens up on 90 nanosec but its 1 sec its after deadline so its zero)

## Soft real time system
- Meeting deadlines is not compulsory for every task.(small delay can be ignored)
- The value of result after a deadline is not zero
- eg: ATM machine,game zones 
