The ATtiny2313 exhibits a UART baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|220|224|u8.0|`w---jPr--`|[urboot_t2313_2s_x22m1184_921k6_uart0_rxd0_txd1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_2_s/external_oscillator_x/22m118400_hz/%2B921k6_baud/uart0_rxd0_txd1/lednop/urboot_t2313_2s_x22m1184_921k6_uart0_rxd0_txd1_lednop.hex)|
|220|224|u8.0|`w---jPr--`|[urboot_t2313_2s_x22m1184_921k6_uart0_rxd0_txd1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_2_s/external_oscillator_x/22m118400_hz/%2B921k6_baud/uart0_rxd0_txd1/lednop/urboot_t2313_2s_x22m1184_921k6_uart0_rxd0_txd1_lednop_pr.hex)|
|254|256|u8.0|`w---jPr-c`|[urboot_t2313_2s_x22m1184_921k6_uart0_rxd0_txd1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_2_s/external_oscillator_x/22m118400_hz/%2B921k6_baud/uart0_rxd0_txd1/lednop/urboot_t2313_2s_x22m1184_921k6_uart0_rxd0_txd1_lednop_pr_ce.hex)|
|284|288|u8.0|`we--jPr--`|[urboot_t2313_2s_x22m1184_921k6_uart0_rxd0_txd1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_2_s/external_oscillator_x/22m118400_hz/%2B921k6_baud/uart0_rxd0_txd1/lednop/urboot_t2313_2s_x22m1184_921k6_uart0_rxd0_txd1_lednop_pr_ee.hex)|
|314|320|u8.0|`we--jPr-c`|[urboot_t2313_2s_x22m1184_921k6_uart0_rxd0_txd1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_2_s/external_oscillator_x/22m118400_hz/%2B921k6_baud/uart0_rxd0_txd1/lednop/urboot_t2313_2s_x22m1184_921k6_uart0_rxd0_txd1_lednop_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x22m1184` is F<sub>CPU</sub> of an external oscillator, here 22.1184 MHz
  + `921k6` shows the fixed communication baud rate, here 921600 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny2313 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_2s_x24m0_1000k0_uart0_rxd0_txd1_lednop
make MCU=attiny2313 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_2s_x24m0_1000k0_uart0_rxd0_txd1_lednop_pr
make MCU=attiny2313 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_2s_x24m0_1000k0_uart0_rxd0_txd1_lednop_pr_ce
make MCU=attiny2313 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_2s_x24m0_1000k0_uart0_rxd0_txd1_lednop_pr_ee
make MCU=attiny2313 WDTO=2S F_CPU=24000000L BAUD_RATE=1000000 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t2313_2s_x24m0_1000k0_uart0_rxd0_txd1_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x720UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x720 -Wl,--section-start=.version=0x7fa -DFRILLS=3 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_2s_x24m0_1000k0_uart0_rxd0_txd1_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x720UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x720 -Wl,--section-start=.version=0x7fa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_2s_x24m0_1000k0_uart0_rxd0_txd1_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x700UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x700 -Wl,--section-start=.version=0x7fa -DFRILLS=5 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_2s_x24m0_1000k0_uart0_rxd0_txd1_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x6e0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x6e0 -Wl,--section-start=.version=0x7fa -DFRILLS=4 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_2s_x24m0_1000k0_uart0_rxd0_txd1_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x6c0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x6c0 -Wl,--section-start=.version=0x7fa -DFRILLS=5 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=24000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=1000000 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_2s_x24m0_1000k0_uart0_rxd0_txd1_lednop_pr_ee_ce.elf urboot.c
```

