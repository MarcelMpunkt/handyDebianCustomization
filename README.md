# handyDebianCustomization
Handy Customizations for debianbased LinuxDistros (like Ubuntu,...)
Please feel free to expand the list further 👍

## 1. Update system without requesting a password (as non-administrative user)

edit __/etc/sudoers__ file:

- open terminal
- change __/etc/sudoers__ file
  - `sudo visudo -f /etc/sudoers`
    - __visudo__ for error-checking
    - __-f__ edits /etc/sudoers.tmp and changes the original only if there are no errors

- append at the end of the file:
```cosole
# customizations

"#1000" ALL = NOPASSWD: 
/usr/bin/apt-get update,
/usr/bin/apt-get upgrade,
/usr/bin/apt-get upgrade -y,
/usr/bin/apt full-upgrade,
/usr/bin/apt full-upgrade -y,
/usr/bin/apt dist-upgrade,
/usr/bin/apt dist-upgrade -y,
/usr/bin/apt autoremove,
/usr/bin/apt autoremove -y,
/usr/bin/apt clean,
/usr/bin/apt clean -y

```
  - __#1000__ id of standard user (created on installation process)
  - on __ALL__ host machines
  - __NOPASSWD__ no password needed for following commands
  
- <kbd>ctrl</kbd> + <kbd>x</kbd> exit editor
- <kbd>y</kbd> confirm changes
- <kbd>enter</kbd>       confirm name and check for errors
  
## 2. Update system by typing only one character
  
  create __bash_alias__ file
  
  - open termial
  - go to __HOME Dir__
  ```console
  cd
  ```
  - create __bash_aliases__ file
  ```console
  sudo nano .bash_aliases
  ```
  - create permanent __alias__
  ```console
  alias u="
  echo -n '-> Sync time:' &&
  timedatectl set-ntp 0 &&
  timedatectl set-ntp 1 &&
  echo ' ✓ done' &&
  sleep 1 &&
  echo '-> Updating: ' &&
  sudo apt-get update &&
  echo '-> Full Upgrade:' &&
  sudo apt full-upgrade -y &&
  echo '-> Cleanig Cache:' &&
  sudo apt autoremove -y &&
  sudo apt clean -y &&
  echo ' ' &&
  echo 'System is up-to-date  ✓' &&
  sleep 4 &&
  exit";

  ```
  - exit nano: <kbd>ctrl</kbd> + <kbd>x</kbd>
  - confirm changes: <kbd>y</kbd>
  - confirm name: <kbd>enter</kbd>
  - for testing type:
  ```console
  source ~/.bashrc 
  ```
  - type the following for upgrading system: <kbd>u</kbd> -> <kbd>enter</kbd>
  
## 3. Sync time by typing only one char (e.g. due to wrong time by waking up a debian-based virtual machine)
  
  - open terminal
  - append or create __bash_aliases__ (see above) file
  ```console
  cd;\
  sudo nano .bash_aliases
  ```
  - initiate time synchronization and exit terminal via __"t"__
  ```console
  alias t="
  timedatectl set-ntp 0 &&
  timedatectl set-ntp 1 &&
  echo ' ' &&
  echo 'time is up-to-date ✓' &&
  sleep 4 &&
  exit";
  ```
- exit editor: <kbd>ctrl</kbd> + <kbd>x</kbd>
- confirm changes: <kbd>y</kbd>
- confirm name: <kbd>enter</kbd>
- open new termial for testing: <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>n</kbd>
- type the following for sync time of system: <kbd>t</kbd> -> <kbd>enter</kbd>

## 4. Changing hostname before executing program via __"h"__

- open terminal
- append or create __bash_aliases__ (see above) file
  ```console
  cd;\
  sudo nano .bash_aliases
  ```
- initiate timesync and change hostname to a random value before executing specific program
  ```console
  alias h="
  echo -n '-> Sync time:' &&
  timedatectl set-ntp 0 &&
  timedatectl set-ntp 1 &&
  echo ' ✓ done' &&
  sleep 1 &&
  echo -n 'Changning hostname:'&&
  hostnamectl set-hostname host$RANDOM &&
  echo ' ✓ done' &&
  sleep 1 &&
  (/usr/bin/XXXXXXX &)";

  ```
  - where __XXXXXX__ is name of program
  
- exit editor: <kbd>ctrl</kbd> + <kbd>x</kbd>
- confirm changes: <kbd>y</kbd>
- confirm name: <kbd>enter</kbd>
- open new termial for testing: <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>n</kbd>
- type the following for sync time of system and start specific programm: <kbd>h</kbd> -> <kbd>enter</kbd>

## 5. Turn off automatic screen lock and screensaver

- open terminal and type:
```console
gsettings set org.gnome.desktop.session idle-delay 0 &&\
gsettings set org.gnome.desktop.screensaver lock-delay 0
```

