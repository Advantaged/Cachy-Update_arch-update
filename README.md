# Cachy-Update_arch-update
## Additional Settings
### Wherw to find the file:
``~/.config/systemd/user/timers.target.wants/arch-update.timer`
### 1. Short explanation:
* `~/.config` mean `/home/username(your name)/.(hidden folder or file) config/…`
* Enable by removing `#` & Disable by adding `#` on front of the line/command.
* If you add `Persistent=true`, you should disable `OnStartupSec=15` with a `#` on front like below.
* Further setting options for `systemd.time` on [Freedesktop.org](https://www.freedesktop.org/software/systemd/man/latest/systemd.time.html#Parsing%20Time%20Spans).

### 2. How to:

* Open `~/.config/systemd/user/timers.target.wants/arch-update.timer` with an editor at your choice.
* Replace original text with the following & assure an empty line at end is present.
```
[Unit]
#Description=Run arch-update auto check at boot and then every hour
#Description=Run arch-update auto check at boot and then every 5 days
Description=Run arch-update auto check at boot and then every Monday

[Timer]
OnStartupSec=15
#OnUnitActiveSec=1h
#OnUnitActiveSec=5d
OnCalendar=Mon *-*-* 09:09:09
Persistent=true

[Install]
WantedBy=timers.target

```

* Reload the 'daemon' if already enabled & started: `systemctl --user daemon-reload`
* If the 'daemon' is not yet enabled & started: `systemctl --user enable --now arch-update.timer`
* If you want make it step-by-step, execute following two commands:

```
systemctl --user enable arch-update.timer

systemctl --user start arch-update.timer

```

### 3. Check everything is OK:

* Use following command: `systemctl --user status arch-update.timer`
* Here the output:
```
systemctl --user status arch-update.timer
● arch-update.timer - Run arch-update auto check at boot and then every Monday
     Loaded: loaded (/usr/lib/systemd/user/arch-update.timer; enabled; preset: enabled)
     Active: active (waiting) since Thu 2025-09-04 10:21:07 CEST; 2h 47min ago
 Invocation: 326ec25c3c9b4af2bbdfd6fb637e9558
    Trigger: Mon 2025-09-08 09:09:09 CEST; 3 days left
   Triggers: ● arch-update.service

Sep 04 10:21:07 cachyos-zfs-disk-2 systemd[1696]: Started Run arch-update auto check at boot and then every hour.
```
* After restart you get following output:
```
systemctl --user status arch-update.timer
● arch-update.timer - Run arch-update auto check at boot and then every Monday
     Loaded: loaded (/usr/lib/systemd/user/arch-update.timer; enabled; preset: enabled)
     Active: active (waiting) since Sun 2025-09-07 15:40:24 CEST; 16min ago
 Invocation: abb6359841f542d8a1709218fc4bf640
    Trigger: Mon 2025-09-08 09:09:09 CEST; 17h left
   Triggers: ● arch-update.service

Sep 07 15:40:24 cachyos-zfs-disk-2 systemd[1714]: Started Run arch-update auto check at boot and then every Monday.
```




