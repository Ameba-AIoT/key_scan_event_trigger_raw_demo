
* [中文版](./README_CN.md)
### Ameba RTL8721Dx SoC: key_scan_event_trigger_demo (Raw API, FreeRTOS)

🚀 This example is a “Key-Scan” demo based on the RTL8721Dx series SoC.  
It demonstrates how to use the Key-Scan peripheral with a **4×4 keypad matrix** in event-trigger mode using the raw API.

- 📎 EVB Purchase Links: [🛒 Taobao](https://item.taobao.com/item.htm?id=904981157046) | [📦 Amazon](https://www.amazon.com/-/zh/dp/B0FB33DT2C/)
- 📄 [Chip Information](https://aiot.realmcu.com/zh/module/rtl8721dx.html)
- 📚 [Key-Scan Documentation](https://aiot.realmcu.com/cn/latest/rtos/peripherals/key_scan/index.html)

---

### ✨ Features

✅ 4×4 keypad matrix support  
✅ Event-trigger mode: for each key press/release, only **one event** is pushed into the FIFO  
✅ Multi-key detection: up to **6 keys** can be pressed simultaneously  
✅ 4×4 Keypad Matrix Pin Assignment
![alt text](image.png)
Row pins:

| Row | Pin  |
|-----|------|
| Row 1 | PA31 |
| Row 2 | PA30 |
| Row 3 | PA29 |
| Row 4 | PA28 |

Column pins:

| Column | Pin  |
|--------|------|
| Col 1 | PB17 |
| Col 2 | PB18 |
| Col 3 | PB20 |
| Col 4 | PA14 |

---

### Working Principle

- The Key-Scan peripheral scans row/column pins to detect changes on the keypad matrix.  
- When a key is pressed or released, an interrupt is generated and the corresponding event is written into the FIFO.  
- This demo uses **event-trigger mode**: an application thread reads events from the FIFO and prints the key information.  
- For more details, refer to the SDK Key-Scan chapter:  
  📚 [Key-Scan Documentation](https://aiot.realmcu.com/cn/latest/rtos/peripherals/key_scan/index.html)

---

### 🚀 Quick Start


1️⃣ **Select SDK**  
   - Set the path for `env.sh` (`env.bat`): `source {sdk}/env.sh`  
   - Replace `{sdk}` with the absolute path to `env.sh` in the root directory of the [ameba-rtos SDK](https://github.com/Ameba-AIoT/ameba-rtos). This step only needs to be performed once if the SDK path remains unchanged.

2️⃣ **Build**  
   - Execute the following in the demo example directory:  
     ```bash
     source env.sh
     ameba.py build -p
     ```

3️⃣ **Burning the Firmware**  
   > Replace `COMx` with your actual serial port (for example, `COM5`).

```bash
ameba.py flash --p COMx --image km4_boot_all.bin 0x08000000 0x8014000 --image km0_km4_app.bin 0x08014000 0x8200000
```

 ⚡ **Note**: If you want to use the **prebuilt binaries** provided in the project directory (parent folder), run:

```bash
ameba.py flash --p COMx --image ../km4_boot_all.bin 0x08000000 0x8014000 --image ../km0_km4_app.bin 0x08014000 0x8200000
```

4️⃣ **Monitor**  
   - `ameba.py monitor --port COMx --b 1500000`

5️⃣ **Keypad Test**

- Press and release keys on the 4×4 keypad matrix;  
- Observe the key events printed on the serial terminal (including row/column information).

6️⃣ **Check Log Output** 📜  

- Refer to the following “Log Example” section to verify that Key-Scan initialization and interrupt events are working properly.

---

### 📝 Log Example

```bash
Log example:
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
