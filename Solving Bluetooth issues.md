# Troubleshooting Bluetooth Issues
If you're having bluetooth issues, try the following (may not work with every chipset). Tested on various Ubuntu-based distros

## Quick fix
Try the below quick fix
1. Remove `btusb` and `btintel` modules 
   ```
    sudo rmmod btusb btintel
   ```

2. Reload the 2 modules
   ```
    sudo modprobe btusb btintel
   ```
3. Restart the bluetooth service
   ```
    sudo service bluetooth restart
   ```

## Another alternative
Copy and paste the following script in the terminal:

```
#!/bin/bash
echo "fixing BT"
## Hard Refresh
## End Service (If it is running)
sudo systemctl stop bluetooth.service
## Removes Hardware Emulation
sudo systemctl unmask bluetooth.service
## Start Service
sudo systemctl start bluetooth.service
sudo systemctl enable bluetooth
## Re-Enable Hardware Emulation
sudo systemctl mask bluetooth.service
sudo rmmod btusb
sudo modprobe btusb
## Unblock from rfkill
rfkill unblock all 
```

###### *Source: [Stack Exchange - Bluetooth stopped working](https://askubuntu.com/questions/1273266/bluetooth-suddenly-stopped-working-ubuntu-20-04-no-default-controller-availabl)*