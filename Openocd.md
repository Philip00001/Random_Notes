https://zhuanlan.zhihu.com/p/711322588
# OpenOCD简明指南

[![woshiren](https://pica.zhimg.com/v2-5cb622c5a9680d5e5b21af70999594de_l.jpg?source=32738c0c&needBackground=1)](https://www.zhihu.com/people/yejiacong)

[woshiren](https://www.zhihu.com/people/yejiacong)

​![](https://picx.zhimg.com/v2-4812630bc27d642f7cafcd6cdeca3d7a.jpg?source=88ceefae)

我是人

10 人赞同了该文章

[OpenOCD](https://zhida.zhihu.com/search?content_id=246202923&content_type=Article&match_order=1&q=OpenOCD&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njg4OTI3ODEsInEiOiJPcGVuT0NEIiwiemhpZGFfc291cmNlIjoiZW50aXR5IiwiY29udGVudF9pZCI6MjQ2MjAyOTIzLCJjb250ZW50X3R5cGUiOiJBcnRpY2xlIiwibWF0Y2hfb3JkZXIiOjEsInpkX3Rva2VuIjpudWxsfQ.84YPn9wbq2BqcXZ4fVeFclnTNFaOk2tTU4UrHw1KaWQ&zhida_source=entity)（Open On Chip Debugger）是一个开源的嵌入式调试软件，支持多种[SoC](https://zhida.zhihu.com/search?content_id=246202923&content_type=Article&match_order=1&q=SoC&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njg4OTI3ODEsInEiOiJTb0MiLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoyNDYyMDI5MjMsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9.Ct6h59lZOCSMcqdqhjVXyVEy-kpUOtWtnwiZO4iEQ6E&zhida_source=entity)、[FPGA](https://zhida.zhihu.com/search?content_id=246202923&content_type=Article&match_order=1&q=FPGA&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njg4OTI3ODEsInEiOiJGUEdBIiwiemhpZGFfc291cmNlIjoiZW50aXR5IiwiY29udGVudF9pZCI6MjQ2MjAyOTIzLCJjb250ZW50X3R5cGUiOiJBcnRpY2xlIiwibWF0Y2hfb3JkZXIiOjEsInpkX3Rva2VuIjpudWxsfQ.b88ltPHokD_O4U3jIp4LnWVBNfyqwZiF4Ywu8m2pDNg&zhida_source=entity)、[CPLD](https://zhida.zhihu.com/search?content_id=246202923&content_type=Article&match_order=1&q=CPLD&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njg4OTI3ODEsInEiOiJDUExEIiwiemhpZGFfc291cmNlIjoiZW50aXR5IiwiY29udGVudF9pZCI6MjQ2MjAyOTIzLCJjb250ZW50X3R5cGUiOiJBcnRpY2xlIiwibWF0Y2hfb3JkZXIiOjEsInpkX3Rva2VuIjpudWxsfQ.ZC08_uqtgqG2g403OEMSjngROg7cvIrMKZoc64O702A&zhida_source=entity)和调试器等，提供了一个优秀的抽象层，使得用户可以通过几乎一致的操作对嵌入式工程进行调试。

本指南仅涉及嵌入式SoC的烧录与调试操作。

有关FPGA和CPLD的使用笔者暂未探索。

### OpenOCD CLI Options

这里仅介绍常用的若干命令选项

- **`-f` 或 `--file <filename>`**:
    
    - 指定配置文件。配置文件定义了目标设备、接口和调试器的设置。
        
    - 示例：`openocd -f board/stm32f4discovery.cfg`
        
- **`-c` 或 `--command <cmd>`**:
    
    - 执行指定的命令，然后退出。可以用于执行一系列脚本命令。
        
    - 示例：`openocd -c "init; reset halt; exit"`
        
- **`-d` 或 `--debug <level>`**:
    
    - 设置调试输出级别。级别从0（无调试信息）到3（详细调试信息）。
        
    - 示例：`openocd -d 3`
        
- **`-s` 或 `--search <dir>`**:
    
    - 添加脚本搜索路径。
        
    - 示例：`openocd -s /path/to/scripts`
        
- **`--telnet_port <port>`**:
    
    - 指定[Telnet](https://zhida.zhihu.com/search?content_id=246202923&content_type=Article&match_order=1&q=Telnet&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njg4OTI3ODEsInEiOiJUZWxuZXQiLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoyNDYyMDI5MjMsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9.kPjmE-it3mhv48SM7Xj2EV76XhiIWmLRacM5EhNq7Ac&zhida_source=entity)服务器端口，用于调试会话。
    - 示例：`openocd --telnet_port 4444`
- **`--gdb_port <port>`**:
    
    - 指定[GDB](https://zhida.zhihu.com/search?content_id=246202923&content_type=Article&match_order=1&q=GDB&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njg4OTI3ODEsInEiOiJHREIiLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoyNDYyMDI5MjMsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9.aVnl_Fn0foWu7LilSkluR9LKGwavS5k9bnlvFr_fa7k&zhida_source=entity)服务器端口，用于连接GDB调试器。
    - 示例：`openocd --gdb_port 3333`
- **`--tcl_port <port>`**:
    
    - 指定[TCL](https://zhida.zhihu.com/search?content_id=246202923&content_type=Article&match_order=1&q=TCL&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njg4OTI3ODEsInEiOiJUQ0wiLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoyNDYyMDI5MjMsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9.YnSXeCOqpIlEAdJKIG4PeiN5gd875uSmUD7JuRFMJ5M&zhida_source=entity)服务器端口，用于脚本控制。
    - 示例：`openocd --tcl_port 6666`

把端口指定为disabled将禁用对应服务器。

### OpenOCD Config

在使用OpenOCD对进行编程调试时，需要提供若干cfg文件用于提供信息：

- interface：调试器接口，如[ST-Link](https://zhida.zhihu.com/search?content_id=246202923&content_type=Article&match_order=1&q=ST-Link&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njg4OTI3ODEsInEiOiJTVC1MaW5rIiwiemhpZGFfc291cmNlIjoiZW50aXR5IiwiY29udGVudF9pZCI6MjQ2MjAyOTIzLCJjb250ZW50X3R5cGUiOiJBcnRpY2xlIiwibWF0Y2hfb3JkZXIiOjEsInpkX3Rva2VuIjpudWxsfQ.2eUTxFxBp5u3FPaJoyI5VB000k99S2rI7bcv3vr-Ia8&zhida_source=entity)等；
- board：开发板，如ST-Nucleo系列的开发板等；
- target：嵌入式SoC，如STM32F4等；

interface指明了使用的调试器硬件，target指明了待调试的目标SoC。

特定的board有确定的target和interface，所以board内部一般会直接引用interface和target。

北邮机器人队内部常用两种调试器ST-Link和正点原子[DAP-Link](https://zhida.zhihu.com/search?content_id=246202923&content_type=Article&match_order=1&q=DAP-Link&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3Njg4OTI3ODEsInEiOiJEQVAtTGluayIsInpoaWRhX3NvdXJjZSI6ImVudGl0eSIsImNvbnRlbnRfaWQiOjI0NjIwMjkyMywiY29udGVudF90eXBlIjoiQXJ0aWNsZSIsIm1hdGNoX29yZGVyIjoxLCJ6ZF90b2tlbiI6bnVsbH0.-hbXB-_eS2R1IgKdSelRpeDgrYbglle3ziWbkbesIjU&zhida_source=entity)和STM32F4系列的MCU，因此有两种典型的配置：

```tcl
# stm32f4 with cmsis-dap
source [find interface/cmsis-dap.cfg]
source [find target/stm32f4x.cfg]
reset_config none
```

```tcl
# stm32f4 with st-link
source [find interface/stlink.cfg]
source [find target/stm32f4x.cfg]
reset_config none
```

- `source <config file>`指的是引入指定的配置文件。
- `find <path>`指的是在特定位置（如OpenOCD的安装目录）搜索指定的配置文件。
- `reset_config`指的是OpenOCD复位指令的行为，常用的选项如下：
    - `srst_only`：仅系统复位，有JTAG门控
    - `srst_nogate`：仅系统复位，无JTAG门控
    - `none`：默认配置，一般来说用这个就好

### OpenOCD Server

OpenOCD启动后会运行三种服务：

- GDB：默认运行在3333端口，GDB调试服务；
- TCL：默认运行在6666端口，TCL脚本服务；
- Telnet：默认运行在4444端口，Telnet服务；

GDB服务用于接入GDB，在GDB中输入`target remote :<port>`即可接入调试；

Telnet服务可以通过Telnet客户端登录，通过手动输入指令的方式进行调试；

TCL服务可以通过Socket连接，执行复杂的TCL脚本进行自动化调试；

### OpenOCD Command

OpenOCD指令众多，官方文档[Documentation (openocd.org)](https://link.zhihu.com/?target=https%3A//openocd.org/pages/documentation.html)有详细的介绍，由于一般使用GDB进行调试，这里不过多介绍其他指令，仅介绍一些常用的指令：

**Program**

```tcl
program <filename> [verify] [reset] [exit] [file_offset] [mem_offset] [bank]
```

- **`<filename>`**:
    
    - 要编程的文件的路径，可以是二进制文件（*.bin）、Intel HEX 文件（*.hex）或 ELF 文件（*.elf）。
    - bin文件是纯粹的二进制数据，不包含任何包括地址信息在内的其他数据，烧录时必须指定内存偏移；
    - hex文件是文本文件，包含十六进制编码的数据和地址信息，可以直接烧录；
    - elf文件是标准的二进制文件，除了数据及其地址之外，还包含了符号表、调试信息等完整的元数据，可以直接烧录；
- **`verify`**（可选）:
    
    - 编程后进行校验，确保数据正确写入。
- **`reset`**（可选）:
    
    - 编程完成后复位目标设备。
- **`exit`**（可选）:
    
    - 编程完成后退出 OpenOCD。
- **`file_offset`**（可选）:
    
    - 文件中数据的偏移量，通常用于将部分文件编程到设备。
    - 指定文件偏移时，必须同时指定内存偏移；
- **`mem_offset`**（可选）:
    
    - 目标设备内存中的偏移地址，指定数据写入的位置。
    - 仅指定一个地址时，该地址被视为内存偏移；
- **`bank`**（可选）:
    
    - 指定 Flash 存储器的Bank，当设备具有多个 Flash bank 时使用。

**实例：**

```tcl
program firmware.elf verify reset exit
```

烧录firmware.elf，校验并重置目标SoC，完成后退出OpenOCD。

```tcl
program firmware.bin 0x08000000 verify reset exit
```

烧录firmware.bin，从地址0x08000000开始烧录，校验并重置目标SoC，完成后退出OpenOCD

**Reset指令**

```tcl
reset [run|halt|init|deassert|assert|none]
```

- **`run`**:
    
    - 复位目标设备并立即让它运行。这是默认的复位行为。
        
    - 使用场景：通常用于将设备复位到初始状态并继续运行，例如在固件更新后让设备开始执行新的固件。
        
- **`halt`**:
    
    - 复位目标设备并让它在复位后保持暂停状态。
        
    - 使用场景：在调试时常用，以确保设备在已知状态下暂停，便于检查初始化状态或设置断点。
        
- **`init`**:
    
    - 复位目标设备，并在复位后执行初始化步骤。
        
    - 使用场景：在需要重新初始化调试器和设备状态时使用，确保设备从复位后的已知状态开始。
        
- **`deassert`**:
    
    - 取消复位信号，将目标设备从复位状态释放。
        
    - 使用场景：在需要手动控制复位信号的复杂调试场景中使用。
        
- **`assert`**:
    
    - 断言复位信号，使目标设备进入复位状态。
        
    - 使用场景：在需要手动控制复位信号的复杂调试场景中使用。
        
- **`none`**:
    
    - 不进行任何复位操作，通常与 `reset_config` 配置配合使用。
        
    - 使用场景：当复位行为已通过其他方式配置时使用。
        

**实例**

```tcl
reset run
```

复位目标SoC，使之开始运行；

```text
reset halt
```

复位目标SoC，暂停于复位向量处；

```tcl
reset init
```

复位目标SoC，执行到某个被指定的位置（完成初始化），相当于保证设备处于已初始化的稳定态；

### 实践指导

**烧录**

```sh
openocd -f <config-file> -c 'program <firware-file> verify reset exit'
```

**调试**

```sh
openocd -f <config-file> -c 'program <firware-file> verify reset' -c 'init; reset init;'
```

- program指令是可选的，但是笔者认为一般还是重新烧录比较稳妥（以防忘记烧录新固件）；
    
- init指令和reset指令是可选的，但是执行一次复位之后可以确保设备与调试器均处于稳定态；
    
- 可以通过指令指定服务器端口，参考第一节；
    

此后，启用调试有三种方法：

- 使用telnet连接openocd
- 连接tcl服务器执行tcl脚本
- 使用gdb，连接远程目标到openocd的gdbserver

```zsh
openocd -f interface/cmsis-dap.cfg -f target/stm32f1x.cfg
```

To debug, use [[arm-none-eabi-gdb]] for arm chips.

https://openocd.org/doc/html/GDB-and-OpenOCD.html

Also possible to use telnet localhost 4444:
https://acassis.wordpress.com/2016/02/25/using-openocd-to-program-a-homebrew-nrf51822-board/

Official list of targets:
https://sourceforge.net/p/openocd/code/ci/master/tree/tcl/target/


## Day 03: [Lab] 簡單操作OpenOCD

系統架構秘辛：了解RISC-V 架構底層除錯器的秘密！ 系列 第 3 篇

[![](https://member.ithome.com.tw/avatars/126388?s=ithelp)](https://ithelp.ithome.com.tw/m/users/20107327)

[HelloWorld](https://ithelp.ithome.com.tw/m/users/20107327)

8 年前 ‧ 24711 瀏覽

1

# 0. 前言

經過前面那篇~~廢話~~之後，相信應該能夠Build好自己一版的OpenOCD了吧!?  
如果不行的話，那..... 後面也不用看了 (誤

本篇是第一篇的Lab，應該算蠻淺顯易懂的，簡單的介紹一下OpenOCD的使用!  
    
    
  

# 1. 環境需求

- ARM相關開發版，這篇用的是[STM32F429I-DISCOVERY](http://www.st.com/en/evaluation-tools/32f429idiscovery.html)，單純剛好手邊有，另外上面有自帶ST-LINK/V2~!  
        
        
      

# 2. 環境設定

## 2.1 Connection

如圖所示，將STM32F429I-DISCOVERY開發版接到電腦上就行了!

![https://ithelp.ithome.com.tw/upload/images/20171221/201073270CzQEVJjOy.jpg](https://ithelp.ithome.com.tw/upload/images/20171221/201073270CzQEVJjOy.jpg)

連線好之後，開發版會上電，LD2正常亮起燈才對!  
    
  

## 2.2 OpenOCD Config

一般而言，官方的Source Code中已經針對部分平台，預先寫好一些常用的config file，  
而裡面會將相關設定做好初始化，那當然，我們就是直接把他拿來用啦XD

通常這些config都是放在\tcl中，下圖展示了相關的目錄結構

```Bash
|-- board
|-- chip
|   |-- atmel
|   |   `-- at91
|   |-- st
|   |   |-- spear
|   |   `-- stm32
|   `-- ti
|       `-- lm3s
|-- cpld
|-- cpu
|   `-- arm
|-- fpga
|-- interface
|   `-- ftdi
|-- target
|-- test
`-- tools
```

比較常用的目錄主要有三個: board、interface、target  
  

## 2.2.1 OpenOCD Config的使用

OpenOCD Config所使用的語法為TCL，我們可以簡單的建立openocd.cfg，  
來將所需要的Commands寫入!!

例如我們要透過ST-Link連到STM32-F4的板子上，可在openocd.cfg中放入以下內容:

```
source [find interface/stlink-v2.cfg]
source [find target/stm32f4x.cfg]
reset_config srst_only srst_nogate

init
reset
halt
```

## 2.2.2 OpenOCD的使用

為了方便起見，先將\tcl中的target、interface這兩個資料夾、OpenOCD的執行檔openocd，放入同一目錄中!

然後就是執行

```Bash
./openocd -f openocd.cfg
```

**常用的參數如下**

- -f : 指定config file的路徑，如果沒有設定的話，OpenOCD預設會開啟`openocd.cfg`
- -d : Level數字-3~3，從LOG_LVL_SILENT(-3)~LOG_LVL_DEBUG(3)
    - 編按: 現在多了一個LOG_LVL_DEBUG_IO(4)的Level用來底層I/O除錯用
- -l : Log file的路徑，預設會直接打印在OpenOCD的console上，加上這個可以把log導向檔案中，方便除錯!

成功執行OpenOCD後應該會出現以下類似的提示:

```
Open On-Chip Debugger 0.10.0+dev-00131-gb8db82f-dirty (2017-12-19-13:14)
Licensed under GNU GPL v2
For bug reports, read
    http://openocd.org/doc/doxygen/bugs.html
Info : auto-selecting first available session transport "hla_swd". To override use 'transport select <transport>'.
Info : The selected transport took over low-level target control. The results might differ compared to plain JTAG/SWD
adapter speed: 950 kHz
adapter_nsrst_delay: 100
srst_only separate srst_nogate srst_open_drain connect_deassert_srst
srst_only separate srst_nogate srst_open_drain connect_deassert_srst
Info : clock speed 950 kHz
Info : STLINK v2 JTAG v27 API v2 SWIM v0 VID 0x0483 PID 0x3748
Info : using stlink api v2
Info : Target voltage: 2.892163
Info : stm32f4x.cpu: hardware has 6 breakpoints, 4 watchpoints
**Info : Listening on port 3333 for gdb connections**
adapter speed: 950 kHz
target halted due to breakpoint, current mode: Thread 
xPSR: 0x21000000 pc: 0x08000460 msp: 0x20000720
Info : Listening on port 6666 for tcl connections
**Info : Listening on port 4444 for telnet connections**
```

其中可以看出目前Telent的Port在4444，而GDB的Port在3333，  
接下來就可以試著連線，以下分成Telnet連線和GDB連線介紹  
    
    
  

# 3. Lab操作

重於進入重頭戲--操作的部分，本節將先會介紹Telnet連線的方式和簡單的操作，  
後半段將介紹GDB連線的方式和簡單的操作，其他詳細Commands將會在日後的文章中介紹!  
    
  

## 3.1 Telnet

### 3.1.1 Telnet Connect

在Linux中，telnet連線的方式很簡單:

```
telnet <host> <port>
```

例如上節所提到的部分，Telnet的Port為4444，  
因此可以輸入以下指令來連線:

```
telnet localhost 4444
```

連上之後會出現類似下面的這個畫面

```
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
Open On-Chip Debugger
> 
```

就表示已經正常連線上去，可以開始進行一些操作!  
  

### 3.1.2 OpenOCD <--> Telnet的操作

比方說我們可以輸入`targets`這個指令來看目前連線上各個target的狀況:

```
> targets
    TargetName         Type       Endian TapName            State       
--  ------------------ ---------- ------ ------------------ ------------
 0* stm32f4x.cpu       hla_target little stm32f4x.cpu       halted
```

從這邊可以做一些簡單的分析，比方說目前連線的Target名稱為stm32f4x，屬於little endian的CPU，另外就是目前狀態是halted!

然後可以輸入`help`來看OpenOCD所支援的Commands:

```
...太多了，不想節錄。

全部省略XD
```

如果要結束連線的話，就簡單地輸入`exit`就行了!

```
> exit
Connection closed by foreign host.
```

那Telnet的介紹就到這邊!  
~~好短啊XD~~  
    
  

## 3.2 GDB

這部分跟往後學習有關，可以先建立一些基礎的環境和概念，  
當然，不會太詳細的講有關ARM設定的部分，這不是本文的重點，  
網路上也有更多優秀的文件可以參考!  
  

### 3.2.1 ARM Toolchain的取得與安裝

ARM的Toolchain在網路上都可以免費下載，請從[GNU Arm Embedded Toolchain](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads)取得所需的工具，  
這邊簡單的選擇gcc-arm-none-eabi-5_4-2016q3-20160926-linux作為Lab的學習工具!

下載下來把他解壓縮就行了，  
然後在$PATH中把<gcc-arm-none-eabi-5_4-2016q3的PATH>/bin加入，就可以直接使用!  
  

### 3.2.2 GDB Connection

GDB操作的教學很多，這邊推薦一個當初學習的時候，常參考的文件!

Ref:  
[Debugging with GDB （入門篇）](http://www.study-area.org/goldencat/debug.htm)

將<gcc-arm-none-eabi-5_4-2016q3的PATH>/bin加入$PATH後，可以利用以下Commmand來叫起GDB

```
$ arm-none-eabi-gdb
GNU gdb (GNU Tools for ARM Embedded Processors) 7.10.1.20160923-cvs
Copyright (C) 2015 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "--host=i686-linux-gnu --target=arm-none-eabi".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
<http://www.gnu.org/software/gdb/documentation/>.
For help, type "help".
Type "apropos word" to search for commands related to "word".
(gdb) 

```

然後在上節另外有提到GDB目前可使用的Port在3333，因此我們輸入以下Command來進行連接!

```
(gdb) target remote :3333
Remote debugging using :3333
0x08000460 in ?? ()
(gdb) 
```

接上之後，就可以看到目前$PC所在的位置為0x08000460，並等待使用者進一步的操作!  
  

### 3.2.3 OpenOCD <--> GDB的操作

同上節Telnet操作的範例，我們也用`targets`這個Command來熱身一下!

**注意的是，在GDB中要使用OpenOCD所支援的Command的時候，必須要使用以下方式:**

```
monitor <Commands>
```

以這個例子來說:

```
(gdb) monitor targets
    TargetName         Type       Endian TapName            State       
--  ------------------ ---------- ------ ------------------ ------------
 0* stm32f4x.cpu       hla_target little stm32f4x.cpu       halted
```

這邊出現的訊息同Telnet的解釋，不在另行敘述!

然後我們也可以使用`help`來看看OpenOCD所支援的Commands

```
(gdb) monitor help
adapter_khz [khz]
      With an argument, change to the specified maximum jtag speed.  For
      JTAG, 0 KHz signifies adaptive  clocking. With or without argument,
      display current setting. (command valid any time)
adapter_name
      Returns the name of the currently selected adapter (driver) (command
      valid any time)

.......太多了，不詳細寫!


```

最後是介紹離開的方式，簡單地輸入`quit`就行了!

```
(gdb) quit
A debugging session is active.

    Inferior 1 [Remote target] will be detached.

Quit anyway? (y or n) y
Detaching from program: , Remote target
Ending remote debugging.
```

好! 以上就是GDB的介紹，相信應該學會GDB的操作了 (誤!  
~~還是一樣的簡短~~  
    
    
  

# 99. 結語

第一篇Lab，稍微淺顯一點的介紹，主要還是在熟悉環境和操作上，  
還是沒有正式進入Source Code的世界中XD  
在之後文章介紹到GDB/GDB Server的部分時，還會在更加詳細的說明GDB <--> OpenOCD之間的關聯!  
    
    
  

# 參考資料

1. [Programming STM32 F2, F4 ARMs under Linux: A Tutorial from Scratch](http://www.triplespark.net/elec/pdev/arm/stm32.html)
2. [Lab6: Hardware](http://wiki.csie.ncku.edu.tw/embedded/Lab6)
3. [UM1670: Discovery kit with STM32F429ZI MCU](http://www.st.com/content/ccc/resource/technical/document/user_manual/6b/25/05/23/a9/45/4d/6a/DM00093903.pdf/files/DM00093903.pdf/jcr:content/translations/en.DM00093903.pdf)

- 留言
- 追蹤
- 分享
- 訂閱

[

此系列  
上一篇

](https://ithelp.ithome.com.tw/m/articles/10192529)

[

此系列  
下一篇

](https://ithelp.ithome.com.tw/m/articles/10193006)

## 0 則留言

- iThome 服務  
 - [iThome online](https://www.ithome.com.tw/)
 - [iThome Learning](https://learning.ithome.com.tw/)

- 電週文化事業版權所有、轉載必究 | Copyright © iThome
 - [刊登廣告](https://www.ithome.com.tw/aboutus/)
 - [服務信箱](mailto:ithelp@mail.ithome.com.tw)
 - [隱私權聲明與會員使用條款](https://www.ithome.com.tw/terms)
https://ithelp.ithome.com.tw/m/articles/10192744


# Config
![[openocd.cfg]]


