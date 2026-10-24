# LabReport week05

## Lab5_1
# report Lab5-1

I (31) boot: ESP-IDF v5.1.2-dirty 2nd stage bootloader
I (31) boot: compile time Oct 24 2026 15:05:10
I (31) boot: Multicore bootloader
I (36) boot: chip revision: v3.1
I (40) boot.esp32: SPI Speed      : 40MHz
I (44) boot.esp32: SPI Mode       : DIO
I (49) boot.esp32: SPI Flash Size : 2MB
I (53) boot: Enabling RNG early entropy source...
I (59) boot: Partition Table:
I (62) boot: ## Label            Usage          Type ST Offset   Length
I (70) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (77) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (85) boot:  2 factory          factory app      00 00 00010000 00100000
I (92) boot: End of partition table
I (96) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=1ff5ch (130908) map
I (152) esp_image: segment 1: paddr=0002ff84 vaddr=3ffb0000 size=00094h (   148) load
I (152) esp_image: segment 2: paddr=00030020 vaddr=400d0020 size=810a0h (528544) map
I (349) esp_image: segment 3: paddr=000b10c8 vaddr=3ffb0094 size=039e8h ( 14824) load
I (355) esp_image: segment 4: paddr=000b4ab8 vaddr=40080000 size=15c3ch ( 89148) load
I (403) boot: Loaded app from partition at offset 0x10000
I (403) boot: Disabling RNG early entropy source...
I (415) cpu_start: Multicore app
I (415) cpu_start: Pro cpu up.
I (415) cpu_start: Starting app cpu, entry point is 0x40081390
--- 0x40081390: call_start_cpu1 at /Users/kittikarnkaewnual/esp/esp-idf/components/esp_system/port/cpu_start.c:157
I (0) cpu_start: App cpu up.
I (433) cpu_start: Pro cpu start user code
I (433) cpu_start: cpu freq: 160000000 Hz
I (433) cpu_start: Application information:
I (438) cpu_start: Project name:     wifi_scan_phase
I (443) cpu_start: App version:      e6e557f
I (448) cpu_start: Compile time:     Oct 24 2026 15:05:02
I (454) cpu_start: ELF file SHA256:  3947e4fa2710b06b...
I (460) cpu_start: ESP-IDF:          v5.1.2-dirty
I (466) cpu_start: Min chip rev:     v0.0
I (470) cpu_start: Max chip rev:     v3.99 
I (475) cpu_start: Chip rev:         v3.1
I (480) heap_init: Initializing. RAM available for dynamic allocation:
I (487) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (493) heap_init: At 3FFB7B18 len 000284E8 (161 KiB): DRAM
I (499) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (506) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (512) heap_init: At 40095C3C len 0000A3C4 (40 KiB): IRAM
I (520) spi_flash: detected chip: generic
I (523) spi_flash: flash io: dio
W (527) spi_flash: Detected size(4096k) larger than the size in the binary image header(2048k). Using the size in the binary image header.
I (541) app_start: Starting scheduler on CPU0
I (545) app_start: Starting scheduler on CPU1
I (545) main_task: Started on CPU0
I (555) main_task: Calling app_main()
I (555) LAB_WIFI_SCAN: [FORENSIC]: Call nvs_flash_init()
I (585) LAB_WIFI_SCAN: [FORENSIC]: nvs_flash_init() returned ESP_OK (0x0)
I (585) LAB_WIFI_SCAN: [FORENSIC]: Call esp_netif_init()
I (595) LAB_WIFI_SCAN: [FORENSIC]: esp_netif_init() returned ESP_OK (0x0)
I (595) LAB_WIFI_SCAN: [FORENSIC]: Call esp_event_loop_create_default()
I (605) LAB_WIFI_SCAN: [FORENSIC]: esp_event_loop_create_default() returned ESP_OK (0x0)
I (615) LAB_WIFI_SCAN: [FORENSIC]: Call esp_netif_create_default_wifi_sta()
I (625) LAB_WIFI_SCAN: [FORENSIC]: esp_netif_create_default_wifi_sta() returned pointer 0x3ffbd598
I (635) LAB_WIFI_SCAN: [FORENSIC]: Call esp_wifi_init(&cfg)
I (645) wifi:wifi driver task: 3ffbfbf0, prio:23, stack:6656, core=0
I (665) wifi:wifi firmware version: 91b9630
I (665) wifi:wifi certification version: v7.0
I (665) wifi:config NVS flash: enabled
I (665) wifi:config nano formating: disabled
I (665) wifi:Init data frame dynamic rx buffer num: 32
I (675) wifi:Init static rx mgmt buffer num: 5
I (675) wifi:Init management short buffer num: 32
I (685) wifi:Init dynamic tx buffer num: 32
I (685) wifi:Init static 
คำถามท้ายการทดลอง (Post-Lab Questions)

1. การกำหนดค่าในโครงสร้าง `wifi_scan_config_t` สำหรับสแกนเจาะจงเฉพาะช่องความถี่ (ข้อ 5.1.2) ช่วยลดเวลาในการสแกนเมื่อเทียบกับการสแกนทุกช่องความถี่ (ข้อ 5.1.1) อย่างไร และมีข้อจำกัดอย่างไร?
    ตอบ ช่วยลดเวลาเพราะสแกนเฉพาะช่องที่กำหนด แต่หากเครือข่ายอยู่ช่องอื่นจะค้นหาไม่พบ
2. เมื่อสังเกตผล Forensic Log ในข้อ 5.1.4 (สแกนหา SSID ที่ไม่มีอยู่จริง) ฟังก์ชัน `esp_wifi_scan_start()`, `esp_wifi_scan_get_ap_num()` และ `esp_wifi_scan_get_ap_records()` ส่งคืนค่าอย่างไร?
    ตอบ esp_wifi_scan_start() คืน ESP_OK เมื่อเริ่มสแกนสำเร็จ ส่วน esp_wifi_scan_get_ap_num() ได้จำนวน 0 และ esp_wifi_scan_get_ap_records() ไม่มีรายการ AP ให้ดึง
