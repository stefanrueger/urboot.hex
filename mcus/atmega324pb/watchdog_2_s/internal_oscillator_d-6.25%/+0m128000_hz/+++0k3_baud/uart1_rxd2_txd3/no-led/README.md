The ATmega324PB exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|246|256|u8.0|`w---jPr--`|[urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_2_s/internal_oscillator_d-6.25%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxd2_txd3/no-led/urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led.hex)|
|246|256|u8.0|`w---jPr--`|[urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_2_s/internal_oscillator_d-6.25%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxd2_txd3/no-led/urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr.hex)|
|256|256|u8.0|`w---jPr-c`|[urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_2_s/internal_oscillator_d-6.25%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxd2_txd3/no-led/urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ce.hex)|
|352|384|u8.0|`weU-jPr--`|[urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_2_s/internal_oscillator_d-6.25%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxd2_txd3/no-led/urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ee.hex)|
|378|384|u8.0|`weU-jPr-c`|[urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_2_s/internal_oscillator_d-6.25%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxd2_txd3/no-led/urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ee_ce.hex)|
|380|512|u8.0|`weU-hpr-c`|[urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/atmega324pb/watchdog_2_s/internal_oscillator_d-6.25%25/%2B0m128000_hz/%2B%2B%2B0k3_baud/uart1_rxd2_txd3/no-led/urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_ee_ce_hw.hex)|

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
  + `d0m128` is F<sub>CPU</sub> of a too slow internal oscillator, here 0.128 MHz - 6.25%
  + `0k3` shows the fixed communication baud rate, here 300 baud
  + `uart1` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega324pb WDTO=2S F_CPU=120000L BAUD_RATE=300 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led
make MCU=atmega324pb WDTO=2S F_CPU=120000L BAUD_RATE=300 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr
make MCU=atmega324pb WDTO=2S F_CPU=120000L BAUD_RATE=300 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ce
make MCU=atmega324pb WDTO=2S F_CPU=120000L BAUD_RATE=300 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ee
make MCU=atmega324pb WDTO=2S F_CPU=120000L BAUD_RATE=300 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ee_ce
make MCU=atmega324pb WDTO=2S F_CPU=120000L BAUD_RATE=300 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=120000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=300 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=120000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=300 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=120000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=300 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfb3 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=120000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=300 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=8 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=120000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=300 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf8a -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=132 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega324pb -DF_CPU=120000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=300 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m324pb_2s_d0m128_0k3_uart1_rxd2_txd3_no-led_ee_ce_hw.elf urboot.c
```

