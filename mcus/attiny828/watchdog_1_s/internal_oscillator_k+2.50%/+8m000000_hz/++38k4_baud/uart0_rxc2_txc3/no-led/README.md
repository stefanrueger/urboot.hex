The ATtiny828 exhibits a SWIO baud rate quantisation error of -0.21% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.21% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|250|256|u8.0|`w---hpr--`|[urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny828/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxc2_txc3/no-led/urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_hw.hex)|
|256|256|u8.0|`w---jPr--`|[urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny828/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxc2_txc3/no-led/urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led.hex)|
|256|256|u8.0|`w---jPr--`|[urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny828/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxc2_txc3/no-led/urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr.hex)|
|304|320|u8.0|`w---jPr-c`|[urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny828/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxc2_txc3/no-led/urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ce.hex)|
|314|320|u8.0|`we--jPr--`|[urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny828/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxc2_txc3/no-led/urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ee.hex)|
|382|384|u8.0|`weU-jPr-c`|[urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny828/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxc2_txc3/no-led/urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ee_ce.hex)|
|404|512|u8.0|`weU-hpr-c`|[urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny828/watchdog_1_s/internal_oscillator_k%2B2.50%25/%2B8m000000_hz/%2B%2B38k4_baud/uart0_rxc2_txc3/no-led/urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_ee_ce_hw.hex)|

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
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `k8m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 8.0 MHz + 2.50%
  + `38k4` shows the fixed communication baud rate, here 38400 baud
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
make MCU=attiny828 WDTO=1S F_CPU=8200000L BAUD_RATE=38400 SWIO=1 RX=AtmelPC2 TX=AtmelPC3 VBL=0 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_hw
make MCU=attiny828 WDTO=1S F_CPU=8200000L BAUD_RATE=38400 SWIO=1 RX=AtmelPC2 TX=AtmelPC3 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led
make MCU=attiny828 WDTO=1S F_CPU=8200000L BAUD_RATE=38400 SWIO=1 RX=AtmelPC2 TX=AtmelPC3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr
make MCU=attiny828 WDTO=1S F_CPU=8200000L BAUD_RATE=38400 SWIO=1 RX=AtmelPC2 TX=AtmelPC3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ce
make MCU=attiny828 WDTO=1S F_CPU=8200000L BAUD_RATE=38400 SWIO=1 RX=AtmelPC2 TX=AtmelPC3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ee
make MCU=attiny828 WDTO=1S F_CPU=8200000L BAUD_RATE=38400 SWIO=1 RX=AtmelPC2 TX=AtmelPC3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ee_ce
make MCU=attiny828 WDTO=1S F_CPU=8200000L BAUD_RATE=38400 SWIO=1 RX=AtmelPC2 TX=AtmelPC3 VBL=0 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfe0 -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=4 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny828 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=0 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPC3 -DRX=AtmelPC2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny828 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPC3 -DRX=AtmelPC2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1f00UL -DRJMPWP=0xcfdc -Wl,--section-start=.text=0x1f00 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny828 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPC3 -DRX=AtmelPC2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd2 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=5 -D_urboot_AVAILABLE=16 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny828 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPC3 -DRX=AtmelPC2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ec0UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1ec0 -Wl,--section-start=.version=0x1ffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny828 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPC3 -DRX=AtmelPC2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e80UL -DRJMPWP=0xcfcc -Wl,--section-start=.text=0x1e80 -Wl,--section-start=.version=0x1ffa -DFRILLS=6 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny828 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPC3 -DRX=AtmelPC2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1e00UL -DRJMPWP=0xcf96 -Wl,--section-start=.text=0x1e00 -Wl,--section-start=.version=0x1ffa -DFRILLS=10 -D_urboot_AVAILABLE=108 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny828 -DF_CPU=8200000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=38400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPC3 -DRX=AtmelPC2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t828_1s_k8m0_38k4_swio_rxc2_txc3_no-led_ee_ce_hw.elf urboot.c
```

