The AT90USB82 exhibits a UART baud rate quantisation error of +1.73% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 1.73% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|246|256|u8.0|`w---jPr--`|[urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb82/watchdog_2_s/external_oscillator_x/%2B2m500000_hz/%2B%2B38k4_baud/uart0_rxd2_txd3/no-led/urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led.hex)|
|246|256|u8.0|`w---jPr--`|[urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb82/watchdog_2_s/external_oscillator_x/%2B2m500000_hz/%2B%2B38k4_baud/uart0_rxd2_txd3/no-led/urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led_pr.hex)|
|256|256|u8.0|`w---jPr-c`|[urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb82/watchdog_2_s/external_oscillator_x/%2B2m500000_hz/%2B%2B38k4_baud/uart0_rxd2_txd3/no-led/urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led_pr_ce.hex)|
|352|384|u8.0|`weU-jPr--`|[urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb82/watchdog_2_s/external_oscillator_x/%2B2m500000_hz/%2B%2B38k4_baud/uart0_rxd2_txd3/no-led/urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led_pr_ee.hex)|
|378|384|u8.0|`weU-jPr-c`|[urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb82/watchdog_2_s/external_oscillator_x/%2B2m500000_hz/%2B%2B38k4_baud/uart0_rxd2_txd3/no-led/urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led_pr_ee_ce.hex)|
|380|512|u8.0|`weU-hpr-c`|[urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90usb82/watchdog_2_s/external_oscillator_x/%2B2m500000_hz/%2B%2B38k4_baud/uart0_rxd2_txd3/no-led/urboot_usb82_2s_x2m5_38k4_uart0_rxd2_txd3_no-led_ee_ce_hw.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x2m5` is F<sub>CPU</sub> of an external oscillator, here 2.5 MHz
  + `38k4` shows the fixed communication baud rate, here 38400 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=at90usb82 WDTO=2S F_CPU=5000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led
make MCU=at90usb82 WDTO=2S F_CPU=5000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led_pr
make MCU=at90usb82 WDTO=2S F_CPU=5000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led_pr_ce
make MCU=at90usb82 WDTO=2S F_CPU=5000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led_pr_ee
make MCU=at90usb82 WDTO=2S F_CPU=5000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led_pr_ee_ce
make MCU=at90usb82 WDTO=2S F_CPU=5000000L BAUD_RATE=76800 UARTNUM=0 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb82 -DF_CPU=5000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb82 -DF_CPU=5000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb82 -DF_CPU=5000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfb3 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb82 -DF_CPU=5000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=8 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb82 -DF_CPU=5000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf8a -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=132 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90usb82 -DF_CPU=5000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_usb82_2s_x5m0_76k8_uart0_rxd2_txd3_no-led_ee_ce_hw.elf urboot.c
```

