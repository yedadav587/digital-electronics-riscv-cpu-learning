8位极简CPU设计（7天从零实现）- GitHub仓库笔记

8bit-Mini-CPU

7天从零设计8位极简单周期CPU，纯Logisim画图仿真（无FPGA、无硬件），适配数电学习进度，兼顾数电知识点巩固与CPU设计实践，最终可跑简单汇编程序。

📚 项目介绍

- 核心目标：设计一款8位、单周期、RISC架构CPU，可仿真、能跑基础汇编指令，巩固数电（组合逻辑、时序逻辑）与计算机组成原理基础。

- 实现方式：优先用 Logisim Evolution 画图（纯数电门电路，不用写代码），后续可扩展 Verilog 版本。

- 适配进度：对应数电学习（Day01数制→Day10简易CPU+RV32I入门），边学数电边做CPU，每天1小时，7天完成。

- 最终效果：能运行 `mov`/`add`/`sub`/`and`/`or`/`jmp` 指令，直观看到寄存器、ALU、PC的工作过程。

🔧 环境准备

必备软件

- 仿真工具：Logisim Evolution（推荐版本：v3.16.1）

- 辅助工具：VS Code（整理笔记、编写汇编）、GitHub Desktop（上传仓库）

软件安装

1. Logisim Evolution：从上述链接下载对应系统版本（Windows/macOS/Linux），无需安装，解压即可运行。

2. 汉化（可选）：将汉化包放入软件根目录，重启即可（仓库内可放置汉化文件）。

📂 仓库目录结构

8bit-Mini-CPU/
├── README.md               # 项目总览、导航、注意事项
├── 00-Environment/         # 环境准备（Logisim安装包、汉化包）
├── 01-ALU/                 # Day01：8位ALU设计（图纸、笔记）
├── 02-PC-IR-IM/            # Day02：PC、IR、指令存储器设计
├── 03-RegFile/             # Day03：寄存器堆设计
├── 04-DataPath/            # Day04：数据通路拼接
├── 05-ControlUnit/         # Day05：控制单元CU设计
├── 06-FullCPU/             # Day06：完整CPU拼接
├── 07-Debug-Run/           # Day07：调试、运行汇编程序
├── Doc/                    # 补充文档（指令集、数电对应关系）
│   ├── InstructionSet.md   # 7条极简指令集详解
│   ├── DigitalLogic-CPU.md # 数电知识点与CPU模块对应表
│   └── RISC-V-RV32I.md     # 向RV32I延伸说明
└── Logisim-Files/          # 所有Logisim仿真文件（按天数分类）

📅 7天任务导航（每日1小时）

天数

核心任务

数电知识点

成果物

Day01

搭建环境 + 设计8位ALU

全加器、MUX、组合逻辑

8位ALU Logisim图纸

Day02

设计PC、IR、指令存储器IM

计数器、寄存器、ROM

取指通路模块图纸

Day03

设计寄存器堆RegFile

寄存器阵列、译码器

2-4个通用寄存器模块

Day04

拼接RegFile→ALU→写回通路

数据通路、MUX选择

执行通路完整图纸

Day05

设计控制单元CU

指令译码、组合逻辑

控制信号生成模块

Day06

拼接完整CPU + 实现跳转

时序逻辑、模块级联

完整CPU Logisim图纸

Day07

调试CPU + 运行汇编程序

仿真调试、指令执行流程

可运行的CPU仿真文件

📖 核心文档详情

1. InstructionSet.md（7条极简指令集）

采用8位指令格式：高4位为操作码（opcode），低4位为立即数/寄存器编号，适配8位CPU字长。

指令

功能描述

opcode（高4位）

低4位含义

示例

NOP

空操作，不执行任何指令

0000

无意义（可填0000）

00000000

MOV Rd, #imm

立即数imm送入寄存器Rd

0001

Rd（2位） + imm（2位）

00010010（R0=2）

ADD Rd, Rs1, Rs2

Rd = Rs1 + Rs2

0010

Rd（2位）+ Rs1（1位）+ Rs2（1位）

00101001（R1=R0+R3）

SUB Rd, Rs1, Rs2

Rd = Rs1 - Rs2（补码运算）

0011

Rd（2位）+ Rs1（1位）+ Rs2（1位）

00111001（R1=R0-R3）

AND Rd, Rs1, Rs2

Rd = Rs1 & Rs2（按位与）

0100

Rd（2位）+ Rs1（1位）+ Rs2（1位）

01001001（R1=R0&R3）

OR Rd, Rs1, Rs2

Rd = Rs1 | Rs2（按位或）

0101

Rd（2位）+ Rs1（1位）+ Rs2（1位）

01011001（R1=R0|R3）

JMP addr

无条件跳转，PC = addr

1111

跳转地址addr（4位）

11110010（PC=2）

