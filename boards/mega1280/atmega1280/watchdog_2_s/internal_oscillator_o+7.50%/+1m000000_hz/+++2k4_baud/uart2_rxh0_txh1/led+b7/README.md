The ATmega1280 exhibits a UART baud rate quantisation error of -0.02% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.02% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---jPr--`|[urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led+b7.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_2_s/internal_oscillator_o%2B7.50%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart2_rxh0_txh1/led%2Bb7/urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led%2Bb7.hex)|
|256|256|u8.0|`w---jPr--`|[urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led+b7_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_2_s/internal_oscillator_o%2B7.50%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart2_rxh0_txh1/led%2Bb7/urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led%2Bb7_pr.hex)|
|362|512|u8.0|`w-U-jPr-c`|[urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led+b7_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_2_s/internal_oscillator_o%2B7.50%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart2_rxh0_txh1/led%2Bb7/urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led%2Bb7_pr_ce.hex)|
|366|512|u8.0|`weU-jPr--`|[urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led+b7_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_2_s/internal_oscillator_o%2B7.50%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart2_rxh0_txh1/led%2Bb7/urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led%2Bb7_pr_ee.hex)|
|418|512|u8.0|`weU-jPr-c`|[urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led+b7_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_2_s/internal_oscillator_o%2B7.50%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart2_rxh0_txh1/led%2Bb7/urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led%2Bb7_pr_ee_ce.hex)|
|400|1024|u8.0|`weU-hpr-c`|[urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led+b7_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/boards/mega1280/atmega1280/watchdog_2_s/internal_oscillator_o%2B7.50%25/%2B1m000000_hz/%2B%2B%2B2k4_baud/uart2_rxh0_txh1/led%2Bb7/urboot_m1280_2s_o1m0_2k4_uart2_rxh0_txh1_led%2Bb7_ee_ce_hw.hex)|

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
  + `o1m0` is F<sub>CPU</sub> of a too fast internal oscillator, here 1.0 MHz + 7.50%
  + `2k4` shows the fixed communication baud rate, here 2400 baud
  + `uart2` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `led+b7` toggles an active-high (`+`) LED on pin `B7`
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega1280 WDTO=2S F_CPU=8600000L BAUD_RATE=19200 UARTNUM=2 RX=AtmelPH0 TX=AtmelPH1 VBL=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7
make MCU=atmega1280 WDTO=2S F_CPU=8600000L BAUD_RATE=19200 UARTNUM=2 RX=AtmelPH0 TX=AtmelPH1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7_pr
make MCU=atmega1280 WDTO=2S F_CPU=8600000L BAUD_RATE=19200 UARTNUM=2 RX=AtmelPH0 TX=AtmelPH1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7_pr_ce
make MCU=atmega1280 WDTO=2S F_CPU=8600000L BAUD_RATE=19200 UARTNUM=2 RX=AtmelPH0 TX=AtmelPH1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7_pr_ee
make MCU=atmega1280 WDTO=2S F_CPU=8600000L BAUD_RATE=19200 UARTNUM=2 RX=AtmelPH0 TX=AtmelPH1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7_pr_ee_ce
make MCU=atmega1280 WDTO=2S F_CPU=8600000L BAUD_RATE=19200 UARTNUM=2 RX=AtmelPH0 TX=AtmelPH1 VBL=0 EEPROM=1 CHIP_ERASE=1 LED=AtmelPB7 BLINK=1 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7_ee_ce_hw
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=4 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=8600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=2 -DTX=AtmelPH1 -DRX=AtmelPH0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1ff00UL -DRJMPWP=0xcfd7 -Wl,--section-start=.text=0x1ff00 -Wl,--section-start=.version=0x1fffa -DFRILLS=4 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=8600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=2 -DTX=AtmelPH1 -DRX=AtmelPH0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf76 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=150 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=8600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=2 -DTX=AtmelPH1 -DRX=AtmelPH0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf78 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=146 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=8600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=2 -DTX=AtmelPH1 -DRX=AtmelPH0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fe00UL -DRJMPWP=0xcf92 -Wl,--section-start=.text=0x1fe00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=94 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=8600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=2 -DTX=AtmelPH1 -DRX=AtmelPH0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7_pr_ee_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x1fc00UL -DRJMPWP=0xce92 -Wl,--section-start=.text=0x1fc00 -Wl,--section-start=.version=0x1fffa -DFRILLS=10 -D_urboot_AVAILABLE=624 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega1280 -DF_CPU=8600000L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=19200 -DLED=AtmelPB7 -DBLINK=1 -DDUAL=0 -DEEPROM=1 -DVBL=0 -DCHIP_ERASE=1 -DUARTNUM=2 -DTX=AtmelPH1 -DRX=AtmelPH0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m1280_2s_o8m0_19k2_uart2_rxh0_txh1_led+b7_ee_ce_hw.elf urboot.c
```

