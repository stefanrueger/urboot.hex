The ATmega644P exhibits a SWIO baud rate quantisation error of -0.17% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.17% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|254|256|u7.7|`w-u-jpr--`|[urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega644p/watchdog_2_s/internal_oscillator_q%2B10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/no-led/urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led.hex)|
|276|512|u7.7|`w-u-jPr--`|[urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega644p/watchdog_2_s/internal_oscillator_q%2B10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/no-led/urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr.hex)|
|300|512|u7.7|`w-u-jPr-c`|[urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega644p/watchdog_2_s/internal_oscillator_q%2B10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/no-led/urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ce.hex)|
|338|512|u7.7|`weu-jPr--`|[urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega644p/watchdog_2_s/internal_oscillator_q%2B10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/no-led/urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ee.hex)|
|362|512|u7.7|`weu-jPr-c`|[urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega644p/watchdog_2_s/internal_oscillator_q%2B10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/no-led/urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ee_ce.hex)|
|348|1024|u7.7|`weu-hpr-c`|[urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_ee_ce_hw.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega644p/watchdog_2_s/internal_oscillator_q%2B10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/no-led/urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_ee_ce_hw.hex)|
|452|1024|u7.7|`wes-hpr-c`|[urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_ee_ce_hw_stk500.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/u7.7/mcus/atmega644p/watchdog_2_s/internal_oscillator_q%2B10.00%25/%2B0m128000_hz/%2B%2B%2B0k6_baud/uart0_rxd0_txd1/no-led/urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_ee_ce_hw_stk500.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `u` uses urprotocol requiring `avrdude -c urclock` for programming
  + `s` uses skeleton of STK500v1 protocol (deprecated); `-c urclock` and `-c arduino` both work
  + `h` hardware boot section: make sure fuses are set for reset to jump to boot section
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `p` bootloader protects itself from being overwritten
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `q0m128` is F<sub>CPU</sub> of a too fast internal oscillator, here 0.128 MHz + 10.00%
  + `0k6` shows the fixed communication baud rate, here 600 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command
  + `hw` hardware supported bootloader: set fuses to jump to the HW boot section, not to addr 0
  + `stk500` uses deprecated STK500v1 protocol to communicate with bootloader


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=atmega644p WDTO=2S F_CPU=140800L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led
make MCU=atmega644p WDTO=2S F_CPU=140800L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr
make MCU=atmega644p WDTO=2S F_CPU=140800L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ce
make MCU=atmega644p WDTO=2S F_CPU=140800L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ee
make MCU=atmega644p WDTO=2S F_CPU=140800L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ee_ce
make MCU=atmega644p WDTO=2S F_CPU=140800L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=1 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_ee_ce_hw
make MCU=atmega644p WDTO=2S F_CPU=140800L BAUD_RATE=600 SWIO=1 RX=AtmelPD0 TX=AtmelPD1 VBL=0 EEPROM=1 CHIP_ERASE=1 URPROTOCOL=0 BLINK=0 AUTOFRILLS=0,6,4,3,2 NAME=urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_ee_ce_hw_stk500
```

### Avr-gcc commands
```
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xff00UL -DRJMPWP=0xcfe3 -Wl,--section-start=.text=0xff00 -Wl,--section-start=.version=0xfffa -DFRILLS=4 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644p -DF_CPU=140800L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf67 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=236 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644p -DF_CPU=140800L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr.elf urboot.c
./avr-toolchain/4.8.1/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf73 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=212 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644p -DF_CPU=140800L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=600 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf86 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=174 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644p -DF_CPU=140800L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ee.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfe00UL -DRJMPWP=0xcf92 -Wl,--section-start=.text=0xfe00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=150 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644p -DF_CPU=140800L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_pr_ee_ce.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xce92 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=676 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644p -DF_CPU=140800L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=1 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_ee_ce_hw.elf urboot.c
./avr-toolchain/5.4.0/bin/avr-gcc -DSTART=0xfc00UL -DRJMPWP=0xcec6 -Wl,--section-start=.text=0xfc00 -Wl,--section-start=.version=0xfffa -DFRILLS=6 -D_urboot_AVAILABLE=572 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=atmega644p -DF_CPU=140800L -Wno-clobbered -DWDTO=2S -DBAUD_RATE=600 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DURPROTOCOL=0 -DVBL=0 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPD1 -DRX=AtmelPD0 -Wl,--relax -nostartfiles -nostdlib -o urboot_m644p_2s_q0m128_0k6_swio_rxd0_txd1_no-led_ee_ce_hw_stk500.elf urboot.c
```

