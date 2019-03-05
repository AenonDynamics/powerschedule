powerschedule
=============================

**run maschines like backup systems for a scheduled time**

## Features ##

* single file configuration - just set boot/shutdown time
* powersaving
* power-on task via [rtcwake](https://linux.die.net/man/8/rtcwake)
* power-off task via systemd [transient timers](https://wiki.archlinux.org/index.php/Systemd/Timers)
* debian package

## Usage ##

### Configuration ###

The poweron/poweroff settings can be configured within a single file. The time is parsed by [date](https://linux.die.net/man/1/date) and internally converted into a unix timestamp

File: `/etc/powerschedule.conf`

```bash
# daily schedule
# ##########################

# SYSTEM POWERON
# @syntax https://linux.die.net/man/1/date
DAILY_POWERON="20:00 CET"

# SYSTEM POWEROFF
# @syntax https://linux.die.net/man/1/date
DAILY_POWEROFF="23:30 CET"
```

### Enable Services ###

The script requires 2 systemd hooks to setup the schedules

* **on boot**: set the wakeup + shutdown time
* **on shutdown**: set the wakeup again to avoid stall conditions (systems running > 24h without automatic shutdown)

```bash
# enable systemd service
systemctl enable powerschedule.service

# setup initial wakeup+shutdown time (or reboot)
systemctl start powerschedule
```

## Contribution ##

The **.deb** package is automatically generated via a **Continuous Delivery Pipeline** - please do not build packages manually!

## License ##
powerschedule is OpenSource and licensed under the Terms of [Mozilla Public License 2.0](https://opensource.org/licenses/MPL-2.0). You're welcome to [contribute](docs/CONTRIBUTING.md)
