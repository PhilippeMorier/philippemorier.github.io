---
title: OGN
definition: Open Glider Network
tags: paragliding tracker gps ogn esp idf ttgo t-beam
---

1. Install
   [ESP-IDF (Espressif IoT Development Framework)](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/index.html#step-1-install-prerequisites)

   - If error `unrecognized arguments: --no-site-packages` then remove
     `--no-site-packages` from line 1181 so that the line looks like:
     ```python
       subprocess.check_call([sys.executable, '-m', 'virtualenv', idf_python_env_path],
     ```
   - rerun `./install.sh`
   - run `. ./export.sh`

1. Follow https://github.com/pjalocha/esp32-ogn-tracker

   - Get the config for OLED screen: `cp T-Beam_v10_OLED.cfg main/config.h`

   - source esp-idf with `source ~/esp-idf/export.sh` in order to be able to run
     `make` command

   - use `ls /dev/tty* | grep usb` to discover serial ports (e.g. when TTGO
     connected via USB-C adapter)
   - flash with proper port name:
     `make flash ESPPORT=/dev/tty.usbserial-0212BE43`

   - AFAIK this is not needed if above step is applied

     - `/dev/ttyUSB0` is not available on MacOS, it is `/dev/tty.SLAB_USBtoUART`
       change the `--port` param to use `/dev/tty.SLAB_USBtoUART` in the
       following flash command:

       ```bash
       python /Users/philippe/git/esp-idf/components/esptool_py/esptool/esptool.py --chip esp32 --port /dev/tty.SLAB_USBtoUART --baud 921600 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 40m --flash_size detect 0x1000 /Users/philippe/git/esp32-ogn-tracker/build/bootloader/bootloader.bin 0x10000 /Users/philippe/git/esp32-ogn-tracker/build/app-template.bin 0x8000 /Users/philippe/git/esp32-ogn-tracker/build/partitions.bin
       ```

   -`brew install minicom` -`man minicom` // shows add the bottom the path to
   `minirc.dfl` (`/usr/local/Cellar/minicom/2.8/etc`)
   `/usr/local/Cellar/minicom/2.8/etc/`

   - `/dev/tty.SLAB_USBtoUART` OR
   - `/dev/tty.usbserial-0212BE43`
   - edit `minirc.dfl` to set port, baudrate and turn hardware and software
     handshake OFF
     ```bash
     pu lock /usr/local/Cellar/minicom/2.8/var
     pu escape-key Escape (Meta)
     pr port             /dev/tty.SLAB_USBtoUART
     pu baudrate         115200
     pu rtscts           No
     pu xonxoff          No
     ```
   - connect with `minicom`
     - Ctrl-C - lists internal state, internal log files and current parameter
       values.
     - Ctrl-L - list internal log files
     - Ctrl-V - hold the NMEA stream for 1 min
     - Ctrl-X - restarts the system

1. Install Android IDE with expressif

   - https://github.com/espressif/arduino-esp32/blob/master/docs/arduino-ide/boards_manager.md

1. OLED driver `SSD1306`

1. http://wiki.glidernet.org/wiki:manual-installation-guide
