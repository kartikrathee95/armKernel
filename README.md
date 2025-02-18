Build a minimal multi-tasking OS kernel for ARM from scratch

Prerequisites
-------------
- [QEMU with an STM32 microcontroller implementation](http://beckus.github.io/qemu_stm32/)
  - Build instructions
```
./configure --disable-werror --enable-debug \
    --target-list="arm-softmmu" \
    --extra-cflags=-DSTM32_UART_NO_BAUD_DELAY \
    --extra-cflags=-DSTM32_UART_ENABLE_OVERRUN \
    --disable-gtk
make
```
- [GNU Toolchain for ARM](https://launchpad.net/gcc-arm-embedded)
- Set `$PATH` accordingly

Steps
-----
* `00-Semihosting`
  - Minimal semihosted ARM Cortex-M "Hello World"
* `00-HelloWorld`
  - Enable STM32 USART to print trivial greetings
* `01-HelloWorld`
  - Almost identical to the previous one but improved startup routines
* `02-ContextSwitch-1`
  - Basic switch between user and kernel mode
* `03-ContextSwitch-2`
  - system call is introduced as an effective method to return to kernel
* `04-Multitasking`
  - Two user tasks are interatively switching
* `05-TimerInterrupt`
  - Enable SysTick for future scheduler implementation
* `06-Preemptive`
  - Basic preemptive scheduling
* `07-Threads`
  - Implement user-level threads
* `08-CMSIS`
  - Illustrate hardware abstraction layer (HAL) by introducing CMSIS
  - Both emulator (based on stm32-p103) and real device (STM32F429i discovery)
    are supported.

Building and Verification
-------------------------
* Changes the current working directory to the specified one and then
```
make
make qemu
```

Guide to Hacking 08-CMSIS
=========================================
08-CMSIS implements preemptive round-robin scheduling with user-level threads
for STM32F429i-Discovery (real device) and STM32-P103 (qemu).

## Get the dependencies:
```
git submodule init
git submodule update
```
