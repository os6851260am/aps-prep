# APS 面试各科目“底线必知必会（零借口红线）”清单

> **核心原则**：
> 在德国 APS 审核中，由于**物联网工程 (IoT Engineering)** 属于典型的软硬件交叉学科（横跨电子电路、嵌入式、通信、计算机软件），对于某些课程的**深层细节**，你完全可以坦诚且合理地回答：*“作为物联网工程专业，这门课我们的教学重点偏向于 [应用/硬件结合/宏观流程]，没有深入展开 [纯理论推导/底层源码]。”*
>
> **但是**，每一门印在成绩单上的专业课与数学课，都有**3～5 个“开机即学、贯穿全书”的底线概念（Redline Questions）**。只要学过这门课、哪怕只考了 60 分，也**绝不可能没学过这些内容**。一旦在这些问题上卡壳或试图用“不是专业重点”搪塞，考官会立刻判定为**知识体系漏洞或成绩真实性存疑**。
>
> 本文档严格对照你的英文成绩单 `Score-EN.pdf`（全部 30 门专业及数学课程，合并配套课设/实验后共 22 个核心条目），逐科列出：
> - 🔴 **绝对不能答不出来的底线问题（答不上来 = 致命漏洞）** + **一句话英文核心破题点**
> - 🟢 **可以用“非本专业侧重点”合理挡回的边界（安全转移话术）**

---