3. ค่าระดับความแรงสัญญาณ (RSSI) ที่แสดงเป็นตัวเลขติดลบ (เช่น -45 dBm กับ -80 dBm) ค่าใดแสดงถึงสัญญาณที่มีความแรงและความเสถียรมากกว่ากัน?
    ตอบ -45 dBm แรงกว่า -80 dBm เพราะค่าติดลบน้อยกว่าแสดงว่าสัญญาณแรงกว่า
4. เหตุใดการดึงค่า `authmode` (`wifi_auth_mode_t`) จากโครงสร้าง `wifi_ap_record_t` จึงมีความสำคัญต่อการเตรียมการในเฟสถัดไป (Authentication & Association Phase)?
    ตอบ เพื่อทราบประเภทการรักษาความปลอดภัยของ Wi-Fi และเตรียมการเชื่อมต่อให้ถูกต้อง
---

## Lab5_2
# report Lab5-2

I (792) LAB_WIFI_CONN: ------------------------------------------------------------------
I (792) LAB_WIFI_CONN:   Target SSID: "M"
I (802) LAB_WIFI_CONN:   Target Password: "12345678"
I (812) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_stop()
I (812) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_s�ets Jul 29 2019 12:21:46

rst:0x1 (POWERON_RESET),boot:0x13 (SPI_FAST_FLASH_BOOT)
configsip: 0, SPIWP:0xee
clk_drv:0x00,q_drv:0x00,d_drv:0x00,cs0_drv:0x00,hd_drv:0x00,wp_drv:0x00
mode:DIO, clock div:2
load:0x3fff0030,len:7084
ho 0 tail 12 room 4
load:0x40078000,len:15584
load:0x40080400,len:4
--- 0x40080400: _init at ??:?
load:0x40080404,len:3876
entry 0x4008064c
I (31) boot: ESP-IDF v5.1.2-dirty 2nd stage bootloader
I (31) boot: compile time Oct 24 2026 16:15:21
I (31) boot: Multicore bootloader
I (36) boot: chip revision: v3.1
I (40) boot.esp32: SPI Speed      : 40MHz
I (44) boot.esp32: SPI Mode       : DIO
I (49) boot.esp32: SPI Flash Size : 2MB
I (53) boot: Enabling RNG early entropy source...
I (59) boot: Partition Table:
I (62) boot: ## Label            Usage          Type ST Offset   Length
I (70) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (77) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (85) boot:  2 factory          factory app      00 00 00010000 00100000
I (92) boot: End of partition table
I (96) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=20224h (131620) map
I (152) esp_image: segment 1: paddr=0003024c vaddr=3ffb0000 size=03a7ch (14972) load
I (159) esp_image: segment 2: paddr=00033cd0 vaddr=40080000 size=0c348h (49992) load
I (179) esp_image: segment 3: paddr=00040020 vaddr=400d0020 size=812d0h (529104) map
I (371) esp_image: segment 4: paddr=000c12f8 vaddr=4008c348 size=098f4h (39156) load
I (398) boot: Loaded app from partition at offset 0x10000
I (398) boot: Disabling RNG early entropy source...
I (410) cpu_start: Multicore app
I (410) cpu_start: Pro cpu up.
I (410) cpu_start: Starting app cpu, entry point is 0x40081390
--- 0x40081390: call_start_cpu1 at /Users/kittikarnkaewnual/esp/esp-idf/components/esp_system/port/cpu_start.c:157
I (0) cpu_start: App cpu up.
I (428) cpu_start: Pro cpu start user code
I (428) cpu_start: cpu freq: 160000000 Hz
I (428) cpu_start: Application information:
I (433) cpu_start: Project name:     wifi_connection_phase
I (439) cpu_start: App version:      e6e557f-dirty
I (445) cpu_start: Compile time:     Oct 24 2026 16:15:15
I (451) cpu_start: ELF file SHA256:  ff3493f461ae66b4...
I (457) cpu_start: ESP-IDF:          v5.1.2-dirty
I (462) cpu_start: Min chip rev:     v0.0
I (467) cpu_start: Max chip rev:     v3.99 
I (472) cpu_start: Chip rev:         v3.1
I (476) heap_init: Initializing. RAM available for dynamic allocation:
I (484) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (490) heap_init: At 3FFB7B18 len 000284E8 (161 KiB): DRAM
I (496) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (502) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (509) heap_init: At 40095C3C len 0000A3C4 (40 KiB): IRAM
I (516) spi_flash: detected chip: generic
I (519) spi_flash: flash io: dio
W (523) spi_flash: Detected size(4096k) larger than the size in the binary image header(2048k). Using the size in the binary image header.
I (537) app_start: Starting scheduler on CPU0
I (542) app_start: Starting scheduler on CPU1
I (542) main_task: Started on CPU0
I (552) main_task: Calling app_main()
I (552) LAB_WIFI_CONN: [FORENSIC]: Call nvs_flash_init()
I (592) LAB_WIFI_CONN: [FORENSIC]: nvs_flash_init() returned ESP_OK (0x0)
I (602) LAB_WIFI_CONN: [FORENSIC]: Call esp_netif_init()
I (602) LAB_WIFI_CONN: [FORENSIC]: Call esp_event_loop_create_default()
I (612) LAB_WIFI_CONN: [FORENSIC]: Call esp_netif_create_default_wifi_sta()
I (612) LAB_WIFI_CONN: [FORENSIC]: esp_netif_create_default_wifi_sta() returned 0x3ffbd5c0
I (622) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_init(&cfg)
I (642) wifi:wifi driver task: 3ffbfc18, prio:23, stack:6656, core=0
I (652) wifi:wifi firmware version: 91b9630
I (652) wifi:wifi certification version: v7.0
I (652) wifi:config NVS flash: enabled
I (662) wifi:config nano formating: disabled
I (662) wifi:Init data frame dynamic rx buffer num: 32
I (662) wifi:Init static rx mgmt buffer num: 5
I (672) wifi:Init management short buffer num: 32
I (672) wifi:Init dynamic tx buffer num: 32
I (682) wifi:Init static rx buffer size: 1600
I (682) wifi:Init static rx buffer num: 10
I (682) wifi:Init dynamic rx buffer num: 32
I (692) wifi_init: rx ba win: 6
I (692) wifi_init: tcpip mbox: 32
I (702) wifi_init: udp mbox: 6
I (702) wifi_init: tcp mbox: 6
I (702) wifi_init: tcp tx win: 5744
I (712) wifi_init: tcp rx win: 5744
I (712) wifi_init: tcp mss: 1440
I (722) wifi_init: WiFi IRAM OP enabled
I (722) wifi_init: WiFi RX IRAM OP enabled
I (722) LAB_WIFI_CONN: [FORENSIC]: Call esp_event_handler_instance_register(WIFI_EVENT)
I (732) LAB_WIFI_CONN: [FORENSIC]: Call esp_event_handler_instance_register(IP_EVENT)
I (742) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_set_mode(WIFI_MODE_STA)
I (752) LAB_WIFI_CONN: ==================================================================
I (762) LAB_WIFI_CONN:   Lab 5.2: Wi-Fi Connection & IP Assignment (ESP-IDF Forensic)
I (772) LAB_WIFI_CONN: ==================================================================
I (782) LAB_WIFI_CONN: 