2. DigitalLogic-CPU.md（数电与CPU对应关系）

核心：CPU所有模块均由数电知识点构成，边做边复习，强化记忆。

数电知识点

对应CPU模块

应用场景

组合逻辑（门电路、MUX、译码器）

ALU、控制单元CU、指令译码器

运算、指令译码、控制信号生成

时序逻辑（触发器、寄存器）

PC、IR、寄存器堆RegFile

存储指令、数据、程序计数器

计数器

PC程序计数器

自动递增，指向当前指令地址

存储器（ROM/RAM）

IM指令存储器、DM数据存储器

存储指令、临时数据

全加器

ALU加法/减法运算

核心算术运算单元

3. RISC-V-RV32I.md（向RV32I延伸）

本8位极简CPU是RISC-V RV32I的微缩版，核心结构完全一致，后续可无缝延伸：

- 字长：8位 → 32位

- 指令集：7条极简指令 → RISC-V RV32I基础子集（add、sub、lw、sw、jmp等）

- 实现方式：Logisim画图 → Verilog代码 → FPGA验证

- 核心不变：PC→IM→IR→CU→RegFile→ALU的取指-译码-执行-写回流程

🚀 每日任务详情（按文件夹整理）

Day01：8位ALU设计（01-ALU/）

任务目标

设计一个支持加、减、与、或运算的8位ALU，具备运算选择和结果零标志输出。

设计规格

- 输入：A[7:0]（操作数1）、B[7:0]（操作数2）、op[1:0]（运算选择）

- 输出：Result[7:0]（运算结果）、Zero（结果为0时输出高电平）

- 运算选择：op=00（ADD）、op=01（SUB）、op=10（AND）、op=11（OR）

实现步骤

1. 用8个1位全加器级联，实现8位加法器（ADD运算）；

2. 减法实现：B取反 + 1（补码运算），复用加法器；

3. 用8个与门、8个或门，分别实现AND、OR运算；

4. 用4选1 MUX选择最终运算结果，连接到Result输出；

5. 添加零标志检测：Result全为0时，Zero输出高电平。

仓库文件

- ALU.circ：Logisim仿真文件（可直接打开仿真）

- ALU-Design.md：详细设计步骤、真值表、连线说明

- ALU-Test.png：仿真测试截图

Day02：PC + IR + IM设计（02-PC-IR-IM/）

任务目标

实现CPU取指通路：PC产生地址 → IM读取指令 → IR锁存指令。

模块设计

1. PC（程序计数器）：8位计数器，时钟上升沿自动+1，支持跳转（PCSrc控制）；

2. IM（指令存储器）：8位宽、16深度ROM，预先写入指令（地址0~15）；

3. IR（指令寄存器）：8位寄存器，时钟上升沿锁存IM输出的指令，供后续译码使用。

仓库文件

- PC-IR-IM.circ：Logisim仿真文件

- Instruction-Memory-Init.txt：IM初始化指令列表

- Fetch-Path.md：取指通路流程说明、连线图

Day03～Day07（简要框架，对应文件夹）

每个文件夹均包含：Logisim仿真文件、详细设计步骤、测试截图、知识点备注，与Day01/02格式一致，确保可直接照着做。

💡 注意事项

- 所有Logisim文件均已适配版本v3.16.1，避免版本兼容问题；

- 每日任务优先完成核心模块，再进行仿真测试，避免一步错、步步错；

- 若仿真报错，优先检查连线（如引脚未连接、位宽不匹配），其次检查模块设计；

- 可在Doc文件夹中补充自己的学习笔记，记录数电知识点的应用心得。

🎯 最终目标

Day07完成后，运行以下汇编程序，在Logisim中观察寄存器R2的值变为5，即说明CPU设计成功。

; 测试程序：计算 2 + 3 = 5
mov r0, #2   ; 00010010，R0 = 2
mov r1, #3   ; 00010111，R1 = 3
add r2, r0, r1 ; 00101001，R2 = R0 + R1 = 5
nop          ; 00000000，空操作
jmp 3        ; 11110011，跳转至地址3，循环执行nop

📌 后续延伸

1. Verilog版本：将Logisim模块用Verilog代码实现，学习硬件描述语言；

2. 扩展指令集：添加Load/Store指令，实现数据存储器DM的读写；

3. FPGA验证：将Verilog代码下载到FPGA开发板，实现硬件运行；

4. RISC-V RV32I适配：将8位CPU扩展为32位，学习标准精简指令集。

🔗 相关资源

- Logisim官方文档：https://logisim-evolution.org/docs/

- RISC-V RV32I手册：RISC-V Spec

- 数电知识点回顾：组合逻辑、时序逻辑核心公式与电路设计

---

备注：本仓库笔记可直接上传GitHub，每日任务按文件夹同步更新，后续将逐步补充各模块的Logisim详细图纸和步骤说明。
