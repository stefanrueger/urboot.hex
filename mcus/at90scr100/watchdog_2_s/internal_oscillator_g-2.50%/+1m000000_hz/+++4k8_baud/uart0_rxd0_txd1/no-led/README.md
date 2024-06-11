The AT90SCR100 exhibits a SWIO baud rate quantisation error of +0.04% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.04% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u8.0|`w---jpr--`|[urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led.hex)|
|320|512|u8.0|`w-U-jPr--`|[urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr.hex)|
|362|512|u8.0|`w-U-jPr-c`|[urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ce.hex)|
|376|512|u8.0|`weU-jPr--`|[urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ee.hex)|
|404|512|u8.0|`weU-hpr-c`|[urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_ee_ce_hw.hex)|
|418|512|u8.0|`weU-jPr-c`|[urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/at90scr100/watchdog_2_s/internal_oscillator_g-2.50%25/%2B1m000000_hz/%2B%2B%2B4k8_baud/uart0_rxd0_txd1/no-led/urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ee_ce.hex)|

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
  + `g1m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 1.0 MHz - 2.50%
  + `4k8` shows the fixed communication baud rate, here 4800 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=at90scr100 WDTO=2S F_CPU=975000L BAUD_RATE=4800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led
make MCU=at90scr100 WDTO=2S F_CPU=975000L BAUD_RATE=4800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr
make MCU=at90scr100 WDTO=2S F_CPU=975000L BAUD_RATE=4800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ce
make MCU=at90scr100 WDTO=2S F_CPU=975000L BAUD_RATE=4800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ee
make MCU=at90scr100 WDTO=2S F_CPU=975000L BAUD_RATE=4800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_ee_ce_hw
make MCU=at90scr100 WDTO=2S F_CPU=975000L BAUD_RATE=4800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=975000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf68 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=192 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=975000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf7d -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=150 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=975000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf84 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=136 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=975000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf99 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=108 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=975000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf99 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=10 -D_urboot_AVAILABLE=94 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90scr100 -DF_CPU=975000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=4800 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_cr100_2s_g1m0_4k8_swio_rxd0_txd1_no-led_pr_ee_ce.elf urboot.c
```

