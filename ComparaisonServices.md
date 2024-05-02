# Comparaison liste des services

Liste  a l'installation de la machine
```
monadmin@MON1-MonSrv2:~$ sudo systemctl --type=service
  UNIT                               LOAD   ACTIVE SUB     DESCRIPTION
  apparmor.service                   loaded active exited  Load AppArmor profiles
  console-setup.service              loaded active exited  Set console font and keymap
  cron.service                       loaded active running Regular background program processing daemon
  dbus.service                       loaded active running D-Bus System Message Bus
  getty@tty1.service                 loaded active running Getty on tty1
  ifup@ens33.service                 loaded active exited  ifup for ens33
  ifupdown-pre.service               loaded active exited  Helper to synchronize boot up for ifupdown
  keyboard-setup.service             loaded active exited  Set the console keyboard layout
  kmod-static-nodes.service          loaded active exited  Create List of Static Device Nodes
  networking.service                 loaded active exited  Raise network interfaces
  open-vm-tools.service              loaded active running Service for virtual machines hosted on VMware
  ssh.service                        loaded active running OpenBSD Secure Shell server
  systemd-binfmt.service             loaded active exited  Set Up Additional Binary Formats
  systemd-journal-flush.service      loaded active exited  Flush Journal to Persistent Storage
  systemd-journald.service           loaded active running Journal Service
  systemd-logind.service             loaded active running User Login Management
  systemd-modules-load.service       loaded active exited  Load Kernel Modules
  systemd-random-seed.service        loaded active exited  Load/Save Random Seed
  systemd-remount-fs.service         loaded active exited  Remount Root and Kernel File Systems
  systemd-sysctl.service             loaded active exited  Apply Kernel Variables
  systemd-sysusers.service           loaded active exited  Create System Users
  systemd-timesyncd.service          loaded active running Network Time Synchronization
  systemd-tmpfiles-setup-dev.service loaded active exited  Create Static Device Nodes in /dev
  systemd-tmpfiles-setup.service     loaded active exited  Create Volatile Files and Directories
  systemd-udev-trigger.service       loaded active exited  Coldplug All udev Devices
  systemd-udevd.service              loaded active running Rule-based Manager for Device Events and Files
  systemd-update-utmp.service        loaded active exited  Record System Boot/Shutdown in UTMP
  systemd-user-sessions.service      loaded active exited  Permit User Sessions
  user-runtime-dir@1000.service      loaded active exited  User Runtime Directory /run/user/1000
  user@1000.service                  loaded active running User Manager for UID 1000
  vgauth.service                     loaded active running Authentication service for virtual machines hosted on VMware`
  ```


  Liste apres l'installation

  