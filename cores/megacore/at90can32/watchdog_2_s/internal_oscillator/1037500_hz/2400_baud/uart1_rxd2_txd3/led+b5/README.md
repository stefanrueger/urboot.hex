The AT90CAN32 exhibits a UART baud rate quantisation error of +0.07% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.07% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|248|256|u8.0|`w---jPr--`|[urboot_at90can32.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can32/watchdog_2_s/internal_oscillator/1037500_hz/2400_baud/uart1_rxd2_txd3/led%2Bb5/urboot_at90can32.hex)|
|248|256|u8.0|`w---jPr--`|[urboot_at90can32_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can32/watchdog_2_s/internal_oscillator/1037500_hz/2400_baud/uart1_rxd2_txd3/led%2Bb5/urboot_at90can32_pr.hex)|
|342|512|u8.0|`w-U-jPr-c`|[urboot_at90can32_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can32/watchdog_2_s/internal_oscillator/1037500_hz/2400_baud/uart1_rxd2_txd3/led%2Bb5/urboot_at90can32_pr_ce.hex)|
|356|512|u8.0|`weU-jPr--`|[urboot_at90can32_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can32/watchdog_2_s/internal_oscillator/1037500_hz/2400_baud/uart1_rxd2_txd3/led%2Bb5/urboot_at90can32_pr_ee.hex)|
|398|512|u8.0|`weU-jPr-c`|[urboot_at90can32_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can32/watchdog_2_s/internal_oscillator/1037500_hz/2400_baud/uart1_rxd2_txd3/led%2Bb5/urboot_at90can32_pr_ee_ce.hex)|
|384|1024|u8.0|`weU-hpr-c`|[urboot_at90can32_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/cores/megacore/at90can32/watchdog_2_s/internal_oscillator/1037500_hz/2400_baud/uart1_rxd2_txd3/led%2Bb5/urboot_at90can32_ee_ce_hw.hex)|

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
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=at90can32 WDTO=2S F_CPU=8300000L BAUD_RATE=19200 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5
make MCU=at90can32 WDTO=2S F_CPU=8300000L BAUD_RATE=19200 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5_pr
make MCU=at90can32 WDTO=2S F_CPU=8300000L BAUD_RATE=19200 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5_pr_ce
make MCU=at90can32 WDTO=2S F_CPU=8300000L BAUD_RATE=19200 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5_pr_ee
make MCU=at90can32 WDTO=2S F_CPU=8300000L BAUD_RATE=19200 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5_pr_ee_ce
make MCU=at90can32 WDTO=2S F_CPU=8300000L BAUD_RATE=19200 UARTNUM=1 RX=AtmelPD2 TX=AtmelPD3 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB5 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=22 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can32 -DF_CPU=8300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x7f00 -Wl,--section-start=.version=0x7ffa -DFRILLS=4 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can32 -DF_CPU=8300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf73 -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=170 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can32 -DF_CPU=8300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf7a -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=156 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can32 -DF_CPU=8300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7e00UL -DRJMPWP=0xcf8f -Wl,--section-start=.text=0x7e00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=114 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can32 -DF_CPU=8300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x7c00UL -DRJMPWP=0xce8f -Wl,--section-start=.text=0x7c00 -Wl,--section-start=.version=0x7ffa -DFRILLS=10 -D_urboot_AVAILABLE=640 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=at90can32 -DF_CPU=8300000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB5 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=1 -DTX=AtmelPD3 -DRX=AtmelPD2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_c32_2s_l8m0_19k2_uart1_rxd2_txd3_led+b5_ee_ce_hw.elf urboot.c
```

