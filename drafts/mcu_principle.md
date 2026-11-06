# MCU Principle

MCU means Microcontroller Unit which includes 3 parts: ARM Core, Memory and On-chip Peripherals. In this course, we mainly focused on the 3rd part: peripherals. And the detail of Cortex-M3 kernel and memory were covered in ARM Architecture.

I would draw the structure of the knowledge from this course: 

![image.png](MCU%20Principle/image.png)

### Clock Source

Before getting into peripherals, I would talk about Clock first because Clock is the basis of running, the first step is always activation of CLK. 

There’re 4 kinds of clock source: HSE, HSI, LSE, LSI. Commonly we choose 8MHz HSE as system CLK source. 

Then, we configure the clock tree in STM32CubeMX. Make the CLK source Going through PLL and multiplied to 72MHz (which is the maximum frequency of STM32F1), and providing clock for AHB (72), APB1 (36), APB2 (72). 

### GPIO- I/O Interface

The first peripheral I would mention is GPIO. Because the GPIO pins are the interface to input/output.

There’re 7 GPIO ports: A~G, each port has 16 pins (Px0~15). We could configure the modes of pins by CRL/CRH. CNFn:MODEn. MODE is to choose the in/output mode and speed. CNF is to configure the Pull-up/down or Analog or Floating for input and the Push-Pull or Open-Drain for GP or AF. 

We can configure the pins in CubeMX or modify the register directly. The detail of I/O pins’ definition and register bits could be found in Datasheet and the Reference Manual.  

### Timer: TIMx and SysTick

Then, the next peripheral: timer. Timers are used to count events, making delays and output PWM pulse.

SysTick: 

SysTick is a counter built in the Cortex-M3 kernel. SysTick has 3 registers: STCTRL to control SysTick; STRELOAD to refresh the SysTick value; STCURRENT to store the current counting value. SysTick can generate Timebase and Delay, trigger kernel SysTick exception.

TIMx:

TIM is on-chip peripheral. It provides more functions than SysTick. TIMx are divided to 3 parts: TIM6, 7 are basic Timer, are used to trigger TIM interrupt and TRGO; TIM1, 8 are advanced Timer, but we didn’t cover too much; TIM2~5 are General-Purpose Timer, we mainly use them. GP Timer have Capture/Compare Channels. Capture mode is used to measure the time of the inputing events and Compare mode is used to output compare/PWM generation. The modes are determined by CCMR.

PWM

TIM can output PWM pulse by ARR (Auto Reload Reg.) and CCR (Capture/Compare Register): <drawing the PWM working graphic>

### EXTI: External Interrupt

there are 16 vectors for EXTI, The signal workflow is simple: a GPIO pin connects to AFIO (configured by AFIO_EXTICRx), then goes to EXTI, and finally reaches NVIC. NVIC is exception controller built-in kernel, we detail that in ARM architecture. 16 vectors are divided: 0~4 have individual EXTI vectors, 5~15 have been combined to 2 vectors: EXTI9_5, EXTI15_10. The combined EXTIs are serviced by the same ISR: e.g. EXTI9_5_IRQHandler. Then we program the handler using if statements discerning which EXTI line and handling. 

### ADC

Analog-to-Digital converter. STM32F103 adopts SAR ADC: which is the most widely used ADC. SAR means successive approximation register. It measures the analog value via level-by-level comparison. The CLK of ADC is 14MHz max, so it need to prescaler. The pre-set coefficients are 2, 4, 6, 8 so we choose 6 to make ADC running with 12MHz CLK frequency.
There’re 4 ADCs and each ADCx have 4 channels. We need to configure the SQR(sequence register) to determine the sample sequence.

## Serial Communication Protocols

### USART: Universal Synchronous-Asynchronous Receiver-Transmitter

USART has 2 modes: syn and asyn. We mainly covered the UART: asynchronous mode. UART is full-duplex asyn. protocol, so there’re 2 lines without CLK: TX and RX. USART adopts double-buffering mechanism, so there’re 2 registers: DR and Shift Register (invisible).

### I2C: Inter-Integrated Circuit

I2C is half-duplex synchronous protocol, so there’re 2 lines: SDA and SCL. SDA is used for data transmission and SDA is used to synchronize the CLK. I2C is connection-oriented communication which is similar to TCP in computer networking. It need to handshake before and hand wave after communication via START/STOP signal. I2C is widely used in multiple slaves communication. It implement SDA/SCL connecting to slaves directly by Open-Drain output and pull-up resistor. 

### SPI: Serial Peripheral Interface

SPI is full-duplex synchronous protocol, there’re 4 or more lines: SCLK, MOSI, MISO and CS(Chip select) or SS(Slave slect). The transmitting and receiving occur at the same time. If we need to connect more slaves, just connect more SS lines and branch the MOSI/MISO to them. SPI uses SS to choose slave, so doesn’t need to handshake. We can configure the idle CLK level via CPOL and sample edge via CPHA.