The ATmega328P exhibits a SWIO baud rate quantisation error of +0.00% for this F_CPU and baud rate combination.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---jpr--`|[urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/jeenode/atmega328p/watchdog_2_s/external_oscillator_x/%2B4m608000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led-b1/urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1.hex)|
|330|384|u8.0|`w-U-jPr--`|[urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/jeenode/atmega328p/watchdog_2_s/external_oscillator_x/%2B4m608000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led-b1/urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr.hex)|
|366|384|u8.0|`we--jPr-c`|[urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/jeenode/atmega328p/watchdog_2_s/external_oscillator_x/%2B4m608000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led-b1/urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ee_ce.hex)|
|376|384|u8.0|`w-U-jPr-c`|[urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/jeenode/atmega328p/watchdog_2_s/external_oscillator_x/%2B4m608000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led-b1/urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ce.hex)|
|376|384|u8.0|`weU-jPr--`|[urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/jeenode/atmega328p/watchdog_2_s/external_oscillator_x/%2B4m608000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led-b1/urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ee.hex)|
|414|512|u8.0|`weU-hpr-c`|[urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/jeenode/atmega328p/watchdog_2_s/external_oscillator_x/%2B4m608000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/led-b1/urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_ee_ce_hw.hex)|

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
  + `x4m608` is F<sub>CPU</sub> of an external oscillator, here 4.608 MHz
  + `76k8` shows the fixed communication baud rate, here 76800 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led-b1` toggles an active-low (`-`) LED on pin `B1`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega328p WDTO=2S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 LEDPOLARITY=-1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1
make MCU=atmega328p WDTO=2S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LEDPOLARITY=-1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr
make MCU=atmega328p WDTO=2S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LEDPOLARITY=-1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ee_ce
make MCU=atmega328p WDTO=2S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LEDPOLARITY=-1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ce
make MCU=atmega328p WDTO=2S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LEDPOLARITY=-1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ee
make MCU=atmega328p WDTO=2S F_CPU=4608000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 LEDPOLARITY=-1 LED=AtmelPB1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=4608000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB1 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfa8 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=54 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=4608000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB1 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfd1 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=4608000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB1 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfbf -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=4608000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB1 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e80UL -DRJMPWP=0xcfc4 -Wl,--section-start=.text=0x7e80 -Wl,--section-start=.version=0x7ffa -DFRILLS=9 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=4608000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB1 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf9b -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=98 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=4608000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DLED=AtmelPB1 -DLEDPOLARITY=-1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_x4m608_76k8_swio_rxd0_txd1_led-b1_ee_ce_hw.elf urboot.c
```

