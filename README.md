# esp32-micropython
Tutorial for setting up esp32 on micropython in a virtual box environment.

Referencing: https://micropython.org/download/esp32/

Create an Ubuntu Virtual box.  Install guest additions and update all software. Restart the os.
Connect the esp to the computer using a usb cable.
In the Virtual Box menu, select "Devices"->"USB"-> "Settings..". 
Click the "Add USB Filter" and select the esp32 from the menu.  Should look like "Silicon Labs... Bridge Controller"
This should allow the usb connected to appear as /dev/ttyUSB0.
You won't have non-root access to this.  You need to change your users permissions.
```sudo usermod -a -G dialout $USER```
```sudo usermod -a -G tty $USER```

Go to: https://micropython.org/download/esp32/ and download the appropriate firmware.

now install esptool via the following command and ignore any bdist wheel failures
```pip install esptool``` 
now press the 'Boot' button on the device (or a similar button) and run
```esptool.py --chip esp32 --port /dev/ttyUSB0 erase_flash```

now press the 'Boot' button on the device (or a similar button) and run
```esptool.py --chip esp32 --port /dev/ttyUSB0 --baud 460800 write_flash -z 0x1000 <path to firmware binary>```

