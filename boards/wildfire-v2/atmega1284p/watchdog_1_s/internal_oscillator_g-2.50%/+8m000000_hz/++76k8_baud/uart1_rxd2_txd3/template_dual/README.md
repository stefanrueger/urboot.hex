The ATmega1284P exhibits a SWIO baud rate quantisation error of -0.43% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.43% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|500|512|u8.1|`w-UdjPr--`|[urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/wildfire-v2/atmega1284p/watchdog_1_s/internal_oscillator_g-2.50%25/%2B8m000000_hz/%2B%2B76k8_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual.hex)|
|500|512|u8.1|`w-UdjPr--`|[urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/wildfire-v2/atmega1284p/watchdog_1_s/internal_oscillator_g-2.50%25/%2B8m000000_hz/%2B%2B76k8_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr.hex)|
|512|512|u8.1|`w-UdjPr-c`|[urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/wildfire-v2/atmega1284p/watchdog_1_s/internal_oscillator_g-2.50%25/%2B8m000000_hz/%2B%2B76k8_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ce.hex)|
|512|512|u8.1|`we-djPr--`|[urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/wildfire-v2/atmega1284p/watchdog_1_s/internal_oscillator_g-2.50%25/%2B8m000000_hz/%2B%2B76k8_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ee.hex)|
|608|768|u8.1|`weUdjPr-c`|[urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/wildfire-v2/atmega1284p/watchdog_1_s/internal_oscillator_g-2.50%25/%2B8m000000_hz/%2B%2B76k8_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ee_ce.hex)|
|590|1024|u8.1|`weUdhpr-c`|[urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/wildfire-v2/atmega1284p/watchdog_1_s/internal_oscillator_g-2.50%25/%2B8m000000_hz/%2B%2B76k8_baud/uart1_rxd2_txd3/template_dual/urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_ee_ce_hw.hex)|

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
  + `1s` watchdog timeout, ie, time window for upload after external reset
  + `g8m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 8.0 MHz - 2.50%
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
make MCU=atmega1284p WDTO=1S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual
make MCU=atmega1284p WDTO=1S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr
make MCU=atmega1284p WDTO=1S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ce
make MCU=atmega1284p WDTO=1S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ee
make MCU=atmega1284p WDTO=1S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ee_ce
make MCU=atmega1284p WDTO=1S F_CPU=7800000L BAUD_RATE=76800 SWIO=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 DUAL=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfbb -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=30 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=7800000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfbb -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=12 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=7800000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfcb -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=6 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=7800000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=5 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=7800000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fd00UL -DRJMPWP=0xcf71 -Wl,--section-start=.text=0x1fd00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=160 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=7800000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xcef1 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=434 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1284p -DF_CPU=7800000L -Wno-clobbered -DWDTO=1S -DAUTOBAUD=0 -DBAUD_RATE=76800 -DTEMPLATE=1 -DBLINK=1 -DDUAL=1 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1284p_1s_g8m0_76k8_swio_rxd2_txd3_template_dual_ee_ce_hw.elf urboot.c
```

