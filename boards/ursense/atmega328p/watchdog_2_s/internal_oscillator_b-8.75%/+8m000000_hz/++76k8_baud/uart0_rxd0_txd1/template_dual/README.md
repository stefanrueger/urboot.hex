The ATmega328P exhibits a SWIO baud rate quantisation error of +0.05% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.05% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|468|512|u8.1|`w-UdjPr--`|[urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/atmega328p/watchdog_2_s/internal_oscillator_b-8.75%25/%2B8m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual.hex)|
|468|512|u8.1|`w-UdjPr--`|[urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/atmega328p/watchdog_2_s/internal_oscillator_b-8.75%25/%2B8m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr.hex)|
|492|512|u8.1|`we-dhpr-c`|[urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/atmega328p/watchdog_2_s/internal_oscillator_b-8.75%25/%2B8m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_ee_ce_hw.hex)|
|504|512|u8.1|`w-UdjPr-c`|[urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/atmega328p/watchdog_2_s/internal_oscillator_b-8.75%25/%2B8m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ce.hex)|
|504|512|u8.1|`weUdjPr--`|[urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/atmega328p/watchdog_2_s/internal_oscillator_b-8.75%25/%2B8m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ee.hex)|
|506|512|u8.1|`we-djPr-c`|[urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/ursense/atmega328p/watchdog_2_s/internal_oscillator_b-8.75%25/%2B8m000000_hz/%2B%2B76k8_baud/uart0_rxd0_txd1/template_dual/urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `d` dual boot (over-the-air programming from external SPI flash)
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `b8m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 8.0 MHz - 8.75%
  + `76k8` shows the fixed communication baud rate, here 76800 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `template` bootloaders contains `mov rx,rx` nops as placeholders for LED and CS operations
  + `dual` can upload from external SPI flash memory and from serial interface
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega328p WDTO=2S F_CPU=7300000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual
make MCU=atmega328p WDTO=2S F_CPU=7300000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr
make MCU=atmega328p WDTO=2S F_CPU=7300000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_ee_ce_hw
make MCU=atmega328p WDTO=2S F_CPU=7300000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ce
make MCU=atmega328p WDTO=2S F_CPU=7300000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ee
make MCU=atmega328p WDTO=2S F_CPU=7300000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfaf -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=58 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=7300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfaf -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=44 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=7300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=7300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_ee_ce_hw.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfc6 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=9 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=7300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfcb -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=8 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=7300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcfd8 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=5 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega328p -DF_CPU=7300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m328p_2s_b8m0_76k8_swio_rxd0_txd1_template_dual_pr_ee_ce.elf urboot.c
```

