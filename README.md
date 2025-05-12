```markdown
# Serial Data Communication on STM32 (Interrupt-Driven UART)

This project is a practice assignment developed using the STM32L4 Discovery IoT board to explore interrupt-driven UART communication. It was created as part of my Embedded Systems Programming coursework. The core idea was to replace polling with interrupt-based IO and manage data using circular buffers. To make things more interactive, I implemented a simple math quiz that runs entirely over UART.

All base files and setup were provided by my tutor, **Craig Duffy**, who designed them to help us understand embedded development workflows. My responsibility was mainly focused on the `main.c` and `Makefile`—where I implemented the UART logic and quiz functionality.

---

## Features

- Fully interrupt-driven UART communication via USART1
- Circular buffer for both receiving and transmitting (20 bytes)
- Echo and user input handling via UART
- Console-based math quiz using `printf` and `fgets`
- LED toggling for basic visual feedback (GPIO output)
- Bare-metal programming in C (no OS or RTOS)
- Custom low-level IO integration via `__io_putchar` and `__io_getchar`

---

## File Overview

- `main.c` – Contains the UART setup, circular buffer logic, math quiz code, and LED toggling.
- `Makefile` – Cross-compiles the code using `arm-none-eabi-gcc`.
- HAL/CMSIS/Startup files – Provided externally (not part of this repo).

---

## Example UART Output

This is what you'll see in the serial terminal after flashing the board:

```

Welcome to the Math Quiz!

Question 1: What is 3 + 7?
Your answer: 10
Correct!

...
Quiz complete!
You got 5 out of 5 questions correct.

````

---

## How It Works

- UART is set up to use interrupts for both RX and TX.
- The RX interrupt stores incoming characters into a circular buffer.
- TX data is queued in another circular buffer and transmitted via the TX interrupt.
- Standard I/O functions (`fgets`, `printf`) are redirected through these buffers.
- The main loop drives a math quiz that interacts with the user via UART.

---

## Tools Required

- STM32L475 Discovery IoT Board
- ARM Toolchain (`arm-none-eabi-gcc`)
- OpenOCD for flashing/debugging
- Serial terminal (e.g., `minicom`, `PuTTY`)

---

## How to Build and Run

### Build the Project

```bash
make
````

### Flash and Debug

```bash
openocd &               # Start OpenOCD server
arm-none-eabi-gdb demo.elf
> target remote :3333
> load
> continue
```

### Open UART Terminal

```bash
minicom -b 115200 -D /dev/ttyACM0
```

You should now see the welcome message and quiz output.

---

## Skills Gained

* Working with STM32 HAL libraries
* Configuring and using UART with interrupts
* Implementing circular buffers for TX/RX
* Using GDB and OpenOCD for debugging
* Writing and understanding Makefiles
* Bare-metal C programming on ARM Cortex-M

---

## Author

**Mohammad Faraj**
[GitHub](https://github.com/MoFa-14) | [LinkedIn](https://www.linkedin.com/in/mohammad-faraj-480615272/)
