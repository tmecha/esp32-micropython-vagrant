# ESP32 & MicroPython SDK Virtual Machine
Provision the virtual machine:
```
vagrant up
```
Shutdown the VM:
```
vagrant halt
```
## Enable USB passthrough
Go into `virtualbox` and select the VM `esp32-micropython-vagrant...`, then goto
`Settings->USB` click `add new USB filter` then select option `Silicon Labs CP2102 USB to UART Bridge Controller...`. 
If that option is not available make sure you have the driver installed: [see Adafruit's instructions](https://learn.adafruit.com/ladyadas-learn-arduino-lesson-number-0/install-software-mac-os-x#installing-silabs-cp210x-drivers).
Then edit the filter, changing name to `ESP32` and deleting all fields except `Vendor ID` and `Product ID`.

## Build firmware
```
vagrant up
vagrant ssh
cd open-eio/micropython-esp32/esp32
make erase
make deploy
```
## Test REPL
Note that it is necessary to halt the VM in order to reobtain the USB device in the host environment: 
```
exit
vagrant halt
```
For example, on linux:
```
screen /dev/ttyUSB0 115200
```
Hit keystroke `<ctrl-d>`
Then you should see output similar to this:
```
>>> 
PYB: soft reboot
could not open file 'boot.py' for reading
could not open file 'main.py' for reading
MicroPython v1.8.6-649-g22c2ed7 on 2017-03-14; ESP32 module with ESP32
Type "help()" for more information.
>>> 

```