I (782) LAB_WIFI_CONN: ------------------------------------------------------------------
I (792) LAB_WIFI_CONN: >>> Experiment 5.2.1: Connection Test - Correct Credentials
I (802) LAB_WIFI_CONN: ------------------------------------------------------------------
I (802) LAB_WIFI_CONN:   Target SSID: "M"
I (812) LAB_WIFI_CONN:   Target Password: "12345678"
I (822) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_stop()
I (822) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_set_config(WIFI_IF_STA, &wifi_config)
I (872) LAB_WIFI_CONN: [FORENSIC]: esp_wifi_set_config() returned ESP_OK (0x0)
I (872) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_start()
I (872) phy_init: phy_version 4780,16b31a7,Sep 22 2023,20:42:16
I (952) wifi:mode : sta (84:1f:e8:39:b4:48)
I (952) wifi:enable tsf
I (952) LAB_WIFI_CONN: [FORENSIC]: esp_wifi_start() returned ESP_OK (0x0)
I (962) LAB_WIFI_CONN: [EVENT FORENSIC]: WIFI_EVENT_STA_START received
I (962) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_connect()
I (972) LAB_WIFI_CONN: [FORENSIC]: esp_wifi_connect() returned ESP_OK (0x0)
W (3382) LAB_WIFI_CONN: =======================================================
W (3382) LAB_WIFI_CONN: [EVENT FORENSIC]: WIFI_EVENT_STA_DISCONNECTED received!
W (3392) LAB_WIFI_CONN:   -> Target SSID          : M
W (3392) LAB_WIFI_CONN:   -> Reason Code (Decimal): 201
W (3402) LAB_WIFI_CONN:   -> Reason Code (Hex)    : 0xC9
W (3402) LAB_WIFI_CONN:   -> Reason Description   : WIFI_REASON_NO_AP_FOUND (201)
W (3412) LAB_WIFI_CONN: =======================================================
W (3422) LAB_WIFI_CONN: [RESULT]: TEST FAILED - Disconnected event captured.
I (5432) LAB_WIFI_CONN: 

I (5432) LAB_WIFI_CONN: ------------------------------------------------------------------
I (5432) LAB_WIFI_CONN: >>> Experiment 5.2.2: Connection Test - Wrong SSID (No AP Found)
I (5442) LAB_WIFI_CONN: ------------------------------------------------------------------
I (5442) LAB_WIFI_CONN:   Target SSID: "NON_EXISTENT_SSID_9999"
I (5452) LAB_WIFI_CONN:   Target Password: "12345678"
I (5462) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_stop()
E (5462) wifi:NAN WiFi stop
I (5472) LAB_WIFI_CONN: [EVENT FORENSIC]: WIFI_EVENT ID 3 received
I (5472) wifi:flush txq
I (5472) wifi:stop sw txq
I (5482) wifi:lmac stop hw txq
I (5482) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_set_config(WIFI_IF_STA,&wifi_config)
I (5512) LAB_WIFI_CONN: [FORENSIC]: esp_wifi_set_config() returned ESP_OK(0x0)
I (5512) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_start()
I (5522) wifi:mode : sta (84:1f:e8:39:b4:48)
I (5522) wifi:enable tsf
I (5532) LAB_WIFI_CONN: [EVENT FORENSIC]: WIFI_EVENT_STA_START received
I (5532) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_connect()
I (5542) LAB_WIFI_CONN: [FORENSIC]: esp_wifi_connect() returned ESP_OK (0x0)
I (5522) LAB_WIFI_CONN: [FORENSIC]: esp_wifi_start() returned ESP_OK (0x0)
W (7952) LAB_WIFI_CONN: =======================================================
W (7952) LAB_WIFI_CONN: [EVENT FORENSIC]: WIFI_EVENT_STA_DISCONNECTED received!
W (7952) LAB_WIFI_CONN:   -> Target SSID          : NON_EXISTENT_SSID_9999
W (7962) LAB_WIFI_CONN:   -> Reason Code (Decimal): 201
W (7972) LAB_WIFI_CONN:   -> Reason Code (Hex)    : 0xC9
W (7972) LAB_WIFI_CONN:   -> Reason Description   : WIFI_REASON_NO_AP_FOUND (201)
W (7982) LAB_WIFI_CONN: =======================================================
W (7992) LAB_WIFI_CONN: [RESULT]: TEST FAILED - Disconnected event captured.
I (10002) LAB_WIFI_CONN: 

