The ATtiny441 exhibits a SWIO baud rate quantisation error of -0.15% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 0.15% lower than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|256|256|u8.0|`w---jPr--`|[urboot_t441_2s_k0m064_0k3_swio_rxa2_txa1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_2_s/internal_oscillator_k%2B2.50%25/%2B0m064000_hz/%2B%2B%2B0k3_baud/uart0_rxa2_txa1/no-led/urboot_t441_2s_k0m064_0k3_swio_rxa2_txa1_no-led.hex)|
|256|256|u8.0|`w---jPr--`|[urboot_t441_2s_k0m064_0k3_swio_rxa2_txa1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_2_s/internal_oscillator_k%2B2.50%25/%2B0m064000_hz/%2B%2B%2B0k3_baud/uart0_rxa2_txa1/no-led/urboot_t441_2s_k0m064_0k3_swio_rxa2_txa1_no-led_pr.hex)|
|302|320|u8.0|`w---jPr-c`|[urboot_t441_2s_k0m064_0k3_swio_rxa2_txa1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_2_s/internal_oscillator_k%2B2.50%25/%2B0m064000_hz/%2B%2B%2B0k3_baud/uart0_rxa2_txa1/no-led/urboot_t441_2s_k0m064_0k3_swio_rxa2_txa1_no-led_pr_ce.hex)|
|314|320|u8.0|`we--jPr--`|[urboot_t441_2s_k0m064_0k3_swio_rxa2_txa1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_2_s/internal_oscillator_k%2B2.50%25/%2B0m064000_hz/%2B%2B%2B0k3_baud/uart0_rxa2_txa1/no-led/urboot_t441_2s_k0m064_0k3_swio_rxa2_txa1_no-led_pr_ee.hex)|
|354|384|u8.0|`we--jPr-c`|[urboot_t441_2s_k0m064_0k3_swio_rxa2_txa1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/attiny441/watchdog_2_s/internal_oscillator_k%2B2.50%25/%2B0m064000_hz/%2B%2B%2B0k3_baud/uart0_rxa2_txa1/no-led/urboot_t441_2s_k0m064_0k3_swio_rxa2_txa1_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `k0m064` is F<sub>CPU</sub> of a too fast internal oscillator, here 0.064 MHz + 2.50%
  + `0k3` shows the fixed communication baud rate, here 300 baud
  + `swio` software I/O (not UART)
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=attiny441 WDTO=2S F_CPU=524800L BAUD_RATE=2400 SWIO=1 RX=AtmelPA2 TX=AtmelPA1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_2s_k0m512_2k4_swio_rxa2_txa1_no-led
make MCU=attiny441 WDTO=2S F_CPU=524800L BAUD_RATE=2400 SWIO=1 RX=AtmelPA2 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_2s_k0m512_2k4_swio_rxa2_txa1_no-led_pr
make MCU=attiny441 WDTO=2S F_CPU=524800L BAUD_RATE=2400 SWIO=1 RX=AtmelPA2 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_2s_k0m512_2k4_swio_rxa2_txa1_no-led_pr_ce
make MCU=attiny441 WDTO=2S F_CPU=524800L BAUD_RATE=2400 SWIO=1 RX=AtmelPA2 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_2s_k0m512_2k4_swio_rxa2_txa1_no-led_pr_ee
make MCU=attiny441 WDTO=2S F_CPU=524800L BAUD_RATE=2400 SWIO=1 RX=AtmelPA2 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_t441_2s_k0m512_2k4_swio_rxa2_txa1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=3 -D_urboot_AVAILABLE=14 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=524800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=2400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA1 -DRX=AtmelPA2 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_k0m512_2k4_swio_rxa2_txa1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xf00UL -DRJMPWP=0xcfdb -Wl,--section-start=.text=0xf00 -Wl,--section-start=.version=0xffa -DFRILLS=3 -D_urboot_AVAILABLE=0 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=524800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=2400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA1 -DRX=AtmelPA2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_k0m512_2k4_swio_rxa2_txa1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd0 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=10 -D_urboot_AVAILABLE=18 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=524800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=2400 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA1 -DRX=AtmelPA2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_k0m512_2k4_swio_rxa2_txa1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xec0UL -DRJMPWP=0xcfd6 -Wl,--section-start=.text=0xec0 -Wl,--section-start=.version=0xffa -DFRILLS=3 -D_urboot_AVAILABLE=6 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=524800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=2400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DSWIO=1 -DTX=AtmelPA1 -DRX=AtmelPA2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_k0m512_2k4_swio_rxa2_txa1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0xe80UL -DRJMPWP=0xcfca -Wl,--section-start=.text=0xe80 -Wl,--section-start=.version=0xffa -DFRILLS=10 -D_urboot_AVAILABLE=30 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=attiny441 -DF_CPU=524800L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=2400 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DSWIO=1 -DTX=AtmelPA1 -DRX=AtmelPA2 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_t441_2s_k0m512_2k4_swio_rxa2_txa1_no-led_pr_ee_ce.elf urboot.c
```

