## Introduction: 
DUOS refers to Dhaka University Operating System, an experimental educational operating system designed primarily to carry out the OS course assignments for CSE students 
at the University of Dhaka to understand its technologies. Since July 2022, the DUOS has been under continuous development, and the initial credit goes to the 25th batch of 
CSE, DU. The CSE DU develops DUOS  on an ARM processor and, more remarkably, on a Cortex-M4 v7 architecture. DUOS currently supports 32-bit ARMv7-M processor-based MCU such 
as  STM32F4xx. However, the DUOS plans to expand its features to accept other ARM processors (such as ARMv8 and ARMv9 ARM 32 and 64-bit architectures). The Operating system
must be tiny, provide a development venue for the controller designer and intelligent system developers, and help the affiliated technology enterprise deliver industry-grade 
control systems. 



## SysTick implementation involves configuring its registers to use it as a 24-bit down-counter for timing and delays in embedded systems, particularly on ARM Cortex-M 
microcontrollers. Key steps include setting the reload value, enabling the counter and the interrupt, and handling the interrupt handler to perform time-based actions, 
such as a delay or incrementing a counter variable. For example, an implementation might set the reload value for a desired period, enable the SysTick interrupt, and have 
a SysTick_Handler() function that runs when the counter reaches zero to update a timestamp or control an LED. ##
## Core components and configuration : 
  * SysTick Control and Status Register (SysTick_CSR): This register controls the timer's operation. Key bits are:
      1. Enable bit: Enables or disables the counter.
      2. Tick interrupt enable bit: Enables or disables the SysTick exception (interrupt) when the counter reaches zero.
      3. Clock source bit: Selects between the processor's internal or external clock source.
      4. COUNTFLAG: A read-only bit that is set to 1 when the counter has reached zero.
  * SysTick Reload Value Register (SysTick_RVR): Stores the value the counter reloads from each time it reaches zero.
  * SysTick Current Value Register (SysTick_CVR): A 24-bit register that holds the current countdown value. It is cleared when written to, which does not trigger
    the exception.
## Implementation steps : 
  1. Configure the clock source: Select the appropriate clock source in the SysTick_CSR register. Using the internal clock is common.
  2. Calculate the reload value: Determine the value to load into SysTick_RVR to achieve the desired frequency. This is done using the formula:
          ** Reload Value = {Clock Frequency} / {Desired Interrupt Frequency}
  3. Initialize the timer:
       1. Write the calculated reload value to the SysTick_RVR register.
       2. Configure the SysTick_CSR register :
           * Set the clock source and the tick interrupt enable bit.
           * Set the enable bit to start the timer.
  4. Handle the interrupt:
      1. Create a SysTick_Handler()` function. This function will be executed every time the SysTick timer counts down to zero.
      2. Inside the handler, perform actions like updating a timestamp, toggling an LED, or calling a delay function.
  5. For delays: To create a delay, you can either poll a flag set by the SysTick_Handler() or use the SysTick_CVR to wait until the counter reaches a specific value. 