I (10002) LAB_WIFI_CONN: ------------------------------------------------------------------
I (10002) LAB_WIFI_CONN: >>> Experiment 5.2.3: Connection Test - Wrong Password (Auth/Handshake Fail)
I (10012) LAB_WIFI_CONN: ------------------------------------------------------------------
I (10022) LAB_WIFI_CONN:   Target SSID: "M"
I (10022) LAB_WIFI_CONN:   Target Password: "WRONG_PASS_9999"
I (10032) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_stop()
E (10032) wifi:NAN WiFi stop
I (10042) LAB_WIFI_CONN: [EVENT FORENSIC]: WIFI_EVENT ID 3 received
I (10042) wifi:flush txq
I (10042) wifi:stop sw txq
I (10052) wifi:lmac stop hw txq
I (10052) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_set_config(WIFI_IF_STA, &wifi_config)
I (10102) LAB_WIFI_CONN: [FORENSIC]: esp_wifi_set_config() returned ESP_OK (0x0)
I (10102) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_start()
I (10102) wifi:mode : sta (84:1f:e8:39:b4:48)
I (10112) wifi:enable tsf
I (10112) LAB_WIFI_CONN: [EVENT FORENSIC]: WIFI_EVENT_STA_START received
I (10112) LAB_WIFI_CONN: [FORENSIC]: Call esp_wifi_connect()
I (10122) LAB_WIFI_CONN: [FORENSIC]: esp_wifi_connect() returned ESP_OK (0x0)
I (10112) LAB_WIFI_CONN: 
คำถามท้ายการทดลอง (Post-Lab Questions)

1. เหตุใดการระบุ SSID ผิด (ข้อ 5.2.2) จึงส่งผลให้เกิด Disconnect Event ด้วย Reason Code `201` (`WIFI_REASON_NO_AP_FOUND`) ตั้งแต่เฟส Scan?
    ตอบ เพราะ SSID ไม่ตรงกับเครือข่ายที่มีอยู่ จึงค้นหา AP ไม่พบและเกิด Reason Code 201
2. เหตุใดการพิมพ์ Password ผิด (ข้อ 5.2.3) จึงผ่านเฟส Auth และ Assoc มาได้ แต่มาล้มเหลวในเฟส 4-Way Handshake (Reason Code `15` หรือ `204`)?
    ตอบ เพราะรหัสผ่านจะถูกตรวจสอบอย่างสมบูรณ์ในขั้นตอน 4-Way Handshake จึงล้มเหลวเมื่อรหัสผ่านผิด
3. ลำดับการเกิด Event ระหว่าง **`WIFI_EVENT_STA_CONNECTED`** กับ **`IP_EVENT_STA_GOT_IP`** Event ใดเกิดขึ้นก่อนกัน และมีความหมายทางกายภาพของ Layer Network ต่างกันอย่างไร?
    ตอบ WIFI_EVENT_STA_CONNECTED เกิดก่อน หมายถึงเชื่อมต่อ Wi-Fi สำเร็จ ส่วน IP_EVENT_STA_GOT_IP หมายถึงได้รับ IP Address แล้ว
4. สมาชิกตัวแปร `reason` ในโครงสร้าง `wifi_event_sta_disconnected_t` มีประโยชน์อย่างไรต่อการออกแบบระบบค้นหาสาเหตุและกู้คืนการเชื่อมต่อ (Auto-Reconnection Mechanism) ในแอปพลิเคชัน IoT?
    ตอบ ใช้ระบุสาเหตุที่หลุดจาก Wi-Fi เพื่อเลือกวิธีแก้ไขและเชื่อมต่อใหม่ได้เหมาะสม

---

## Lab5_3
# report Lab5-3

I (31) boot: ESP-IDF v5.1.2-dirty 2nd stage bootloader
I (31) boot: compile time Oct 24 2026 17:05:19
I (31) boot: Multicore bootloader
I (36) boot: chip revision: v3.1
I (40) boot.esp32: SPI Speed      : 40MHz
I (44) boot.esp32: SPI Mode       : DIO
I (49) boot.esp32: SPI Flash Size : 2MB
I (53) boot: Enabling RNG early entropy source...
I (59) boot: Partition Table:
I (62) boot: ## Label            Usage          Type ST Offset   Length
I (70) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (77) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (85) boot:  2 factory          factory app      00 00 00010000 00100000
I (92) boot: End of partition table
I (96) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=2020ch (131596) map
I (152) esp_image: segment 1: paddr=00030234 vaddr=3ffb0000 size=03a7ch (14972) load
I (159) esp_image: segment 2: paddr=00033cb8 vaddr=40080000 size=0c360h (50016) load
I (180) esp_image: segment 3: paddr=00040020 vaddr=400d0020 size=811c4h (528836) map
I (371) esp_image: segment 4: paddr=000c11ec vaddr=4008c360 size=098dch (39132) load
I (398) boot: Loaded app from partition at offset 0x10000
I (398) boot: Disabling RNG early entropy source...
I (410) cpu_start: Multicore app
I (410) cpu_start: Pro cpu up.
I (410) cpu_start: Starting app cpu, entry point is 0x40081390
--- 0x40081390: call_start_cpu1 at /Users/kittikarnkaewnual/esp/esp-idf/components/esp_system/port/cpu_start.c:157
I (0) cpu_start: App cpu up.
I (428) cpu_start: Pro cpu start user code
I (428) cpu_start: cpu freq: 160000000 Hz
I (428) cpu_start: Application information:
I (433) cpu_start: Project name:     wifi_auth_assoc_phase
I (439) cpu_start: App version:      e6e557f-dirty
I (444) cpu_start: Compile time:     Oct 24 2026 17:05:12
I (451) cpu_start: ELF file SHA256:  ad1b349ddc3de442...
I (457) cpu_start: ESP-IDF:          v5.1.2-dirty
I (462) cpu_start: Min chip rev:     v0.0
I (467) cpu_start: Max chip rev:     v3.99 
I (471) cpu_start: Chip rev:         v3.1
I (476) heap_init: Initializing. RAM available for dynamic allocation:
I (484) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (489) heap_init: At 3FFB7B18 len 000284E8 (161 KiB): DRAM
I (496) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (502) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (508) heap_init: At 40095C3C len 0000A3C4 (40 KiB): IRAM
I (516) spi_flash: detected chip: generic
I (519) spi_flash: flash io: dio
W (523) spi_flash: Detected size(4096k) larger than the size in the binary image header(2048k). Using the size in the binary image header.
I (537) app_start: Starting scheduler on CPU0
I (541) app_start: Starting scheduler on CPU1
I (541) main_task: Started on CPU0
I (551) main_task: Calling app_main()
I (551) LAB_AUTH_ASSOC: [FORENSIC]: Call nvs_flash_init()
I (581) LAB_AUTH_ASSOC: [FORENSIC]: nvs_flash_init() returned ESP_OK (0x0)
I (581) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_netif_init()
I (591) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_event_loop_create_default()
I (591) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_netif_create_default_wifi_sta()
I (601) LAB_AUTH_ASSOC: [FORENSIC]: esp_netif_create_default_wifi_sta() returned 0x3ffbd5c0
I (611) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_wifi_init(&cfg)
I (631) wifi:wifi driver task: 3ffbfc18, prio:23, stack:6656, core=0
I (641) wifi:wifi firmware version: 91b9630
I (641) wifi:wifi certification version: v7.0
I (651) wifi:config NVS flash: enabled
I (651) wifi:config nano formating: disabled
I (651) wifi:Init data frame dynamic rx buffer num: 32
I (651) wifi:Init static rx mgmt buffer num: 5
I (661) wifi:Init management short buffer num: 32
I (661) wifi:Init dynamic tx buffer num: 32
I (671) wifi:Init static rx buffer size: 1600
I (671) wifi:Init static rx buffer num: 10
I (671) wifi:Init dynamic rx buffer num: 32
I (681) wifi_init: rx ba win: 6
I (681) wifi_init: tcpip mbox: 32
I (691) wifi_init: udp mbox: 6
I (691) wifi_init: tcp mbox: 6
I (691) wifi_init: tcp tx win: 5744
I (701) wifi_init: tcp rx win: 5744
I (701) wifi_init: tcp mss: 1440
I (711) wifi_init: WiFi IRAM OP enabled
I (711) wifi_init: WiFi RX IRAM OP enabled
I (721) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_event_handler_instance_register(WIFI_EVENT)
I (721) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_wifi_set_mode(WIFI_MODE_STA)
I (731) LAB_AUTH_ASSOC: ==================================================================
I (741) LAB_AUTH_ASSOC:   Lab 5.3: Wi-Fi Authentication & Association Phase (ESP-IDF Forensic)
I (751) LAB_AUTH_ASSOC: ==================================================================
I (761) LAB_AUTH_ASSOC: 

