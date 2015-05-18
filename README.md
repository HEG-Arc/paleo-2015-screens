# paleo-2015-screens
Raspberry Pi configuration to act a signage devices

- start a full screen browser on bootup
- get a specific URL
- http://blogs.wcode.org/2013/09/howto-boot-your-raspberry-pi-into-a-fullscreen-browser-kiosk/

## Install

First, we need some packackages

``$ sudo apt-get install chromium matchbox x11-xserver-utils ttf-mscorefonts-installer libnss3 xwit sqlite3``

Second, create a new ``screen`` user with password *screen*

``$ sudo adduser screen``

Third, copy the ``boot-screen.sh`` script in the ``/boot`` folder

Fourth, enable auto-login of user ``screen``. Edit the ``/etc/inittab`` file by replacing line 54:

``1:2345:respawn:/sbin/getty --noclear 38400 tty1``

by:

``1:2345:respawn:/bin/login -f pi tty1 </dev/tty1 >/dev/tty1 2>&1``

Fifth, run ``boot-screen.sh`` at boot by adding the following to ``/etc/rc.local``:

```
if [ -f /boot/boot-screen.sh ]; then
	ln -fs /boot/boot-screen.sh /home/screen/.xinitrc;
	su - screen -c 'startx' &
fi
```

Sixth, copy ``screen.cfg`` to ``/home/screen`` and edit the ``start_url`` value to fit your needs

That's all, reboot and enjoy!


