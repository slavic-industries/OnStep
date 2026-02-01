OnStep EQ5 Telescope Controller
===========================
# Smart Telescope Mount Controller

Custom OnstepX firmware for Skywatcher EQ5 mount with a custom RPi hat PCB.
Based on the [OnStep Project](https://groups.io/g/onstep/wiki/home).

# Hardware Used
* Skywatcher EQ5 mount
* Onstep MaxSTM 3.63 PCB
  * TMC5160 driver for RA and DEC axis 
* Stepper motor model: [17HM19-1684S](https://www.omc-stepperonline.com/nema-17-bipolar-0-9deg-44ncm-62-3oz-in-1-68a-2-8v-42x42x47mm-4-wires-17hm19-1684s)
  * 400 $[step/rev]$
  * 1.68 $[A]$
* RA gear ratio: 
  * 3:1 timing belt * 144:1 worm gear
  * Stepper driver set to 32 microsteps
* DEC gear ratio: 
  * 3:1 timing belt * 144:1 worm gear
  * Stepper driver set to 32 microsteps

# Compiling

## Use `arduino-cli`

### Installing on x86_64 architectures
  - Install `arduino-cli` with `sudo snap install arduino-cli`

### Installing on ARM architectures (RPi)
  - In a new terminal go to your user home directory
  - Install `arduino-cli` with `curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | sh`
    - This installs to `~/bin/arduino-cli`
  - Add the installed folder to PATH
    - `echo 'export PATH=$PATH:$HOME/bin' >> ~/.bashrc && source ~/.bashrc`
  - Test with: `arduino-cli version`

  - Update the cli: `arduino-cli config init`
  - Add the link to STM32 boards: `arduino-cli config add board_manager.additional_urls https://github.com/stm32duino/BoardManagerFiles/raw/main/package_stmicroelectronics_index.json`
  - Update the Arduino index: `arduino-cli core update-index`
  - Instal STM32 boards: `arduino-cli core install STMicroelectronics:stm32`
  - Install the The Makuna RTC Library for DS3231 or DS3234 (version 2.3.5 - Necessary for OnstepX): `arduino-cli lib install "Rtc by Makuna@2.3.5"`


- Compile
  - Open a terminal in the root firmware directory
  - Type: `arduino-cli compile -v --fqbn STMicroelectronics:stm32:GenF4:pnum=BLACKPILL_F411CE --output-dir build .`
  - THe compiled `.bin` file will be in the `/build` folder


## AOB

- Testing compiling and flashing process with [stm32_flash.py](https://github.com/slavic-industries/stm32_flash) -> `compile_aqndflash_with_arduino` branch.