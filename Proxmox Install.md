# Proxmox
Install proxmox on laptop with this link :
https://www.domo-blog.fr/creer-serveur-virtualisation-proxmox-installer-home-assistant-simplement/

Here you can find the summary of the different commands that are in the link above

## Stop enterprise mode :
```
rm /etc/apt/sources.list.d/pve-enterprise.list
echo '# Proxmox community package repository' >> /etc/apt/sources.list
echo 'deb http://download.proxmox.com/debian/pve bullseye pve-no-subscription' >> /etc/apt/sources.list
```

## Update and upgrade 'Linux' dependencies

```
sudo -i
apt-get update && apt-get upgrade -y && apt-get autoclean
```

- Linux Interface Network Manager (Free software: GNU General Public License v2)

```
apt-get install ifupdown2
```

- 'Bridge Manager' ( https://wiki.hutit.fr/capharnaum/openvswitch )

```
apt-get install openvswitch-switch -y
 ```

## Power save and stop stanby
With a laptop the closing of cover causes standby and if the cover stay open the sreen consumes energy
- Turn off screen display after XX seconds

``` 
# edit grub file with nano
nano /etc/default/grub
# modify grub file GRUB_CMDLINE_LINUX=”” by
GRUB_CMDLINE_LINUX="consoleblank=XX"
# Ctrl+O to save and Ctrl+X to exit editor file
# update grud file
update-grub
```

- Stop the stanby with the cover closing (edit the logind.conf)

``` 
# edit logind.conf file with nano
nano /etc/systemd/logind.conf
# modify 2 lines in the file 
HandleLidSwitch=ignore
HandleLidSwitchDocked=ignore
# Ctrl+O to save and Ctrl+X to exit editor file
# update config
systemctl restart systemd-logind.service
```

## Update hypervisor Proxmox

```
pveupgrade
```

And to finish you can reboot your system 
```
sudo reboot
```