I (761) LAB_AUTH_ASSOC: ------------------------------------------------------------------
I (771) LAB_AUTH_ASSOC: >>> Experiment 5.3.1: Link-Layer Auth & Assoc Phase Test
I (781) LAB_AUTH_ASSOC: ------------------------------------------------------------------
I (791) LAB_AUTH_ASSOC:   Target SSID    : "M"
I (791) LAB_AUTH_ASSOC:   Target Password: "12345678"
I (801) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_wifi_stop()
I (801) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_wifi_set_config(WIFI_IF_STA,&wifi_config)
I (841) LAB_AUTH_ASSOC: [FORENSIC]: esp_wifi_set_config() returned ESP_OK(0x0)
I (841) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_wifi_start()
I (851) phy_init: phy_version 4780,16b31a7,Sep 22 2023,20:42:16
I (931) wifi:mode : sta (84:1f:e8:39:b4:48)
I (931) wifi:enable tsf
I (931) LAB_AUTH_ASSOC: [FORENSIC]: esp_wifi_start() returned ESP_OK (0x0)
I (931) LAB_AUTH_ASSOC: [EVENT FORENSIC]: WIFI_EVENT_STA_START received
I (941) LAB_AUTH_ASSOC: [FORENSIC]: Initiating 802.11 Link-Layer Connection (Auth & Assoc)...
I (951) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_wifi_connect()
I (961) LAB_AUTH_ASSOC: [FORENSIC]: esp_wifi_connect() returned ESP_OK (0x0)
I (1571) wifi:new:<6,0>, old:<1,0>, ap:<255,255>, sta:<6,0>, prof:1
I (1571) wifi:state: init -> auth (b0)
I (2911) wifi:state: auth -> assoc (0)
I (2921) wifi:state: assoc -> run (10)
I (2971) wifi:connected with M, aid = 2, channel 6, BW20, bssid = 32:8e:22:50:12:95
I (2981) wifi:security: WPA3-SAE, phy: bgn, rssi: -55
I (2991) wifi:pm start, type: 1

I (2991) LAB_AUTH_ASSOC: =======================================================
I (2991) LAB_AUTH_ASSOC: [EVENT FORENSIC]: WIFI_EVENT_STA_CONNECTED received!
I (3001) LAB_AUTH_ASSOC:   [SUCCESS]: Phase 2 (Auth) & Phase 3 (Assoc) COMPLETED!
I (3011) LAB_AUTH_ASSOC:   -> Connected SSID        : M
I (3011) LAB_AUTH_ASSOC:   -> BSSID (MAC Address)   : 32:8E:22:50:12:95
I (3021) LAB_AUTH_ASSOC:   -> Channel               : 6
I (3031) LAB_AUTH_ASSOC:   -> Auth Mode             : 7
I (3031) LAB_AUTH_ASSOC:   -> Association ID (AID)  : 3
I (3041) LAB_AUTH_ASSOC: =======================================================
I (3051) LAB_AUTH_ASSOC: [RESULT]: TEST PASSED - Phase 2 (Auth) & Phase 3(Assoc) Successful!
I (3101) wifi:AP's beacon interval = 102400 us, DTIM period = 1
I (3991) esp_netif_handlers: sta ip: 172.20.10.3, mask: 255.255.255.240, gw: 172.20.10.1
I (5061) LAB_AUTH_ASSOC: 

I (5061) LAB_AUTH_ASSOC: ------------------------------------------------------------------
I (5061) LAB_AUTH_ASSOC: >>> Experiment 5.3.2: Link-Layer Test - Non-Existent AP
I (5061) LAB_AUTH_ASSOC: ------------------------------------------------------------------
I (5071) LAB_AUTH_ASSOC:   Target SSID    : "NON_EXISTENT_AP_9999"
I (5081) LAB_AUTH_ASSOC:   Target Password: "12345678"
I (5091) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_wifi_stop()
I (5091) wifi:state: run -> init (0)
I (5101) wifi:pm stop, total sleep time: 1197623 us / 2107216 us

