The ATtiny2313 exhibits a UART baud rate quantisation error of +0.23% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.23% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|224|224|u7.7|`w-u-jPr--`|[urboot_t2313_2s_k0m5_1k2_uart0_rxd0_txd1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_2_s/internal_oscillator+2%/+0m500000_hz/+++1k2_baud/uart0_rxd0_txd1/no-led/urboot_t2313_2s_k0m5_1k2_uart0_rxd0_txd1_no-led.hex)|
|224|224|u7.7|`w-u-jPr--`|[urboot_t2313_2s_k0m5_1k2_uart0_rxd0_txd1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_2_s/internal_oscillator+2%/+0m500000_hz/+++1k2_baud/uart0_rxd0_txd1/no-led/urboot_t2313_2s_k0m5_1k2_uart0_rxd0_txd1_no-led_pr.hex)|
|250|256|u7.7|`w-u-jPr-c`|[urboot_t2313_2s_k0m5_1k2_uart0_rxd0_txd1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_2_s/internal_oscillator+2%/+0m500000_hz/+++1k2_baud/uart0_rxd0_txd1/no-led/urboot_t2313_2s_k0m5_1k2_uart0_rxd0_txd1_no-led_pr_ce.hex)|
|288|288|u7.7|`weu-jPr--`|[urboot_t2313_2s_k0m5_1k2_uart0_rxd0_txd1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_2_s/internal_oscillator+2%/+0m500000_hz/+++1k2_baud/uart0_rxd0_txd1/no-led/urboot_t2313_2s_k0m5_1k2_uart0_rxd0_txd1_no-led_pr_ee.hex)|
|318|320|u7.7|`weu-jPr-c`|[urboot_t2313_2s_k0m5_1k2_uart0_rxd0_txd1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny2313/watchdog_2_s/internal_oscillator+2%/+0m500000_hz/+++1k2_baud/uart0_rxd0_txd1/no-led/urboot_t2313_2s_k0m5_1k2_uart0_rxd0_txd1_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `k0m5` is F<sub>CPU</sub> of a too fast internal oscillator, here 0.5 MHz + 2%
  + `1k2` shows the fixed communication baud rate, here 1200 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny2313 WDTO=2S F_CPU=8160000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t2313_2s_k8m0_19k2_uart0_rxd0_txd1_no-led
make MCU=attiny2313 WDTO=2S F_CPU=8160000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t2313_2s_k8m0_19k2_uart0_rxd0_txd1_no-led_pr
make MCU=attiny2313 WDTO=2S F_CPU=8160000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t2313_2s_k8m0_19k2_uart0_rxd0_txd1_no-led_pr_ce
make MCU=attiny2313 WDTO=2S F_CPU=8160000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t2313_2s_k8m0_19k2_uart0_rxd0_txd1_no-led_pr_ee
make MCU=attiny2313 WDTO=2S F_CPU=8160000L BAUD_RATE=19200 UARTNUM=0 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_t2313_2s_k8m0_19k2_uart0_rxd0_txd1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x720UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x720 -Wl,--section-start=.version=0x7fa -DFRILLS=3 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=8160000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_2s_k8m0_19k2_uart0_rxd0_txd1_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x720UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x720 -Wl,--section-start=.version=0x7fa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=8160000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_2s_k8m0_19k2_uart0_rxd0_txd1_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0x700UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x700 -Wl,--section-start=.version=0x7fa -DFRILLS=4 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=8160000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_2s_k8m0_19k2_uart0_rxd0_txd1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x6e0UL -DRJMPWP=0xcfda -Wl,--section-start=.text=0x6e0 -Wl,--section-start=.version=0x7fa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=8160000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_2s_k8m0_19k2_uart0_rxd0_txd1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0x6c0UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0x6c0 -Wl,--section-start=.version=0x7fa -DFRILLS=4 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny2313 -DF_CPU=8160000L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=19200 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t2313_2s_k8m0_19k2_uart0_rxd0_txd1_no-led_pr_ee_ce.elf urboot.c
```

