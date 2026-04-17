
* [English Version](./README.md)

### Ameba RTL8721Dx 系列 SoC：key_scan_event_trigger_demo（Raw API，FreeRTOS）

🚀 本示例基于 RTL8721Dx 系列 SoC 的 Key-Scan 外设，演示了一个 **4×4 键盘矩阵** 的按键扫描与事件触发用法，使用 Raw API 实现。

- 📎 开发板购买链接：[🛒 淘宝](https://item.taobao.com/item.htm?id=904981157046) | [📦 Amazon](https://www.amazon.com/-/zh/dp/B0FB33DT2C/)
- 📄 [芯片详情](https://aiot.realmcu.com/zh/module/rtl8721dx.html)
- 📚 [Key-Scan 文档](https://aiot.realmcu.com/cn/latest/rtos/peripherals/key_scan/index.html)

---

### ✨ 功能特点

✅ 使用 4×4 按键矩阵  
✅ 事件触发模式：每次按键按下 / 松开，FIFO 中只记录一条事件  
✅ 支持多键检测：最多可同时按下 **6 个按键**  
✅ 4×4 键盘矩阵引脚定义
![alt text](image.png)
行（Row）：

| 行号 | 引脚  |
|------|-------|
| Row 1 | PA31 |
| Row 2 | PA30 |
| Row 3 | PA29 |
| Row 4 | PA28 |

列（Column）：

| 列号 | 引脚  |
|------|-------|
| Col 1 | PB17 |
| Col 2 | PB18 |
| Col 3 | PB20 |
| Col 4 | PA14 |

---

### 工作原理

- Key-Scan 外设通过轮询行、列引脚的方式检测按键矩阵状态变化。  
- 当检测到按键按下或松开时，会产生中断，并将事件写入 FIFO。  
- 本示例采用 **事件触发模式 (event trigger mode)**，应用线程从 FIFO 读取数据并打印对应的键值信息。  
- 详细原理请参考 SDK 文档 Key-Scan 章节：  
  📚 [Key-Scan 文档](https://aiot.realmcu.com/cn/latest/rtos/peripherals/key_scan/index.html)

---

### 🚀 快速开始

1️⃣ **选择SDK**  
   - 设置`env.sh`（`env.bat`）路径：`source {sdk}/env.sh`  
   - 将`{sdk}`替换为[ameba-rtos SDK](https://github.com/Ameba-AIoT/ameba-rtos)根目录中`env.sh`的绝对路径。如果SDK路径没有改变，此步骤仅需执行一次。

   ⚡ **注意**：本示例仅支持 SDK 版本 **≥ v1.2**

2️⃣ **编译**  
   - 在当前工程目录下执行：  
     ```bash
     source env.sh
     ameba.py build -p
     ```

3️⃣ **烧录固件**
   >请将命令中的 `COMx` 替换为实际串口号（例如 `COM5`）
   ```bash
   ameba.py flash --p COMx --image km4_boot_all.bin 0x08000000 0x8014000 --image km0_km4_app.bin 0x08014000 0x8200000
   ```
   ⚡ **Note**: 若直接使用项目目录中已提供的预编译 bin 文件，可使用如下命令（注意相对路径）：
   ```bash
   ameba.py flash --p COMx --image ../km4_boot_all.bin 0x08000000 0x8014000 --image ../km0_km4_app.bin 0x08014000 0x8200000
   ```

4️⃣ **打开串口监视**  
   - `ameba.py monitor --port COMx --b 1500000`

5️⃣ **按键测试**

- 按下/松开 4×4 键盘矩阵上的按键；  
- 在串口终端中观察按键事件输出（包含行、列信息等）。

6️⃣ **观察日志输出** 📜  
- 参考下方“日志示例”，确认 Key-Scan 初始化和中断事件是否正常工作。

---

### 📝 日志示例

```bash
日志示例：
18:13:46.347  ROM:[V1.1]
18:13:46.347  FLASH RATE:1, Pinmux:1
18:13:46.347  IMG1(OTA1) VALID, ret: 0
18:13:46.347  IMG1 ENTRY[f800779:0]
18:13:46.347  [BOOT-I] KM4 BOOT REASON 0: Initial Power on
18:13:46.347  [BOOT-I] KM4 CPU CLK: 240000000 Hz
18:13:46.347  [BOOT-I] KM0 CPU CLK: 96000000 Hz
18:13:46.347  [BOOT-I] PSRAM Ctrl CLK: 240000000 Hz 
18:13:46.347  [BOOT-I] IMG1 ENTER MSP:[30009FDC]
18:13:46.347  [BOOT-I] Build Time: Feb  4 2026 16:20:53
18:13:46.347  [BOOT-I] IMG1 SECURE STATE: 1
18:13:46.362  [FLASH-I] FLASH CLK: 80000000 Hz
18:13:46.362  [FLASH-I] Flash ID: 85-20-16 (Capacity: 32M-bit)
18:13:46.362  [FLASH-I] Flash Read 4IO
18:13:46.362  [FLASH-I] FLASH HandShake[0x2 OK]
18:13:46.362  [BOOT-I] KM0 XIP IMG[0c000000:82c0]
18:13:46.362  [BOOT-I] KM0 SRAM[20068000:860]
18:13:46.362  [BOOT-I] KM0 PSRAM[0c008b20:20]
18:13:46.362  [BOOT-I] KM0 ENTRY[20004d00:60]
18:13:46.362  [BOOT-I] KM4 XIP IMG[0e000000:18820]
18:13:46.362  [BOOT-I] KM4 SRAM[2000b000:480]
18:13:46.362  [BOOT-I] KM4 PSRAM[0e018ca0:20]
18:13:46.362  [BOOT-I] KM4 ENTRY[20004d80:40]
18:13:46.362  [BOOT-I] IMG2 BOOT from OTA 1, Version: 1.1 
18:13:46.362  [BOOT-I] Image2Entry @ 0xe007b5d ...
18:13:46.362  [APP-I] KM4 APP START
18:13:46.362  [APP-I] VTOR: 30007000, VTOR_NS:30007000
18:13:46.362  [APP-I] IMG2 SECURE STATE: 1
18:13:46.362  [MAIN-I] IWDG refresh on!
18:13:46.362  [MAIN-I] KM0 OS START 
18:13:46.362  [CLK-I] [CAL4M]: delta:0 target:320 PPM: 0 PPM_Limit:30000 
18:13:46.378  [CLK-I] [CAL131K]: delta:10 target:2441 PPM: 4096 PPM_Limit:30000 
18:13:46.378  [LOCKS-I] KM4 init_retarget_locks
18:13:46.378  [APP-I] BOR arises when supply voltage decreases under 2.57V and recovers above 2.7V.
18:13:46.378  [MAIN-I] KM4 MAIN 
18:13:46.378  [VER-I] AMEBA-RTOS SDK VERSION: 1.2.0
18:13:46.378  [MAIN-I] File System Init Success 
18:13:46.378  [app_main-I] kscan_event_trigger_raw_thread create!
18:13:46.378  [MAIN-I] KM4 START SCHEDULER 

18:13:48.937  [app_main-I] SCAN_EVENT_INT FIFO Data: 111 
18:13:49.095  [app_main-I] SCAN_EVENT_INT FIFO Data: 11 
18:13:49.110  [app_main-I] ALL RELEASE intr
18:13:49.456  [app_main-I] SCAN_EVENT_INT FIFO Data: 121 
18:13:49.613  [app_main-I] SCAN_EVENT_INT FIFO Data: 21 
18:13:49.613  [app_main-I] ALL RELEASE intr
...
```