I (5101) wifi:new:<6,0>, old:<6,0>, ap:<255,255>, sta:<6,0>, prof:1
E (5111) wifi:NAN WiFi stop
W (5111) LAB_AUTH_ASSOC: =======================================================
W (5121) LAB_AUTH_ASSOC: [EVENT FORENSIC]: WIFI_EVENT_STA_DISCONNECTED received!
W (5131) LAB_AUTH_ASSOC:   -> Target SSID          : M
W (5131) LAB_AUTH_ASSOC:   -> Reason Code (Decimal): 8
W (5141) LAB_AUTH_ASSOC:   -> Reason Code (Hex)    : 0x08
W (5141) LAB_AUTH_ASSOC:   -> Reason Diagnosis     : OTHER_DISCONNECT_REASON
W (5151) LAB_AUTH_ASSOC: =======================================================
I (5161) LAB_AUTH_ASSOC: [EVENT FORENSIC]: WIFI_EVENT ID 3 received
I (5191) wifi:flush txq
I (5191) wifi:stop sw txq
I (5191) wifi:lmac stop hw txq
I (5191) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_wifi_set_config(WIFI_IF_STA, &wifi_config)
I (5211) LAB_AUTH_ASSOC: [FORENSIC]: esp_wifi_set_config() returned ESP_OK (0x0)
I (5211) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_wifi_start()
I (5221) wifi:mode : sta (84:1f:e8:39:b4:48)
I (5221) wifi:enable tsf
I (5231) LAB_AUTH_ASSOC: [FORENSIC]: esp_wifi_start() returned ESP_OK (0x0)
I (5231) LAB_AUTH_ASSOC: [EVENT FORENSIC]: WIFI_EVENT_STA_START received
I (5241) LAB_AUTH_ASSOC: [FORENSIC]: Initiating 802.11 Link-Layer Connection (Auth & Assoc)...
I (5251) LAB_AUTH_ASSOC: [FORENSIC]: Call esp_wifi_connect()
I (5261) LAB_AUTH_ASSOC: [FORENSIC]: esp_wifi_connect() returned ESP_OK (0x0)
W (5261) LAB_AUTH_ASSOC: [RESULT]: TEST FAILED - Disconnected event captured in Link-Layer.
I (5271) LAB_AUTH_ASSOC: ==================================================================
I (5281) LAB_AUTH_ASSOC:   [Phase 2 & Phase 3 Completed: Link-Layer Auth & Assoc Finished]
I (5291) LAB_AUTH_ASSOC: ==================================================================
I (5301) main_task: Returned from app_main()
W (7671) LAB_AUTH_ASSOC: =======================================================
W (7671) LAB_AUTH_ASSOC: [EVENT FORENSIC]: WIFI_EVENT_STA_DISCONNECTED received!
W (7671) LAB_AUTH_ASSOC:   -> Target SSID          : NON_EXISTENT_AP_9999
W (7681) LAB_AUTH_ASSOC:   -> Reason Code (Decimal): 201
W (7691) LAB_AUTH_ASSOC:   -> Reason Code (Hex)    : 0xC9
W (7691) LAB_AUTH_ASSOC:   -> Reason Diagnosis     : WIFI_REASON_NO_AP_FOUND (201) [Phase 1: SSID Not Found]
W (7701) LAB_AUTH_ASSOC: =======================================================


 คำถามท้ายการทดลอง (Post-Lab Questions)

1. **Association ID (AID)** คืออะไร มีบทบาทอย่างไรใน Phase 3 และส่งคืนมาในโครงสร้างข้อมูลตัวแปรใด?
    ตอบ AID คือหมายเลขประจำสถานีที่ Access Point กำหนดขณะ Association โดยอยู่ในตัวแปร aid ของ wifi_event_sta_connected_t
2. เหตุใดการเชื่อมต่อ Wi-Fi ความปลอดภัยแบบ WPA2-PSK จึงสามารถผ่าน Phase 2 (Authentication) และ Phase 3 (Association) จนเกิด Event `WIFI_EVENT_STA_CONNECTED` ได้สำเร็จ แม้ผู้ใช้จะป้อนรหัสผ่าน (Password) ผิด?
    ตอบ เพราะ Authentication และ Association ยังไม่ตรวจสอบรหัสผ่าน WPA2-PSK อย่างสมบูรณ์ ต้องตรวจสอบใน 4-Way Handshake
3. หาก Router มีการตั้งค่า **MAC Address Filtering** (อนุญาตเฉพาะ MAC ที่ลงทะเบียน) ESP32 จะล้มเหลวในเฟสใด และจะส่ง Disconnect Reason Code ใดออกมา?
    ตอบ ล้มเหลวในขั้น Association โดยอาจเกิด Reason Code 2 (WIFI_REASON_ASSOC_NOT_AUTHED) ขึ้นอยู่กับการตอบสนองของ Router
4. สรุปความแตกต่างสำคัญระหว่างจุดสิ้นสุดของ **Phase 3 (Link-Layer Connected)** กับจุดสิ้นสุดของ **Phase 5 (IP Address Assigned)**
    ตอบ Phase 3 คือเชื่อมต่อ Wi-Fi ระดับ Link Layer สำเร็จ ส่วน Phase 5 คือได้รับ IP Address และพร้อมสื่อสารผ่านเครือข่าย IP

---

## Lab5_4
# report Lab5-4

