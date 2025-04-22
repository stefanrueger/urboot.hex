The ATtiny841 exhibits a UART baud rate quantisation error of -0.79% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.79% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|252|256|u8.0|`w---jPr--`|[urboot_t841_2s_x0m5_1k8_uart0_alt1_rxb2_txa7_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_2_s/external_oscillator_x/%2B0m500000_hz/%2B%2B%2B1k8_baud/uart0_alt1_rxb2_txa7/lednop/urboot_t841_2s_x0m5_1k8_uart0_alt1_rxb2_txa7_lednop.hex)|
|252|256|u8.0|`w---jPr--`|[urboot_t841_2s_x0m5_1k8_uart0_alt1_rxb2_txa7_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_2_s/external_oscillator_x/%2B0m500000_hz/%2B%2B%2B1k8_baud/uart0_alt1_rxb2_txa7/lednop/urboot_t841_2s_x0m5_1k8_uart0_alt1_rxb2_txa7_lednop_pr.hex)|
|290|320|u8.0|`w---jPr-c`|[urboot_t841_2s_x0m5_1k8_uart0_alt1_rxb2_txa7_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_2_s/external_oscillator_x/%2B0m500000_hz/%2B%2B%2B1k8_baud/uart0_alt1_rxb2_txa7/lednop/urboot_t841_2s_x0m5_1k8_uart0_alt1_rxb2_txa7_lednop_pr_ce.hex)|
|314|320|u8.0|`we--jPr--`|[urboot_t841_2s_x0m5_1k8_uart0_alt1_rxb2_txa7_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_2_s/external_oscillator_x/%2B0m500000_hz/%2B%2B%2B1k8_baud/uart0_alt1_rxb2_txa7/lednop/urboot_t841_2s_x0m5_1k8_uart0_alt1_rxb2_txa7_lednop_pr_ee.hex)|
|346|384|u8.0|`we--jPr-c`|[urboot_t841_2s_x0m5_1k8_uart0_alt1_rxb2_txa7_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny841/watchdog_2_s/external_oscillator_x/%2B0m500000_hz/%2B%2B%2B1k8_baud/uart0_alt1_rxb2_txa7/lednop/urboot_t841_2s_x0m5_1k8_uart0_alt1_rxb2_txa7_lednop_pr_ee_ce.hex)|

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
  + `x0m5` is F<sub>CPU</sub> of an external oscillator, here 0.5 MHz
  + `1k8` shows the fixed communication baud rate, here 1800 baud
  + `uart0` UART number
  + `alt1` alternative RX/TX pin assignment
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny841 WDTO=2S F_CPU=16000000L BAUD_RATE=57600 UARTNUM=0 UARTALT=1 RX=AtmelPB2 TX=AtmelPA7 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t841_2s_x16m0_57k6_uart0_alt1_rxb2_txa7_lednop
make MCU=attiny841 WDTO=2S F_CPU=16000000L BAUD_RATE=57600 UARTNUM=0 UARTALT=1 RX=AtmelPB2 TX=AtmelPA7 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t841_2s_x16m0_57k6_uart0_alt1_rxb2_txa7_lednop_pr
make MCU=attiny841 WDTO=2S F_CPU=16000000L BAUD_RATE=57600 UARTNUM=0 UARTALT=1 RX=AtmelPB2 TX=AtmelPA7 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t841_2s_x16m0_57k6_uart0_alt1_rxb2_txa7_lednop_pr_ce
make MCU=attiny841 WDTO=2S F_CPU=16000000L BAUD_RATE=57600 UARTNUM=0 UARTALT=1 RX=AtmelPB2 TX=AtmelPA7 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t841_2s_x16m0_57k6_uart0_alt1_rxb2_txa7_lednop_pr_ee
make MCU=attiny841 WDTO=2S F_CPU=16000000L BAUD_RATE=57600 UARTNUM=0 UARTALT=1 RX=AtmelPB2 TX=AtmelPA7 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t841_2s_x16m0_57k6_uart0_alt1_rxb2_txa7_lednop_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DUARTALT=1 -DTX=AtmelPA7 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_2s_x16m0_57k6_uart0_alt1_rxb2_txa7_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DUARTALT=1 -DTX=AtmelPA7 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_2s_x16m0_57k6_uart0_alt1_rxb2_txa7_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=30 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DUARTALT=1 -DTX=AtmelPA7 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_2s_x16m0_57k6_uart0_alt1_rxb2_txa7_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DUARTALT=1 -DTX=AtmelPA7 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_2s_x16m0_57k6_uart0_alt1_rxb2_txa7_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfc6 -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=38 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny841 -DF_CPU=16000000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=57600 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DUARTALT=1 -DTX=AtmelPA7 -DRX=AtmelPB2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t841_2s_x16m0_57k6_uart0_alt1_rxb2_txa7_lednop_pr_ee_ce.elf urboot.c
```

