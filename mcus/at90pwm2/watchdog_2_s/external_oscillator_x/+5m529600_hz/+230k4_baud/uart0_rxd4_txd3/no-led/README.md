The AT90PWM2 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|244|256|u8.0|`w---hpr--`|[urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B230k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_hw.hex)|
|248|256|u8.0|`w---jPr--`|[urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B230k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led.hex)|
|248|256|u8.0|`w---jPr--`|[urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B230k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_pr.hex)|
|314|320|u8.0|`w-U-jPr-c`|[urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B230k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_pr_ce.hex)|
|318|320|u8.0|`we--jPr--`|[urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B230k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_pr_ee.hex)|
|370|384|u8.0|`weU-jPr-c`|[urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B230k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_pr_ee_ce.hex)|
|392|512|u8.0|`weU-hpr-c`|[urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2/watchdog_2_s/external_oscillator_x/%2B5m529600_hz/%2B230k4_baud/uart0_rxd4_txd3/no-led/urboot_pwm2_2s_x5m5296_230k4_uart0_rxd4_txd3_no-led_ee_ce_hw.hex)|

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
  + `x5m5296` is F<sub>CPU</sub> of an external oscillator, here 5.5296 MHz
  + `230k4` shows the fixed communication baud rate, here 230400 baud
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
make MCU=at90pwm2 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_hw
make MCU=at90pwm2 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led
make MCU=at90pwm2 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_pr
make MCU=at90pwm2 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_pr_ce
make MCU=at90pwm2 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_pr_ee
make MCU=at90pwm2 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_pr_ee_ce
make MCU=at90pwm2 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc6 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf90 -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=120 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2_2s_x24m0_1000k0_uart0_rxd4_txd3_no-led_ee_ce_hw.elf urboot.c
```

