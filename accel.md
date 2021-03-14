# Accelerometer

## Requirements:

* Python3 (preferable).
* PySerial installed.
* accel.py

## Verification list:

* Check python version:

```
 $ python3 --version
```

* Check that PySerial is installed:

```
 $ python3 -c "import serial; print(serial.__version__)"
```

* Check that accel is connected:

First check tty connection:

```
 $ ls -lt /dev/ttyUSB*
```

```
crw-rw---- 1 root dialout 188, 0 Mar 12 07:39 /dev/ttyUSB0
```

In this example, the port is /dev/ttyUSB0

```
 $ udevadm info --a --name /dev/ttyUSB0
```

```
[...]

  looking at device '/devices/70090000.xusb/usb1/1-2/1-2.3/1-2.3:1.0/ttyUSB0/tty/ttyUSB0':
    KERNEL=="ttyUSB0"
    SUBSYSTEM=="tty"
    DRIVER==""

  looking at parent device '/devices/70090000.xusb/usb1/1-2/1-2.3/1-2.3:1.0/ttyUSB0':
    KERNELS=="ttyUSB0"
    SUBSYSTEMS=="usb-serial"
    DRIVERS=="pl2303"
    ATTRS{port_number}=="0"

[...]
```

If something similar is displayed, we can assume that the accelerometer is connected.

* Check disk free space

```
 $ df -h | grep ' /$'
```

The accel system requires around 1MB/min for data storage. df -h will help you determine if there's enough space.  If the system is not going to be left unattended for a few hours, this item sholudn't be a problem.


## Running the system

Before running the system, make sure all the items in the verification list are checked.

In order to start the system, simply run:

```
$ python3 accel.py
```

The information from the sensor will be retrieved and decoded and finally be saved to accel.csv

## Checking system status

The fastest way to determine if the system is operational is by running:

```
$ tail -f accel.csv
```

This command will output in real time the contents of the output file. The file should be updated a few times per second, so new lines should be displayed in the terminal.  To finish this command press Ctrl+C.


