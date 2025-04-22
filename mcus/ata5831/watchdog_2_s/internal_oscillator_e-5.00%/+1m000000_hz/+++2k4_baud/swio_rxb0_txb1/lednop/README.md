The ATA5831 exhibits a SWIO baud rate quantisation error of -0.04% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.04% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u8.0|`w---jpr--`|[urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/watchdog_2_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/swio_rxb0_txb1/lednop/urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop.hex)|
|254|256|u8.0|`w---jpr--`|[urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/watchdog_2_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/swio_rxb0_txb1/lednop/urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop_pr.hex)|
|300|320|u8.0|`w---jpr-c`|[urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/watchdog_2_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/swio_rxb0_txb1/lednop/urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop_pr_ce.hex)|
|316|320|u8.0|`we--jpr--`|[urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/watchdog_2_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/swio_rxb0_txb1/lednop/urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop_pr_ee.hex)|
|382|384|u8.0|`weU-jpr-c`|[urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/watchdog_2_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/swio_rxb0_txb1/lednop/urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop_pr_ee_ce.hex)|
|372|20464|u8.0|`-eU-hpr-c`|[urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata5831/watchdog_2_s/internal_oscillator_e-5.00%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/swio_rxb0_txb1/lednop/urboot_a5831_2s_e1m0_2k4_swio_rxb0_txb1_lednop_ee_ce_hw.hex)|

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
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `e1m0` is F<sub>CPU</sub> of a too slow internal oscillator, here 1.0 MHz - 5.00%
  + `2k4` shows the fixed communication baud rate, here 2400 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `lednop` is a template bootloader with `mov rx,rx` nops as placeholders for LED operations
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=ata5831 WDTO=2S F_CPU=7600000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop
make MCU=ata5831 WDTO=2S F_CPU=7600000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop_pr
make MCU=ata5831 WDTO=2S F_CPU=7600000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop_pr_ce
make MCU=ata5831 WDTO=2S F_CPU=7600000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop_pr_ee
make MCU=ata5831 WDTO=2S F_CPU=7600000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop_pr_ee_ce
make MCU=ata5831 WDTO=2S F_CPU=7600000L BAUD_RATE=19200 SWIO=1 RX=AtmelPB0 TX=AtmelPB1 VBL=0 EEPROM=1 CHIP_ERASE=1 TEMPLATE=1 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 PGMWRITEPAGE=0 NAME=urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x4f00UL -DRJMPWP=0xcfe4 -Wl,--section-start=.text=0x4f00 -Wl,--section-start=.version=0x4ffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5831 -DF_CPU=7600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x4f00UL -DRJMPWP=0xcfe4 -Wl,--section-start=.text=0x4f00 -Wl,--section-start=.version=0x4ffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5831 -DF_CPU=7600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x4ec0UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x4ec0 -Wl,--section-start=.version=0x4ffa -DFRILLS=5 -D_urboot_AVAILABLE=20 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5831 -DF_CPU=7600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x4ec0UL -DRJMPWP=0xcfe1 -Wl,--section-start=.text=0x4ec0 -Wl,--section-start=.version=0x4ffa -DFRILLS=3 -D_urboot_AVAILABLE=4 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5831 -DF_CPU=7600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x4e80UL -DRJMPWP=0xcfd5 -Wl,--section-start=.text=0x4e80 -Wl,--section-start=.version=0x4ffa -DFRILLS=6 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5831 -DF_CPU=7600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x0UL -DRJMPWP=0x9508 -Wl,--section-start=.text=0x0 -Wl,--section-start=.version=0x4ffa -DFRILLS=10 -D_urboot_AVAILABLE=20092 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata5831 -DF_CPU=7600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DTEMPLATE=1 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPB1 -DRX=AtmelPB0 -DPGMWRITEPAGE=0 -Wl,--relax -nostartfiles -nostdlib -o urboot_a5831_2s_e8m0_19k2_swio_rxb0_txb1_lednop_ee_ce_hw.elf urboot.c
```

