The AT90PWM2B exhibits a UART baud rate quantisation error of -0.57% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.57% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|246|256|u8.0|`w---hpr--`|[urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2b/watchdog_2_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd4_txd3/lednop/urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_hw.hex)|
|250|256|u8.0|`w---jPr--`|[urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2b/watchdog_2_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd4_txd3/lednop/urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop.hex)|
|250|256|u8.0|`w---jPr--`|[urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2b/watchdog_2_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd4_txd3/lednop/urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr.hex)|
|316|320|u8.0|`w-U-jPr-c`|[urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2b/watchdog_2_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd4_txd3/lednop/urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ce.hex)|
|320|320|u8.0|`we--jPr--`|[urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2b/watchdog_2_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd4_txd3/lednop/urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ee.hex)|
|372|384|u8.0|`weU-jPr-c`|[urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2b/watchdog_2_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd4_txd3/lednop/urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ee_ce.hex)|
|394|512|u8.0|`weU-hpr-c`|[urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90pwm2b/watchdog_2_s/internal_oscillator_m%2B5.00%25/%2B8m000000_hz/%2B%2B%2B9k6_baud/uart0_rxd4_txd3/lednop/urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_ee_ce_hw.hex)|

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
  + `m8m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 8.0 MHz + 5.00%
  + `9k6` shows the fixed communication baud rate, here 9600 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=at90pwm2b WDTO=2S F_CPU=8400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_hw
make MCU=at90pwm2b WDTO=2S F_CPU=8400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop
make MCU=at90pwm2b WDTO=2S F_CPU=8400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr
make MCU=at90pwm2b WDTO=2S F_CPU=8400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ce
make MCU=at90pwm2b WDTO=2S F_CPU=8400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ee
make MCU=at90pwm2b WDTO=2S F_CPU=8400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ee_ce
make MCU=at90pwm2b WDTO=2S F_CPU=8400000L BAUD_RATE=9600 UARTNUM=0 RX=AtmelPD4 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfde -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2b -DF_CPU=8400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2b -DF_CPU=8400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2b -DF_CPU=8400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfcb -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2b -DF_CPU=8400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2b -DF_CPU=8400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc7 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2b -DF_CPU=8400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf91 -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=118 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90pwm2b -DF_CPU=8400000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=9600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD3 -DRX=AtmelPD4 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_pwm2b_2s_m8m0_9k6_uart0_rxd4_txd3_lednop_ee_ce_hw.elf urboot.c
```