I (31) boot: ESP-IDF v5.1.2-dirty 2nd stage bootloader
I (31) boot: compile time Oct 24 2026 17:33:09
I (31) boot: Multicore bootloader
I (36) boot: chip revision: v3.1
I (40) boot.esp32: SPI Speed      : 40MHz
I (44) boot.esp32: SPI Mode       : DIO
I (49) boot.esp32: SPI Flash Size : 2MB
I (53) boot: Enabling RNG early entropy source...
I (59) boot: Partition Table:
I (62) boot: ## Label            Usage          Type ST Offset   Length
I (70) boot:  0 nvs              WiFi data        01 02 00009000 00006000
I (77) boot:  1 phy_init         RF data          01 01 0000f000 00001000
I (85) boot:  2 factory          factory app      00 00 00010000 00100000
I (92) boot: End of partition table
I (96) esp_image: segment 0: paddr=00010020 vaddr=3f400020 size=20024h (131108) map
I (152) esp_image: segment 1: paddr=0003004c vaddr=3ffb0000 size=03a7ch ( 14972) load
I (158) esp_image: segment 2: paddr=00033ad0 vaddr=40080000 size=0c548h ( 50504) load
I (180) esp_image: segment 3: paddr=00040020 vaddr=400d0020 size=813e4h (529380) map
I (371) esp_image: segment 4: paddr=000c140c vaddr=4008c548 size=096f4h ( 38644) load
I (398) boot: Loaded app from partition at offset 0x10000
I (398) boot: Disabling RNG early entropy source...
I (410) cpu_start: Multicore app
I (410) cpu_start: Pro cpu up.
I (410) cpu_start: Starting app cpu, entry point is 0x40081390
--- 0x40081390: call_start_cpu1 at /Users/kittikarnkaewnual/esp/esp-idf/components/esp_system/port/cpu_start.c:157
I (0) cpu_start: App cpu up.
I (428) cpu_start: Pro cpu start user code
I (428) cpu_start: cpu freq: 160000000 Hz
I (428) cpu_start: Application information:
I (433) cpu_start: Project name:     wifi_handshake_ip_phase
I (439) cpu_start: App version:      e6e557f-dirty
I (445) cpu_start: Compile time:     Oct 24 2026 17:33:03
I (451) cpu_start: ELF file SHA256:  adfdfdb0f5f0ee37...
I (457) cpu_start: ESP-IDF:          v5.1.2-dirty
I (462) cpu_start: Min chip rev:     v0.0
I (467) cpu_start: Max chip rev:     v3.99 
I (472) cpu_start: Chip rev:         v3.1
I (477) heap_init: Initializing. RAM available for dynamic allocation:
I (484) heap_init: At 3FFAE6E0 len 00001920 (6 KiB): DRAM
I (490) heap_init: At 3FFB7B20 len 000284E0 (161 KiB): DRAM
I (496) heap_init: At 3FFE0440 len 00003AE0 (14 KiB): D/IRAM
I (502) heap_init: At 3FFE4350 len 0001BCB0 (111 KiB): D/IRAM
I (509) heap_init: At 40095C3C len 0000A3C4 (40 KiB): IRAM
I (516) spi_flash: detected chip: generic
I (519) spi_flash: flash io: dio
W (523) spi_flash: Detected size(4096k) larger than the size in the binary image header(2048k). Using the size in the binary image header.
I (537) app_start: Starting scheduler on CPU0
I (542) app_start: Starting scheduler on CPU1
I (542) main_task: Started on CPU0
I (552) main_task: Calling app_main()
I (552) LAB_HANDSHAKE_IP: [INIT] Initializing NVS
I (582) LAB_HANDSHAKE_IP: [INIT] Initializing network interface
I (592) LAB_HANDSHAKE_IP: [INIT] Initializing Wi-Fi driver
I (602) wifi:wifi driver task: 3ffbfc20, prio:23, stack:6656, core=0
I (612) wifi:wifi firmware version: 91b9630
I (612) wifi:wifi certification version: v7.0
I (612) wifi:config NVS flash: enabled
I (622) wifi:config nano formating: disabled
I (622) wifi:Init data frame dynamic rx buffer num: 32
I (622) wifi:Init static rx mgmt buffer num: 5
I (632) wifi:Init management short buffer num: 32
I (632) wifi:Init dynamic tx buffer num: 32
I (642) wifi:Init static rx buffer size: 1600
I (642) wifi:Init static rx buffer num: 10
I (642) wifi:Init dynamic rx buffer num: 32
I (652) wifi_init: rx ba win: 6
I (652) wifi_init: tcpip mbox: 32
I (662) wifi_init: udp mbox: 6
I (662) wifi_init: tcp mbox: 6
I (662) wifi_init: tcp tx win: 5744
I (672) wifi_init: tcp rx win: 5744
I (672) wifi_init: tcp mss: 1440
I (682) wifi_init: WiFi IRAM OP enabled
I (682) wifi_init: WiFi RX IRAM OP enabled
I (692) LAB_HANDSHAKE_IP: [INIT] Registering event handlers
I (692) LAB_HANDSHAKE_IP: [INIT] Setting Wi-Fi station mode
I (702) LAB_HANDSHAKE_IP: ==================================================
I (712) LAB_HANDSHAKE_IP: Lab 5.4: 4-Way Handshake and IP Assignment
I (712) LAB_HANDSHAKE_IP: ==================================================
I (722) LAB_HANDSHAKE_IP: 
I (722) LAB_HANDSHAKE_IP: --------------------------------------------------
I (732) LAB_HANDSHAKE_IP: >>> Experiment 5.4.1: Correct Password
I (742) LAB_HANDSHAKE_IP: --------------------------------------------------
I (752) LAB_HANDSHAKE_IP: Target SSID: "M"
I (752) LAB_HANDSHAKE_IP: Password length: 8
I (762) LAB_HANDSHAKE_IP: [FORENSIC] Calling esp_wifi_stop()
I (762) LAB_HANDSHAKE_IP: [FORENSIC] esp_wifi_stop(): ESP_OK (0x0)
I (972) LAB_HANDSHAKE_IP: [FORENSIC] Calling esp_wifi_set_config()
I (992) LAB_HANDSHAKE_IP: [FORENSIC] esp_wifi_set_config(): ESP_OK (0x0)
I (992) LAB_HANDSHAKE_IP: [FORENSIC] Calling esp_wifi_start()
I (1002) phy_init: phy_version 4780,16b31a7,Sep 22 2023,20:42:16
I (1082) wifi:mode : sta (84:1f:e8:39:b4:48)
I (1082) wifi:enable tsf
I (1082) LAB_HANDSHAKE_IP: [FORENSIC] esp_wifi_start(): ESP_OK (0x0)
I (1082) LAB_HANDSHAKE_IP: [FORENSIC] Waiting for connection result (timeout 15000 ms)
I (1082) LAB_HANDSHAKE_IP: [EVENT] WIFI_EVENT_STA_START received
I (1102) LAB_HANDSHAKE_IP: [FORENSIC] Calling esp_wifi_connect()
I (1112) LAB_HANDSHAKE_IP: [FORENSIC] esp_wifi_connect(): ESP_OK (0x0)
W (3522) LAB_HANDSHAKE_IP: [EVENT] WIFI_EVENT_STA_DISCONNECTED received
W (3522) LAB_HANDSHAKE_IP: Target SSID: M
W (3522) LAB_HANDSHAKE_IP: Reason Code: 201 (0xC9)
W (3522) LAB_HANDSHAKE_IP: Diagnosis: WIFI_REASON_NO_AP_FOUND: SSID not found
W (3532) LAB_HANDSHAKE_IP: [RESULT] TEST FAILED
W (3542) LAB_HANDSHAKE_IP: Disconnected or failed during Wi-Fi connection
I (5542) LAB_HANDSHAKE_IP: 
I (5542) LAB_HANDSHAKE_IP: --------------------------------------------------
I (5542) LAB_HANDSHAKE_IP: >>> Experiment 5.4.2: Incorrect Password
I (5542) LAB_HANDSHAKE_IP: --------------------------------------------------
I (5552) LAB_HANDSHAKE_IP: Target SSID: "M"
I (5552) LAB_HANDSHAKE_IP: Password length: 19
I (5562) LAB_HANDSHAKE_IP: [FORENSIC] Calling esp_wifi_stop()
E (5572) wifi:NAN WiFi stop
I (5572) LAB_HANDSHAKE_IP: [EVENT] Wi-Fi event ID: 3
I (5582) wifi:flush txq
I (5582) wifi:stop sw txq
I (5582) wifi:lmac stop hw txq
I (5582) LAB_HANDSHAKE_IP: [FORENSIC] esp_wifi_stop(): ESP_OK (0x0)
I (5792) LAB_HANDSHAKE_IP: [FORENSIC] Calling esp_wifi_set_config()
I (5812) LAB_HANDSHAKE_IP: [FORENSIC] esp_wifi_set_config(): ESP_OK (0x0)
I (5812) LAB_HANDSHAKE_IP: [FORENSIC] Calling esp_wifi_start()
I (5822) wifi:mode : sta (84:1f:e8:39:b4:48)
I (5822) wifi:enable tsf
I (5822) LAB_HANDSHAKE_IP: [EVENT] WIFI_EVENT_STA_START received
I (5832) LAB_HANDSHAKE_IP: [FORENSIC] Calling esp_wifi_connect()
I (5842) LAB_HANDSHAKE_IP: [FORENSIC] esp_wifi_connect(): ESP_OK (0x0)
I (5822) LAB_HANDSHAKE_IP: [FORENSIC] esp_wifi_start(): ESP_OK (0x0)
I (5852) LAB_HANDSHAKE_IP: [FORENSIC] Waiting for connection result (timeout 15000 ms)
W (8252) LAB_HANDSHAKE_IP: [EVENT] WIFI_EVENT_STA_DISCONNECTED received
W (8252) LAB_HANDSHAKE_IP: Target SSID: M
W (8252) LAB_HANDSHAKE_IP: Reason Code: 201 (0xC9)
W (8252) LAB_HANDSHAKE_IP: Diagnosis: WIFI_REASON_NO_AP_FOUND: SSID not found
W (8262) LAB_HANDSHAKE_IP: [RESULT] TEST FAILED
W (8272) LAB_HANDSHAKE_IP: Disconnected or failed during Wi-Fi connection
I (8272) LAB_HANDSHAKE_IP: ==================================================
I (8282) LAB_HANDSHAKE_IP: Lab 5.4 tests finished
I (8292) LAB_HANDSHAKE_IP: ==================================================
I (8302) main_task: Returned from app_main()

