The ATA6617C exhibits a LINUART baud rate quantisation error of +1.69% for this F_CPU and baud rate combination. Assuming perfect F<sub>CPU</sub>, the actual baud rate is therefore 1.69% higher than wanted. An overall deviation (including that of the oscillator and that of the uploading computer) of up to 1.5% is well within communication tolerance. In practice, up to 2.5% deviation is likely to work with short cables and benign line noise.

|Size|Usage|Version|Features|Hex file|
|:-:|:-:|:-:|:-:|:--|
|246|256|u8.0|`w---jPr--`|[urboot_a6617c_2s_x7m3728_250k0_uart0_rxa0_txa1_no-led.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6617c/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxa0_txa1/no-led/urboot_a6617c_2s_x7m3728_250k0_uart0_rxa0_txa1_no-led.hex)|
|246|256|u8.0|`w---jPr--`|[urboot_a6617c_2s_x7m3728_250k0_uart0_rxa0_txa1_no-led_pr.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6617c/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxa0_txa1/no-led/urboot_a6617c_2s_x7m3728_250k0_uart0_rxa0_txa1_no-led_pr.hex)|
|254|256|u8.0|`w---jPr-c`|[urboot_a6617c_2s_x7m3728_250k0_uart0_rxa0_txa1_no-led_pr_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6617c/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxa0_txa1/no-led/urboot_a6617c_2s_x7m3728_250k0_uart0_rxa0_txa1_no-led_pr_ce.hex)|
|352|384|u8.0|`weU-jPr--`|[urboot_a6617c_2s_x7m3728_250k0_uart0_rxa0_txa1_no-led_pr_ee.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6617c/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxa0_txa1/no-led/urboot_a6617c_2s_x7m3728_250k0_uart0_rxa0_txa1_no-led_pr_ee.hex)|
|376|384|u8.0|`weU-jPr-c`|[urboot_a6617c_2s_x7m3728_250k0_uart0_rxa0_txa1_no-led_pr_ee_ce.hex](https://raw.githubusercontent.com/stefanrueger/urboot.hex/main/mcus/ata6617c/watchdog_2_s/external_oscillator_x/%2B7m372800_hz/%2B250k0_baud/uart0_rxa0_txa1/no-led/urboot_a6617c_2s_x7m3728_250k0_uart0_rxa0_txa1_no-led_pr_ee_ce.hex)|

- **Size:** Bootloader code size including small table at top end
- **Usage:** How many bytes of flash are needed, ie, HW boot section or a multiple of the page size
- **Version:** For example, u7.6 is an urboot version, o5.2 is an optiboot version
- **Features:**
  + `w` bootloader provides `pgm_write_page(sram, flash)` for the application at `FLASHEND-4+1`
  + `e` EEPROM read/write support
  + `U` checks whether flash pages need writing before doing so
  + `j` vector bootloader: applications *need to be patched externally*, eg, using `avrdude -c urclock`
  + `P` vector bootloader only: protects itself and reset vector from being overwritten
  + `r` preserves reset flags for the application in the register R2
  + `c` bootloader provides chip erase functionality (recommended for large MCUs)
  + `-` corresponding feature not present
- **Hex file:** often qualified by the MCU name and/or configuration
  + `2s` watchdog timeout, ie, time window for upload after external reset
  + `x7m3728` is F<sub>CPU</sub> of an external oscillator, here 7.3728 MHz
  + `250k0` shows the fixed communication baud rate, here 250000 baud
  + `uart0` UART number
  + `rxd0 txd1` I/O using, in this example, lines RX `D0` and TX `D1`
  + `no-led` bootloader does not operate LEDs
  + `pr` vector bootloader protecting the reset vector
  + `ee` bootloader supports EEPROM read/write
  + `ce` bootloader provides a chip erase command


Note below that baud rate and F<sub>CPU</sub> may be different from the path name's as long as the quotient F<sub>CPU</sub>/baud rate is the same.

### Make commands
```
make MCU=ata6617c WDTO=2S F_CPU=14745600L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6617c_2s_x14m7456_500k0_uart0_rxa0_txa1_no-led
make MCU=ata6617c WDTO=2S F_CPU=14745600L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6617c_2s_x14m7456_500k0_uart0_rxa0_txa1_no-led_pr
make MCU=ata6617c WDTO=2S F_CPU=14745600L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=0 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6617c_2s_x14m7456_500k0_uart0_rxa0_txa1_no-led_pr_ce
make MCU=ata6617c WDTO=2S F_CPU=14745600L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=0 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6617c_2s_x14m7456_500k0_uart0_rxa0_txa1_no-led_pr_ee
make MCU=ata6617c WDTO=2S F_CPU=14745600L BAUD_RATE=500000 UARTNUM=0 RX=AtmelPA0 TX=AtmelPA1 VBL=1 PROTECTRESET=1 EEPROM=1 CHIP_ERASE=1 BLINK=0 AUTOFRILLS=0,6,8..10,5,4,3,2 NAME=urboot_a6617c_2s_x14m7456_500k0_uart0_rxa0_txa1_no-led_pr_ee_ce
```

### Avr-gcc commands
```
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=24 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6617c -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6617c_2s_x14m7456_500k0_uart0_rxa0_txa1_no-led.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfd9 -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=5 -D_urboot_AVAILABLE=10 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6617c -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6617c_2s_x14m7456_500k0_uart0_rxa0_txa1_no-led_pr.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3f00UL -DRJMPWP=0xcfdd -Wl,--section-start=.text=0x3f00 -Wl,--section-start=.version=0x3ffa -DFRILLS=3 -D_urboot_AVAILABLE=2 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6617c -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=0 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6617c_2s_x14m7456_500k0_uart0_rxa0_txa1_no-led_pr_ce.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfb5 -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=10 -D_urboot_AVAILABLE=32 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6617c -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=0 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6617c_2s_x14m7456_500k0_uart0_rxa0_txa1_no-led_pr_ee.elf urboot.c
./avr-toolchain/7.3.0/bin/avr-gcc -DSTART=0x3e80UL -DRJMPWP=0xcfcb -Wl,--section-start=.text=0x3e80 -Wl,--section-start=.version=0x3ffa -DFRILLS=8 -D_urboot_AVAILABLE=8 -g -Wundef -Wall -Os -fno-split-wide-types -mrelax -mmcu=ata6617c -DF_CPU=14745600L -Wno-clobbered -DWDTO=2S -DAUTOBAUD=0 -DBAUD_RATE=500000 -DBLINK=0 -DDUAL=0 -DEEPROM=1 -DVBL=1 -DCHIP_ERASE=1 -DUARTNUM=0 -DTX=AtmelPA1 -DRX=AtmelPA0 -DPGMWRITEPAGE=1 -DPROTECTRESET=1 -Wl,--relax -nostartfiles -nostdlib -o urboot_a6617c_2s_x14m7456_500k0_uart0_rxa0_txa1_no-led_pr_ee_ce.elf urboot.c
```