## 目录
1. [第一模块：感知层与嵌入式硬件 (Perception & Embedded Hardware)](#一第一模块感知层与嵌入式硬件-perception--embedded-hardware)
2. [第二模块：计算机核心与系统软件 (CS Core & System Software)](#二第二模块计算机核心与系统软件-cs-core--system-software)
3. [第三模块：网络与物联网通信 (Network & IoT Communication)](#三第三模块网络与物联网通信-network--iot-communication)
4. [第四模块：应用层、GUI 与数据智能 (Application, GUI & Data Science)](#四第四模块应用层gui-与数据智能-application-gui--data-science)
5. [第五模块：数学基础课 (Mathematics Fundamentals)](#五第五模块数学基础课-mathematics-fundamentals)
6. [附：考场“合理挡回 vs 致命踩雷”黄金话术模板](#六附考场合理挡回-vs-致命踩雷黄金话术模板)

---

## 一、第一模块：感知层与嵌入式硬件 (Perception & Embedded Hardware)

### 1. Circuit and Electronic Technology（电路与电子技术）
- **成绩单信息**：Spring 2024 | **5.0 学分（全单最高单科学分）** | **`60(Resit1)`** ⚠️ *极高抽查概率*
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **三大基本物理量与欧姆定律 (Ohm's Law)**：什么是电压 ($U$)、电流 ($I$)、电阻 ($R$)？公式 $U = I \times R$ 及串并联分压/分流规律（考官极喜欢让你在纸上画两个电阻串联/并联算总电阻）。
     - *破题*：`In series: R_total = R1 + R2 (voltage divider); In parallel: 1/R_total = 1/R1 + 1/R2 (current divider).`
  2. **基尔霍夫定律 (Kirchhoff's Laws: KCL & KVL)**：KCL 和 KVL 分别说什么？本质守恒是什么？
     - *破题*：**KCL** (Current Law): 流入节点的电流之和等于流出之和 ($\sum I_{in} = \sum I_{out}$，电荷守恒)。**KVL** (Voltage Law): 闭合回路中所有电压升降的代数和为零 ($\sum U = 0$，能量守恒)。
  3. **直流电 vs 交流电 (DC vs AC) & 电容/电感基本特性**：DC 和 AC 的区别？电容在直流电路中相当于什么？
     - *破题*：电容（Capacitor）“通交流、阻直流”（blocks DC, passes AC），常用于电源去耦滤波（decoupling/filtering）和储能；电感（Inductor）“通直流、阻交流”。
  4. **三大基础半导体器件的核心作用**：二极管 (Diode)、三极管/MOS管 (Transistor)、运算放大器 (Op-Amp) 到底是干嘛的？
     - *破题*：**Diode**：PN 结单向导电（unidirectional conductivity，用于整流或防反接）；**Transistor (BJT/MOSFET)**：小信号放大（amplification）或电子开关（electronic switch，如 MCU 驱动电机/继电器）；**Op-Amp**：放大微弱模拟信号（如传感器信号调理电路）。
  5. **基本数字逻辑门 (Basic Logic Gates)**：能画出并写出 `AND`（与）、`OR`（或）、`NOT`（非）、`XOR`（异或）的真值表 (Truth Table)。
- 🟢 **可合理挡回的边界**：
  - 复杂的三相交流电相量图计算、晶体管高频小信号微变等效电路（$h$ 参数推导）、复杂卡诺图多级时序状态机化简。
  - *话术*：*"In our IoT curriculum, this 5-credit course combined basic circuit analysis, analog electronics, and digital logic into one semester, so we focused on fundamental circuit laws and sensor/MCU interface circuits rather than complex high-frequency transistor derivations."*

---

### 2. Principles of Computer Organization（计算机组成原理）
- **成绩单信息**：Spring 2024 | **3.5 学分** | **`78`**
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **冯·诺依曼架构五大部件 (Von Neumann Architecture)**：计算机由哪 5 部分组成？核心特点是什么？
     - *破题*：运算器 (**ALU**)、控制器 (**Control Unit**)、存储器 (**Memory**)、输入设备 (**Input**)、输出设备 (**Output**)。核心特点是“存储程序 (Stored-Program Concept)”，且**指令和数据共享同一存储器和总线**（对比 ARM Cortex-M 的哈佛架构：指令与数据总线分离）。
  2. **CPU 内部组成与一条指令的执行周期 (CPU Structure & Instruction Cycle)**：CPU 里面有什么？执行一条指令分哪几步？
     - *破题*：CPU = **ALU**（算术逻辑运算）+ **Control Unit**（指令译码与控制信号）+ **Registers**（如 `PC` 程序计数器存下一条指令地址、`IR` 指令寄存器）。指令周期：**Fetch（取指）$\rightarrow$ Decode（译码）$\rightarrow$ Execute（执行）$\rightarrow$ Write-back（写回）**。
  3. **存储器层次结构 (Memory Hierarchy)**：为什么要有 Register $\rightarrow$ Cache $\rightarrow$ RAM (主存) $\rightarrow$ Disk/Flash 的分级？RAM 和 ROM/Flash 的根本区别？
     - *破题*：为了平衡**速度、容量和成本**（局部性原理 Locality of Reference）。**RAM** (SRAM/DRAM) 是易失性的（Volatile，断电丢失）；**ROM/Flash** 是非易失性的（Non-volatile，断电保留）。
  4. **补码与二进制表示 (Two's Complement)**：计算机怎么表示负整数？为什么用补码？
     - *破题*：Two's complement = 反码 (One's complement, 按位取反) + 1。这样可以把**减法统一成加法**，让 ALU 只需设计加法器。
- 🟢 **可合理挡回的边界**：
  - 浮点数 IEEE 754 复杂阶码对阶手算、微程序控制器（Microprogramming）控制存储器编码细节、复杂 Cache 相联映射替换硬件电路。

---

### 3. Embedded C Language Programming（嵌入式 C 语言程序设计）
- **成绩单信息**：Fall 2023 | **3.0 学分** | **`75`**
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **指针的本质 (What is a Pointer?)**：什么是指针？`*p` 和 `&a` 分别代表什么？
     - *破题*：A pointer is a variable that stores a **memory address**. `&` 取变量地址（Address-of operator），`*` 解引用访问该地址里的值（Dereference operator）。
  2. **值传递 vs 地址/指针传递 (Pass by Value vs. Pass by Pointer)**：写一个 `swap(int *a, int *b)` 函数为什么必须传指针？
     - *破题*：Pass by value 只复制一份实参副本（copy），函数内修改不影响外部原变量；Pass by pointer 传递变量的内存地址，可以通过解引用直接修改外部变量或硬件寄存器。
  3. **内存分区：栈 vs 堆 (Stack vs. Heap)**：局部变量存在哪？`malloc` 分配的内存在哪？有什么区别？
     - *破题*：**Stack** 由编译器自动分配释放，存放局部变量和函数调用上下文，速度快但空间小；**Heap** 由程序员手动通过 `malloc()` / `free()` 动态分配，忘记 `free()` 会造成**内存泄漏 (Memory Leak)**。
  4. **嵌入式 C 特有必考：位运算 (Bitwise Operations) 与 `volatile` 关键字**：
     - 怎么把寄存器第 $n$ 位置 1 或清 0？（置 1：`reg |= (1 << n)`；清 0：`reg &= ~(1 << n)`）。
     - `volatile` 是干嘛的？（Tells the compiler **not to optimize** this variable and always read its value directly from memory, because it can be changed unexpectedly by hardware registers or an ISR）。
- 🟢 **可合理挡回的边界**：
  - 复杂的多级函数指针数组语法题、C 标准库底层实现源码。

---

### 4. Microcontroller Principles and Applications（单片机原理及应用）
- **成绩单信息**：Fall 2024 | **3.0 学分** | **`70`** | 已有草稿 [mcu_principle.md](file:///Users/al/Desktop/aps-prep/drafts/mcu_principle.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **MCU vs CPU (MPU)**：单片机（Microcontroller）和电脑里的处理器（Microprocessor）有什么区别？
     - *破题*：**MCU** is a single-chip computer (SoC) integrating CPU core, Flash (ROM), SRAM, and peripherals (GPIO, Timers, ADC, UART) on one chip for control tasks; **MPU/CPU** focuses on high computing power and requires external RAM, storage, and peripheral chips.
  2. **中断 vs 轮询 (Interrupt vs. Polling)**：什么是中断？为什么单片机不一直用 `while(1)` 轮询？
     - *破题*：**Polling** wastes CPU cycles constantly checking device status. **Interrupt** allows an external or internal event to pause the main program, execute an **ISR (Interrupt Service Routine)** immediately, and return, improving real-time response and CPU efficiency.
  3. **三大板级串行通信协议对比 (UART vs I2C vs SPI)**：**必考中的必考**，必须能脱口说出几根线、同步还是异步、全双工还是半双工：
     - **UART**：**2 根线** (`TX`, `RX`)，**异步 (Asynchronous，无时钟线，靠约定波特率 Baud Rate)**，**全双工 (Full-duplex)**，点对点。
     - **I2C**：**2 根线** (`SDA` 数据, `SCL` 时钟)，**同步 (Synchronous)**，**半双工 (Half-duplex)**，开漏输出需上拉电阻，支持多主多从（靠 7-bit 从机地址寻址）。
     - **SPI**：**4 根线** (`SCLK`, `MOSI`, `MISO`, `CS/SS` 片选)，**同步 (Synchronous)**，**全双工 (Full-duplex)**，速度最快，靠片选线选从机。
  4. **GPIO、定时器与 PWM / ADC 的基本原理**：
     - **PWM (脉冲宽度调制)**：通过调节方波的**占空比 (Duty Cycle = High time / Period，由 `CCR/ARR` 决定)**，用数字引脚等效控制模拟平均电压（如调光、控电机转速）。
     - **ADC (模数转换)**：把连续模拟电压（如 $0\sim3.3\text{V}$）采样量化为离散数字量（如 12-bit ADC 对应 $0\sim4095$）。
- 🟢 **可合理挡回的边界**：
  - 记住某一个偏门寄存器的具体十六进制地址或具体某一位缩写（只要能说清通过查 Reference Manual 或 CubeMX 配置寄存器即可）。

---

### 5. ARM Architecture and Programming + Course Project（ARM 体系结构与编程 + 课设）
- **成绩单信息**：Fall 2025 | **3.0 + 0.5 学分** | **`82` / `80`（近期高分核心课）** | 已有草稿 [arm_arch.md](file:///Users/al/Desktop/aps-prep/drafts/arm_arch.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **RISC vs CISC**：ARM 属于什么架构？和 x86 (CISC) 的本质区别是什么？
     - *破题*：ARM 是 **RISC (精简指令集 Reduced Instruction Set Computer)**：指令长度固定/规整、采用 **Load/Store 架构**（只有 `LDR`/`STR` 访问内存，运算都在寄存器间进行）、单周期执行为主、功耗低，非常适合嵌入式设备。
  2. **哈佛架构与流水线 (Harvard Architecture & Pipeline)**：Cortex-M3 为什么用哈佛架构？
     - *破题*：独立的指令总线（I-Code Bus）和数据总线（D-Code Bus），允许**同时取指和读写数据**，配合三级流水线（Fetch-Decode-Execute）大幅提升吞吐率。
  3. **核心特殊寄存器 (`PC`, `SP`, `LR`, `xPSR`) 与中断压栈流程**：
     - *破题*：`PC` (R15) 指向下一条要取的指令；`SP` (R13) 栈指针（分 `MSP` 主栈和 `PSP` 进程栈）；`LR` (R14) 链接寄存器，保存函数调用或中断的**返回地址**。发生中断时，NVIC 仲裁优先级（抢占优先级 Preemption vs 子优先级 Sub-priority），硬件自动将 `R0-R3, R12, LR, PC, xPSR` 压栈。
  4. **课设做了什么 (Course Project)**：必须能用 1 分钟说出你用 STM32 / Cortex-M 做了什么具体功能（用了哪些外设、中断怎么触发、数据怎么处理）。
- 🟢 **可合理挡回的边界**：
  - 手写大段复杂的 ARM 汇编算法程序（能看懂并解释 `MOV`, `LDR`, `STR`, `ADD`, `PUSH/POP`, `BX LR` 即可）。

---

### 6. Principles and Applications of Sensors（传感器原理及应用）
- **成绩单信息**：Spring 2025 | **3.0 学分** | **`75`** | 已有草稿 [sensor_principle.md](file:///Users/al/Desktop/aps-prep/drafts/sensor_principle.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **传感器的定义与完整信号链路 (Definition & Signal Chain)**：传感器把什么变成什么？为什么不能直接连 MCU？
     - *破题*：A sensor converts **non-electrical physical quantities** (temperature, pressure, light, magnetic field) into **electrical signals** (resistance, voltage, current, capacitance).
     - **完整链路（必画图）**：`Physical Signal` $\rightarrow$ `Sensor (微弱电信号/电阻变化)` $\rightarrow$ `Signal Conditioning Circuit (分压/惠斯通电桥/运放放大/滤波)` $\rightarrow$ `ADC` $\rightarrow$ `MCU`。
  2. **至少熟记 2 种典型传感器的物理原理**：
     - **温度传感器 (NTC Thermistor)**：负温度系数热敏电阻，温度升高 $\rightarrow$ 半导体载流子增加 $\rightarrow$ 电阻下降；通过串联分压电路将电阻变化转化为电压变化送给 ADC。
     - **霍尔传感器 (Hall Effect) / 压电传感器 (Piezoelectric) / 光电传感器**：能用一两句话说出对应的物理效应（如霍尔效应：通电导体在垂直磁场中产生横向霍尔电压）。
- 🟢 **可合理挡回的边界**：
  - 传感器材料掺杂的半导体固体物理公式或复杂非线性补偿多项式系数的数学拟合推导。

---

### 7. EDA (Electronic Design Automation) + Course Project（电子设计自动化 + 课设）
- **成绩单信息**：Fall 2025 | **3.0 + 0.5 学分** | **`61` / `89`（理论与课设分差大，高频追问点）** | 已有草稿 [eda.md](file:///Users/al/Desktop/aps-prep/drafts/eda.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **PCB 设计全流程 (Schematic to PCB Workflow)**：你们用 EDA 工具（立创 EDA / Altium）做一块电路板的标准步骤是什么？
     - *破题*：`Component Library (Schematic Symbol + PCB Footprint)` $\rightarrow$ `Schematic Design (原理图绘制)` $\rightarrow$ `ERC (电气规则检查)` $\rightarrow$ `Netlist (网表导入)` $\rightarrow$ `PCB Layout & Routing (布局与布线)` $\rightarrow$ `DRC (设计规则检查)` $\rightarrow$ `Gerber File Export & Soldering`。
  2. **原理图符号 vs PCB 封装 (Symbol vs. Footprint) & ERC vs DRC**：
     - *破题*：**Schematic Symbol** 只是逻辑连接符号；**Footprint (封装)** 是芯片真实物理尺寸和焊盘间距（如 QFN-40、0805 贴片电阻），必须严格查 Datasheet。**ERC** 检查电气逻辑错误（如引脚悬空、电源短路）；**DRC** 检查物理制造约束（如线距过近、过孔重叠）。
  3. **PCB 布线基本常识**：为什么电源线要比信号线宽？（承载电流更大，减小阻抗和压降）；为什么要覆铜（GND Copper Pour）？（提供低阻抗回流路径、抗干扰屏蔽、辅助散热）。
- 🟢 **可合理挡回的边界**：
  - *注意区分*：德国大学有些教授看到 EDA 会联想到 **FPGA / Verilog / VHDL 芯片综合**。如果考官问起 Verilog/FPGA，千万别慌，直接清晰说明：*"In our curriculum, the EDA course focused on **board-level PCB design** (schematic capture, footprint creation, and 4-layer STM32 PCB layout using LC-EDA) rather than IC-level FPGA/Verilog synthesis."*（这是完全正统且合理的解释！）

---

## 二、第二模块：计算机核心与系统软件 (CS Core & System Software)

### 8. Operating Systems（操作系统）
- **成绩单信息**：Fall 2025 | **3.5 学分** | **`60(Resit1)`** ⚠️ *头号必考重灾区* | 已有笔记 [op_system.md](file:///Users/al/Desktop/aps-prep/notes/op_system.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **进程 vs 线程 (Process vs. Thread)**：**APS 计算机类第一高频题**。
     - *破题*：**Process** is the basic unit of **resource allocation** (has its own independent virtual address space). **Thread** is the basic unit of **CPU scheduling and execution**. Threads within the same process share the code, data, and heap, but each has its own **independent Stack and Registers (PC/SP)**, making thread context switching much faster.
  2. **进程三态/五态转换与调度算法 (Process States & CPU Scheduling)**：
     - *破题*：**Ready（就绪）$\leftrightarrow$ Running（运行）$\rightarrow$ Blocked/Waiting（阻塞，等待 I/O 或事件）**。注意：`Blocked` 状态**不能**直接跳回 `Running`，必须先回到 `Ready` 队列等调度器分配 CPU！常见调度算法：FCFS、SJF、Round-Robin（时间片轮转）、Priority Scheduling（抢占式优先级调度）。
  3. **同步互斥与死锁四条件 (Mutex/Semaphore & Deadlock)**：
     - 什么是临界区（Critical Section）和竞态条件（Race Condition）？用 **Mutex（互斥锁）** 和 **Semaphore（信号量，P/V 操作）** 解决。
     - **死锁 (Deadlock) 的四个必要条件**：① **Mutual Exclusion**（互斥）、② **Hold and Wait**（请求与保持）、③ **No Preemption**（不可剥夺）、④ **Circular Wait**（循环等待）。
  4. **虚拟内存与分页 (Virtual Memory & Paging)**：为什么需要虚拟内存？逻辑地址怎么变成物理地址？
     - *破题*：让每个进程以为自己独占连续的大内存，并提供内存隔离保护。通过 **Paging（分页）**：将虚拟内存分为固定大小的 Page，物理内存分为 Frame，由硬件 **MMU** 查 **Page Table（页表，配合 TLB 快表）** 完成地址转换；缺页时触发 Page Fault 进行页面置换（如 **LRU** 最近最少使用、FIFO）。
  5. **物联网专业必联考点：通用 OS (Linux) vs 实时操作系统 (RTOS, 如 FreeRTOS)**：
     - *破题*：Linux 追求高吞吐量（Throughput），需要 MMU；**RTOS** 运行在资源受限的 MCU 上，核心指标是**确定性 (Determinism)**，即任务和中断必须在严格的时间上限（Deadline）内响应，采用基于优先级的抢占式调度（Preemptive Priority Scheduling）。
- 🟢 **可合理挡回的边界**：
  - Linux 内核具体某一个系统调用的 C 源码实现、复杂磁盘调度或多级页表字节级计算、手算复杂的银行家算法大矩阵。

---

### 9. Data Structure and Algorithms（数据结构与算法）
- **成绩单信息**：Fall 2025 | **3.5 学分** | **`75(Retake1)`** ⚠️ *重修核心课，必查* | 已有草稿 [data_structure_algorithms.md](file:///Users/al/Desktop/aps-prep/drafts/data_structure_algorithms.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **数组 vs 链表 (Array vs. Linked List)**：内存分布和时间复杂度有什么区别？
     - *破题*：**Array**：内存连续（contiguous memory），支持下标随机访问 `O(1)`，但中间插入/删除需移动元素 `O(n)`；**Linked List**：内存离散，靠指针连接，按值查找 `O(n)`，但已知节点位置时插入/删除只需改指针 `O(1)`。
  2. **栈 vs 队列 (Stack vs. Queue)**：特点和典型应用场景？
     - *破题*：**Stack** 是 **LIFO**（后进先出，用于函数调用栈、中断现场保护、表达式求值）；**Queue** 是 **FIFO**（先进先出，用于 BFS 广度优先搜索、串口接收环形缓冲区 Ring Buffer、OS 任务就绪队列）。
  3. **二叉树与二叉搜索树 (Binary Tree & BST)**：
     - 什么是 BST？（左子树所有节点 $<$ 根节点 $<$ 右子树所有节点，平均查找 `O(log n)`，退化成单支链时 `O(n)`，所以需要通过旋转平衡，如 AVL 树）。
     - 三种深度遍历顺序：**Pre-order**（根左右）、**In-order**（左根右，BST 中序遍历输出**有序序列**！）、**Post-order**（左右根）。
  4. **哈希表与冲突解决 (Hash Table & Collision Resolution)**：
     - *破题*：通过 Hash Function 将 Key 映射为数组下标，平均查找 `O(1)`。不同 Key 映射到同一位置叫 **Collision（哈希冲突）**，解决方法：① **Chaining（拉链法，挂链表）**；② **Open Addressing（开放定址法，如线性探测 Linear Probing）**。
  5. **基础排序与图遍历 + 时间复杂度 (`Big-O` Notation)**：
     - 能口述并在纸上演示至少一种 `O(n^2)` 排序（如冒泡 Bubble Sort / 插入 Insertion Sort）和一种 `O(n log n)` 排序（如快速排序 Quick Sort 的分治 Partition 思想或归并排序 Merge Sort）。
     - 图的两种表示（邻接矩阵 Adjacency Matrix vs 邻接表 Adjacency List）、两种遍历（**BFS** 用队列 vs **DFS** 用栈/递归）及 **Dijkstra 最短路径**基本贪心思想。
- 🟢 **可合理挡回的边界**：
  - 手写红黑树（Red-Black Tree）五条性质的复杂双旋转删除代码、动态规划（DP）高难竞赛题。

---

### 10. Introduction to Database Systems（数据库系统概论）
- **成绩单信息**：Fall 2024 | **3.5 学分** | **`63`（低分核心课）** ⚠️ | 已有笔记 [database.md](file:///Users/al/Desktop/aps-prep/notes/database.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **主键 vs 外键 (Primary Key vs. Foreign Key) & E-R 图转表**：
     - *破题*：**Primary Key (PK)** 唯一标识表中的每一行（非空且唯一 `NOT NULL & UNIQUE`）；**Foreign Key (FK)** 引用另一张表的主键，用于建立表间关联并保证**参照完整性 (Referential Integrity)**。多对多（`M:N`）关系必须新建一张**中间关联表**（包含两个外键）。
  2. **手写基础 SQL 查询 (Basic SQL)**：考官给两张表（如 `Sensors` 和 `Readings`），必须能当场在纸上手写出：
     - `SELECT ... FROM ... JOIN ... ON ... WHERE ... GROUP BY ... HAVING ...`
     - 区分 `WHERE`（分组前过滤行）和 `HAVING`（分组后过滤聚合结果）。
  3. **数据库三大范式 (Normalization: 1NF, 2NF, 3NF)**：为什么需要范式？（消除数据冗余 Data Redundancy 和增删改异常 Update/Insert/Delete Anomalies）。
     - **1NF**：每个字段都是不可再分的**原子值 (Atomic values)**。
     - **2NF**：满足 1NF，且消除非主属性对联合主键的**部分依赖 (No Partial Dependency)**。
     - **3NF**：满足 2NF，且消除非主属性之间的**传递依赖 (No Transitive Dependency)**。
  4. **事务与 ACID 四大特性 (Transaction & ACID)**：
     - **A**tomicity（原子性：要么全成功，要么全回滚 Rollback）、**C**onsistency（一致性）、**I**solation（隔离性：并发事务互不干扰）、**D**urability（持久性：提交后永久落盘）。
  5. **索引的作用 (Why Index?)**：为什么加索引查询会变快？（通常基于 **B+ 树**，把全表扫描 `O(n)` 降为树查找 `O(log n)`，代价是占用额外空间且拖慢写入 `INSERT/UPDATE`）。
- 🟢 **可合理挡回的边界**：
  - 关系代数演算符号推导、ARJ/ARIES 日志恢复算法底层细节、多版本并发控制（MVCC）源码实现。

---

### 11. Compilation Techniques（编译技术）
- **成绩单信息**：Spring 2026 | **2.5 学分** | **`76`（最新学期课程）**
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **编译器 vs 解释器 (Compiler vs. Interpreter)**：C 语言和 Python 的执行方式有什么本质区别？
     - *破题*：**Compiler**（如 C 的 `gcc`）在运行前把整个源代码一次性翻译成机器码（Executable Machine Code），执行速度快；**Interpreter**（如 Python）在运行时逐行读取并翻译执行，跨平台灵活但运行较慢。
  2. **编译器的核心阶段流水线 (The 6 Phases of Compilation)**：**必背流程，能画框图**！
     - **前端 (Front-end，与源语言相关)**：
       1. **Lexical Analysis（词法分析）**：把源代码字符流切分成一个个单词符号 **Tokens**（基于正则表达式 Regular Expression 和有限自动机 NFA/DFA）。
       2. **Syntax Analysis（语法分析）**：根据上下文无关文法（CFG），把 Tokens 组织成 **语法树 (Parse Tree / AST, Abstract Syntax Tree)**，检查括号不匹配等语法错误。
       3. **Semantic Analysis（语义分析）**：利用符号表（Symbol Table）做**类型检查 (Type Checking)**（如检查是否把字符串赋给了整型变量）。
     - **中间与后端 (Middle & Back-end，与目标架构相关)**：
       4. **Intermediate Code Generation（中间代码生成）**：生成与机器无关的中间表示（如三地址码 Three-Address Code）。
       5. **Code Optimization（代码优化）**：消除冗余计算（如常量折叠、死代码消除）。
       6. **Target Code Generation（目标代码生成）**：生成目标架构（如 x86 或 ARM）的汇编/机器指令并分配寄存器。
  3. **能随手画一个简单表达式的 AST**：比如 `a = b + c * 2`，在纸上画出赋值节点 `=`、加号 `+`、乘号 `*`（体现 `*` 优先级高于 `+`，所以在树の下层）。
- 🟢 **可合理挡回的边界**：
  - 手工构造复杂的 `LR(1)` / `LALR` 分析表、计算大段文法的 `FIRST` 和 `FOLLOW` 集合、图着色寄存器分配算法细节。
  - *话术*：*"As an IoT Engineering major, this was a 2.5-credit introductory course where we focused on the overall 6-stage compilation pipeline, regular expressions/automata, and how C code is cross-compiled into ARM assembly, rather than building complex LR(1) parser generators by hand."*

---

## 三、第三模块：网络与物联网通信 (Network & IoT Communication)

### 12. Computer Networks（计算机网络）
- **成绩单信息**：Spring 2025 | **3.5 学分** | **`68`（偏低分核心课）** ⚠️ | 已有草稿 [computer_networks.md](file:///Users/al/Desktop/aps-prep/drafts/computer_networks.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **五层（或 OSI 七层）网络体系结构及各层代表协议与数据单元**：
     - **Application Layer**（HTTP, DNS, MQTT；数据单元：**Message**）
     - **Transport Layer**（TCP, UDP；负责进程到进程端到端通信，靠 **Port 端口号** 区分应用；数据单元：**Segment**）
     - **Network Layer**（IP, ICMP, Routing；负责跨网络主机到主机寻址与路由，靠 **IP 地址**；数据单元：**Packet / Datagram**）
     - **Data Link Layer**（Ethernet, ARP, CRC；负责同一局域网相邻节点传输，靠 **MAC 地址**；数据单元：**Frame**）
     - **Physical Layer**（传输比特流 **Bits**）。
  2. **TCP vs UDP & TCP 三次握手 (3-Way Handshake)**：
     - **TCP**：面向连接（Connection-oriented）、可靠传输（确认重传、流量控制、拥塞控制）、面向字节流；**UDP**：无连接（Connectionless）、尽最大努力交付、首部开销小、低延迟（适合实时音视频或轻量级物联网报文）。
     - **三次握手（必画图）**：`SYN (seq=x)` $\rightarrow$ `SYN+ACK (seq=y, ack=x+1)` $\rightarrow$ `ACK (seq=x+1, ack=y+1)`。为什么要第三次握手？（确认客户端具备接收能力，并防止已失效的历史连接请求突然到达服务器造成资源浪费）。
  3. **IP 地址、子网掩码 (Subnet Mask)、默认网关 (Default Gateway)、ARP 与 DNS**：
     - **Subnet Mask**：通过与 IP 地址做按位与（Bitwise AND）划分 **Network ID（网络号）** 和 **Host ID（主机号）**，判断目标主机是否在同一个子网内；如果不在同一子网，数据包必须发给 **Default Gateway（路由器）** 转发。
     - **DNS**：把域名（Domain Name）解析为 IP 地址；**ARP**：在同一局域网内通过广播，根据已知的 **IP 地址** 查询目标设备的 **MAC 地址**。
- 🟢 **可合理挡回的边界**：
  - BGP 自治系统跨国路由策略细节、TCP 拥塞控制（Reno/CUBIC）复杂状态机参数推导、IPv6 扩展报头逐字节格式。

---

### 13. Internet of Things Communication Technologies + Practices（物联网通信技术 + 实践）
- **成绩单信息**：Spring 2026 | **3.0 + 2.0 学分** | **`81` / `86`（最新学期高分主干课）** | 已有草稿 [iot_communication.md](file:///Users/al/Desktop/aps-prep/drafts/iot_communication.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **主流物联网无线协议的多维对比 (ZigBee vs. Wi-Fi vs. BLE vs. NB-IoT/LoRa)**：**物联网专业招牌必考题**！必须能从 **传输距离 (Range)、功耗 (Power Consumption)、传输速率 (Data Rate)、是否需要基站/网关** 四个维度说清楚选型原因：
     - **Wi-Fi**：高带宽、高功耗、短距离，适合传视频或直连互联网，不适合纽扣电池供电节点。
     - **BLE (低功耗蓝牙)**：低功耗、短距离，优势在于**手机原生支持**，适合穿戴设备点对点通信。
     - **ZigBee (基于 IEEE 802.15.4)**：低功耗、低速率、短距离，最大优势是支持**自组织 Mesh 网状拓扑 (Self-healing Mesh Network)**，适合智能家居/工业密集传感器组网。
     - **NB-IoT / LoRa (LPWAN 低功耗广域网)**：超远距离（数公里）、极低功耗、极低速率。NB-IoT 工作在授权频谱（依托运营商蜂窝基站）；LoRa 工作在非授权频谱（自建网关）。
  2. **ZigBee 三种设备角色与三种网络拓扑（结合你的 CC2530 实验）**：
     - **三种逻辑角色**：**Coordinator (ZC，协调器，全网唯一，负责建网和分配地址)**、**Router (ZR，路由器，负责转发和允许子节点入网)**、**End Device (ZED，终端节点，可休眠省电，不能转发数据)**。
     - **三种拓扑**：**Star（星型）**、**Tree（树型）**、**Mesh（网状）**。
- 🟢 **可合理挡回的边界**：
  - 物理层正交频分复用（OFDM）或直接序列扩频（DSSS）的复杂积分数学推导。

---

### 14. Industrial Internet Identification and Resolution Technology（工业互联网标识解析技术）
- **成绩单信息**：Spring 2026 | **3.0 学分** | **`81`** | 已有草稿 [industrial_internet_id.md](file:///Users/al/Desktop/aps-prep/drafts/industrial_internet_id.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  > *注：这门课名字很长且在最新学期，考官大概率会问一句：“What is this course about?”*
  1. **一句话定位（物理世界的 DNS）**：
     - *破题*：It acts like the **DNS (Domain Name System) for physical industrial devices and products**. We assign a globally unique, persistent ID (like the **Handle System**: `Prefix/Suffix`, e.g., `88.12345/Device-001`) to every hardware node or product, attach it via **QR Code or RFID**, and resolve that ID through a hierarchical node system (Root Node $\rightarrow$ National/Industry Node $\rightarrow$ Enterprise Node) to locate its lifecycle data or real-time monitoring API across different factories.
  2. **RFID vs 二维码 (QR Code)**：
     - **QR Code**：光学识别，成本极低，但需要**视线可见 (Line-of-Sight)** 且只能逐个扫描；**RFID**：射频识别（通过电磁耦合/反向散射，无源标签无需电池），支持**非视距穿透读取和批量防碰撞识别**，耐油污恶劣环境。
- 🟢 **可合理挡回的边界**：
  - 国家顶级节点底层密码学认证协议或大规模分布式异构标识同步协议规范细节。

---

### 15. Introduction to Internet of Things / IoT Technology（物联网导论 / 物联网技术导论）
- **成绩单信息**：Fall 2023 (`2.0 cr, 85`) & Fall 2024 (`3.0 cr, 69`)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **什么是物联网 (What is IoT?) & 经典三层架构 (The 3-Layer Architecture of IoT)**：
     - **Perception Layer（感知层）**：传感器、RFID、MCU（STM32/CC2530），负责采集物理世界的数据并执行控制动作。
     - **Network Layer（网络层）**：短距无线（ZigBee/BLE/Wi-Fi）通过物联网网关（Gateway）接入互联网/移动蜂窝网（4G/5G/NB-IoT），负责数据可靠传输。
     - **Application Layer（应用层）**：云平台、数据库、机器学习分析、Web 前端看板与嵌入式 GUI，负责数据处理与用户交互。
- 🟢 **可合理挡回的边界**：
  - 这两门本身就是导论概述课，把问题自然引导到你具体的传感器、ARM、ZigBee 或 GUI 课程即可。

---

## 四、第四模块：应用层、GUI 与数据智能 (Application, GUI & Data Science)

### 16. Embedded GUI Development and Applications（嵌入式 GUI 开发及应用）
- **成绩单信息**：Spring 2026 | **2.0 学分** | **`88`（最新学期最高分专业课之一）** | 已有草稿 [embedded_gui.md](file:///Users/al/Desktop/aps-prep/drafts/embedded_gui.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **嵌入式 GUI (LVGL) 与 PC/Web GUI 的最大区别（资源受限与显存策略）**：
     - *破题*：MCU 的 SRAM 非常小（几十 KB），放不下一整帧屏幕图像（Full-frame buffer），因此采用 **脏矩形局部刷新 (Dirty Rectangle)** + **局部双缓冲 (Partial Ping-Pong Double Buffering)**（CPU 渲染 Buffer A 时，DMA 把 Buffer B 刷到屏幕），并用 **RGB565 (2 Bytes/pixel)** 代替 RGB888 节省内存和传输带宽。
  2. **事件驱动机制 (Event-Driven Architecture)**：
     - *破题*：定时器中断提供系统时基（`lv_tick_inc`），主循环周期调用 `lv_timer_handler()` 读取触摸输入、重绘脏区域并触发绑定在控件（Widgets）上的**事件回调函数 (Callback Function)**。
- 🟢 **可合理挡回的边界**：
  - LVGL 底层抗锯齿矢量图形光栅化数学算法源码。

---

### 17. Front-End Development Technologies（前端开发技术）
- **成绩单信息**：Fall 2025 | **3.0 学分** | **`72`** | 已有草稿 [front_end.md](file:///Users/al/Desktop/aps-prep/drafts/front_end.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **前端三剑客各自职责 (HTML vs. CSS vs. JavaScript)**：
     - **HTML**：网页的骨架与语义结构（解析为 **DOM Tree**）。
     - **CSS**：样式与布局（**Box Model 盒模型**：`Content` $\rightarrow$ `Padding` $\rightarrow$ `Border` $\rightarrow$ `Margin`，以及 **Flexbox** 弹性布局）。
     - **JavaScript**：动态交互逻辑（通过操作 DOM 节点和 `addEventListener` 监听用户事件，或用异步请求更新页面数据）。
- 🟢 **可合理挡回的边界**：
  - 复杂的 React/Vue 虚拟 DOM Diff 算法源码、Webpack 打包底层机制（明确说明作为物联网专业，学前端主要是为了给物联网系统做轻量级监控仪表盘 Web Dashboard 即可）。

---

### 18. Python-Based Machine Learning（基于 Python 的机器学习）
- **成绩单信息**：Spring 2026 | **2.0 学分** | **`82`** | 已有草稿 [machine_learning.md](file:///Users/al/Desktop/aps-prep/drafts/machine_learning.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **监督学习 vs 无监督学习 (Supervised vs. Unsupervised Learning)**：
     - **Supervised**：训练数据**有标签 (Labeled data)**，分两类任务——**Regression（回归，预测连续值，如线性回归预测温度/房价）** 和 **Classification（分类，预测离散类别，如 KNN、SVM、朴素贝叶斯）**。
     - **Unsupervised**：训练数据**无标签 (Unlabeled data)**，如 **K-Means 聚类 (Clustering)**，根据距离自动把相似样本聚成 $K$ 簇。
  2. **训练集 / 测试集划分与过拟合 (Train/Test Split & Overfitting)**：
     - 为什么要把数据分成 Training Set 和 Test Set？（评估模型对未知数据的**泛化能力 Generalization**）。
     - 什么是 **Overfitting（过拟合）**？（模型把训练集的噪声也死记硬背下来了，在训练集上准确率极高，但在测试集上表现很差；可通过增加数据、简化模型或正则化 Regularization 缓解）。
  3. **损失函数与梯度下降 (Loss Function & Gradient Descent)** + **至少能口述 1 个分类算法（如 KNN 或 SVM）和 K-Means 的步骤**：
     - 线性回归用均方误差 **MSE** 作为 Loss，沿梯度的反方向（Negative Gradient）迭代更新权重以最小化 Loss。
- 🟢 **可合理挡回的边界**：
  - SVM 拉格朗日对偶问题与 KKT 条件的完整黑板数学证明、深度神经网络反向传播矩阵求导链式展开（这只是 2 学分的 Python 机器学习入门课）。

---

### 19. Data Visualization and Intelligent Analysis（数据可视化与智能分析）
- **成绩单信息**：Spring 2026 | **3.0 学分** | **`88`** | 已有草稿 [data_visualization.md](file:///Users/al/Desktop/aps-prep/drafts/data_visualization.md)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **数据分析与可视化标准流水线 (Data Analysis Pipeline)**：
     - **Step 1: Data Cleaning (Pandas)** —— 处理缺失值（`dropna` / `fillna`）、去重（`drop_duplicates`）、类型转换、分组聚合（`groupby` + `mean/sum`）。
     - **Step 2: Chart Selection (Matplotlib)** —— 根据分析目的选图：**折线图 (Line chart)** 看随时间变化趋势（Time-series trend）；**柱状图 (Bar chart)** 看不同类别对比；**散点图 (Scatter plot)** 看两个变量的相关性（Correlation）；**直方图 (Histogram)** 看数据分布（Distribution）。
- 🟢 **可合理挡回的边界**：
  - 复杂的商业 BI 平台架构或高维流形降维可视化数学推导。

---

### 20. Java Programming & Python Programming（Java 程序设计 & Python 程序设计）
- **成绩单信息**：Java (Spring 2025, `3.0 cr, 73`) | Python (Fall 2025, `3.0 cr, 86`)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **Java — 面向对象编程三大特性 (3 Pillars of OOP)**：**必背概念**！
     - **Encapsulation（封装）**：把数据（`private` 属性）和操作数据的方法捆绑在类（Class）中，隐藏内部细节，通过 `public` 方法访问。
     - **Inheritance（继承，`extends`）**：子类复用父类的属性和方法，并扩展新功能。
     - **Polymorphism（多态）**：同一接口/父类引用指向不同子类对象时，调用重写（Override）的方法表现出不同的行为。
     - **Class vs Object**：Class 是模板/蓝图（Blueprint），Object 是根据类实例化出来的具体实体（Instance）。
  2. **Python — 核心内置数据结构与特点**：
     - 动态类型解释型语言；四大内置容器的区别：**List (`[]`，有序可变)**、**Tuple (`()`，有序不可变 Immutable)**、**Dict (`{k:v}`，键值对哈希映射，查找快)**、**Set (`{}`，无序不重复元素集)**。
- 🟢 **可合理挡回的边界**：
  - Java JVM 字节码类加载双亲委派底层细节或垃圾回收器（G1/ZGC）调优参数、Python 元编程与 GIL 底层 C 源码。

---

## 五、第五模块：数学基础课 (Mathematics Fundamentals — 5 门)

> **APS 数学考察特点**：对于工科生，考官很少单独花 10 分钟考纯数学证明；**但你的高数 A1 (`60 Resit1`)、高数 A2 (`60 Resit1`)、线代 (`72 Retake1`)、离散 (`60`)、概率论 (`64`) 分数普遍偏低且有补考/重修**。考官极可能会随口问一个最基础的数学概念，来测试你是不是“完全没学懂就混过去了”。以下底线概念必须张口就来：

### 21. Advanced Mathematics A1 & A2（高等数学 A1 & A2）
- **成绩单信息**：A1 (Spring 2024, `4.0 cr, 60 Resit1`) | A2 (Fall 2024, `4.0 cr, 60 Resit1`)
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **导数 (Derivative) 的几何意义与应用**：
     - 几何意义：函数曲线在某一点的**切线斜率 (Slope of the tangent line)**，代表瞬时变化率（Rate of change）。当一阶导数 $f'(x) = 0$ 时用于求函数的**极值点 (Local Maximum / Minimum)**。
  2. **定积分 (Definite Integral) 的几何意义**：
     - 几何意义：函数曲线与坐标轴围成的**有向面积 (Area under the curve)**。微积分基本定理（牛顿-莱布尼茨公式）：积分是求导的逆运算，$\int_a^b f(x)dx = F(b) - F(a)$。
  3. **偏导数与梯度 (Partial Derivative & Gradient —— A2 核心)**：
     - 多元函数对其中一个变量求导（把其他变量看作常数）叫 **Partial Derivative**；所有偏导数组成的向量叫 **Gradient（梯度）**，指向函数值**增长最快的方向**（所以在机器学习中沿着负梯度方向做 Gradient Descent 找最小值）。

### 22. Linear Algebra（线性代数）
- **成绩单信息**：Fall 2025 | **4.0 学分** | **`72(Retake1)`**
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **矩阵乘法条件与逆矩阵 (Matrix Multiplication & Inverse)**：
     - 矩阵 $A_{m \times n}$ 和 $B_{n \times p}$ 相乘，必须满足 **$A$ 的列数等于 $B$ 的行数**，结果是 $m \times p$（且通常 $AB \neq BA$）。
     - 方阵可逆（Invertible, $A A^{-1} = I$）的充要条件是其**行列式不等于 0 ($\det(A) \neq 0$，即满秩 Full Rank)**。
  2. **特征值与特征向量 (Eigenvalues & Eigenvectors)**：
     - 定义公式：**$A\mathbf{x} = \lambda\mathbf{x}$**（其中 $\mathbf{x} \neq \mathbf{0}$）。几何直观：矩阵 $A$ 对特征向量 $\mathbf{x}$ 进行线性变换时，**只改变它的长度（缩放 $\lambda$ 倍），不改变它的方向**。

### 23. Probability Theory and Mathematical Statistics（概率论与数理统计）
- **成绩单信息**：Fall 2024 | **4.0 学分** | **`64`**
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **数学期望 (Expectation / Mean) 与方差 (Variance)**：
     - **Expectation $E(X)$**：随机变量取值的加权平均值（反映数据的中心位置）；**Variance $Var(X) = E[(X - E(X))^2]$**：反映数据偏离均值的**离散/波动程度 (Spread / Volatility)**，开根号即为标准差（Standard Deviation $\sigma$）。
  2. **条件概率与贝叶斯公式 (Conditional Probability & Bayes' Theorem)**：
     - $P(A|B) = \frac{P(AB)}{P(B)}$；贝叶斯定理：$P(A|B) = \frac{P(B|A)P(A)}{P(B)}$（根据已知结果反推原因的后验概率，是朴素贝叶斯分类器的数学基础）。
  3. **正态分布 (Normal / Gaussian Distribution)**：钟形曲线（Bell-shaped curve），由均值 $\mu$（决定对称轴位置）和方差 $\sigma^2$（决定胖瘦高矮）完全决定。

### 24. Discrete Mathematics（离散数学）
- **成绩单信息**：Spring 2024 | **3.0 学分** | **`60`**
- 🔴 **绝对底线（答不上来 = 漏洞）**：
  1. **命题逻辑基本联结词 (Propositional Logic)**：合取（AND, $\wedge$）、析取（OR, $\vee$）、否定（NOT, $\neg$）、蕴含（Implication, $P \rightarrow Q$，只有“前真后假”时才为假）。
  2. **集合运算与图论基础概念 (Sets & Graph Theory)**：并集（Union $\cup$）、交集（Intersection $\cap$）、差集；图 $G = (V, E)$ 由顶点集（Vertices）和边集（Edges）组成，树（Tree）是**连通且无环的无向图 (Connected acyclic undirected graph)**（直接衔接《数据结构》）。

---

## 六、附：考场“合理挡回 vs 致命踩雷”黄金话术模板

### ❌ 绝对不能说的踩雷话术（考官立刻警觉）
- *"Sorry, I got 60 in this course so I forgot everything."*（忌讳：承认自己完全没掌握）
- *"Our teacher didn't teach what a pointer / TCP handshake / Kirchhoff's law is."*（忌讳：违背常识，任何大学讲这门课都不可能不讲）

### ✅ 遇到超纲/非本专业深水区问题时的“先守住底线、再优雅挡回”公式
> **公式 = 【第 1 句：立刻答出该概念所属的基础底线定义，证明你真学过】 + 【第 2 句：说明物联网工程专业在这门课上的实际侧重点/实验内容，把话题引向你的强项】**

- **示例 1（当《编译技术》被问到复杂的 LR 分析表构造时）**：
  > *"LR parsing belongs to the **Syntax Analysis** phase of a compiler, which builds a **Parse Tree / AST** from tokens based on a Context-Free Grammar. In our IoT Engineering program, this 2.5-credit course focused on the overall 6-stage compilation pipeline and how C code is cross-compiled and optimized into ARM instructions, rather than manually constructing complex LR(1) state tables."*
- **示例 2（当《电路与电子技术》被问到复杂的三极管高频微变等效电路计算时）**：
  > *"A transistor mainly works in two modes: **amplification** in the active region and **electronic switching** between cutoff and saturation. Because our course combined circuit theory, analog, and digital electronics into one semester for IoT students, we mainly focused on fundamental laws like **KCL/KVL**, **Op-Amp signal conditioning for sensors**, and **MOSFET switching circuits for MCUs**, rather than complex high-frequency small-signal modeling."*
- **示例 3（当《数据库》被问到复杂的底层 B+ 树分裂或日志恢复算法时）**：
  > *"An index uses a **B+ Tree** structure to speed up queries from full-table scan `O(n)` to `O(log n)`, and transaction recovery relies on the **ACID** properties. In our coursework, we primarily focused on **E-R modeling, 1NF to 3NF normalization, and writing SQL JOIN/GROUP BY queries** to store and analyze IoT sensor data."*
