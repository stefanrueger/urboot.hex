The AT90PWM3B exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|244|256|u7.7|`w-u-hpr--`|[urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90pwm3b/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B38k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_hw.hex)|
|250|256|u7.7|`w-u-jPr--`|[urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90pwm3b/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B38k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led.hex)|
|250|256|u7.7|`w-u-jPr--`|[urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90pwm3b/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B38k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_pr.hex)|
|288|320|u7.7|`w-u-jPr-c`|[urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90pwm3b/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B38k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_pr_ce.hex)|
|316|320|u7.7|`weu-jPr--`|[urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90pwm3b/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B38k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_pr_ee.hex)|
|350|384|u7.7|`weu-jPr-c`|[urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90pwm3b/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B38k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_pr_ee_ce.hex)|
|332|512|u7.7|`weu-hpr-c`|[urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90pwm3b/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B38k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_ee_ce_hw.hex)|
|436|512|u7.7|`wes-hpr-c`|[urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/at90pwm3b/watchdog_2_s/external_oscillator_x/%2B1m843200_hz/%2B%2B38k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm3b_2s_x1m8432_38k4_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `s` uses skeleton of STK500v1 protocol (deprecated); `-c urclock` and `-c arduino` both work
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x1m8432` is F<sub>CPU</sub> of an external oscillator, here 1.8432 MHz
  + `38k4` shows the fixed communication baud rate, here 38400 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=at90pwm3b WDTO=2S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_hw
make MCU=at90pwm3b WDTO=2S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led
make MCU=at90pwm3b WDTO=2S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_pr
make MCU=at90pwm3b WDTO=2S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_pr_ce
make MCU=at90pwm3b WDTO=2S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_pr_ee
make MCU=at90pwm3b WDTO=2S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_pr_ee_ce
make MCU=at90pwm3b WDTO=2S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_ee_ce_hw
make MCU=at90pwm3b WDTO=2S F_CPU=24000000L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_hw.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc9 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=34 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf89 -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=180 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcfbd -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=76 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm3b -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm3b_2s_x24m0_500k0_uart0_rxd4_txd3_no-led_ee_ce_hw_stk500.elf urboot.c
```

