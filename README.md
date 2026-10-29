## Build and flash application
```
export BOARD=nucleo_h563zi/stm32h563xx

source ../.venv/bin/activate
west build .

# or explicit
# west build -b nucleo_h563zi/stm32h563xx .

west flash
```
## Initial installation
Mostly based on https://docs.zephyrproject.org/latest/develop/getting_started/index.html
### Installing west
```
sudo apt install --no-install-recommends git cmake ninja-build gperf \
  ccache dfu-util device-tree-compiler wget python3-dev python3-venv python3-tk \
  xz-utils file make gcc gcc-multilib g++-multilib libsdl2-dev libmagic1
```

```
mkdir ~/zephyr-workspace/
python3 -m venv ~/zephyr-workspace/.venv
source ~/zephyr-workspace/.venv/bin/activate
pip install west
west init -m https://github.com/zephyrproject-rtos/zephyr ~/zephyr-workspace
cd ~/zephyr-workspace
west update
west packages pip --install
west zephyr-export
```

### Installing SDK
```
cd ~/zephyr-workspace/zephyr
west sdk install
```

### Basic test example

```
cd ~/zephyr-workspace/zephyr
#Change nucleo_h563zi/stm32h563xx for your board
west build -p always -b nucleo_h563zi/stm32h563xx samples/basic/blinky
```

### Flashing

Download from https://www.st.com/content/st_com/en/stm32cubeprogrammer.html
Alledgly you can download it with an email verification without making an account but i never had such luck, just make the account.


```
sudo cp ~/STMicroelectronics/STM32Cube/STM32CubeProgrammer/Drivers/rules/*.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules
sudo udevadm trigger
```

```
west flash
```

### Proper project structure
`zephyr-workspace` can contain multiple Zephyr projects. Most sane to create these as individial repos