คำถามท้ายการทดลอง (Post-Lab Questions)

1. เหตุใดกระบวนการ **4-Way Handshake** จึงพิสูจน์ทราบรหัสผ่าน Wi-Fi ได้โดยไม่ต้องส่งรหัสผ่าน (Passphrase) ลอยไปในอากาศเลยแม้แต่แพ็กเกจเดียว?
    ตอบ เพราะทั้งสองฝ่ายใช้รหัสผ่านสร้างคีย์และตรวจสอบข้อความยืนยันร่วมกัน โดยไม่ต้องส่งรหัสผ่านจริงผ่านอากาศ
2. อธิบายบทบาทและที่มาของคีย์ **PMK (Pairwise Master Key)** และ **PTK (Pairwise Transient Key)** ว่ามีความสัมพันธ์กันอย่างไรในการเข้ารหัสเฟรมข้อมูล?
    ตอบ PMK เป็นคีย์หลัก ส่วน PTK สร้างจาก PMK และข้อมูลของทั้งสองฝ่าย เพื่อใช้ตรวจสอบและเข้ารหัสข้อมูล
3. เหตุใดเมื่อเราพิมพ์ Password ผิด (ข้อ 5.4.2) ESP32 จึงยังคงได้รับ Event **`WIFI_EVENT_STA_CONNECTED`** ก่อนที่จะเกิด Event **`WIFI_EVENT_STA_DISCONNECTED`** ตามมาในภายหลัง?
    ตอบ เพราะ ESP32 เชื่อมต่อระดับ Wi-Fi ได้ก่อน แต่เมื่อตรวจสอบรหัสผ่านใน 4-Way Handshake ไม่ผ่าน จึง Disconnect ภายหลัง
4. หากเครือข่าย Wi-Fi ไม่มี DHCP Server (ไม่มีการแจก IP อัตโนมัติ) ผลการทดลองในข้อ 5.4.1 จะหยุดอยู่ที่ขั้นตอนใด และจะไม่เกิด Event ใดขึ้น?
    ตอบ หยุดที่ขั้นเชื่อมต่อ Wi-Fi แต่ไม่ได้รับ IP Address จึงไม่เกิด Event IP_EVENT_STA_GOT_IP