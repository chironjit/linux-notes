# Setting custom resolution on VMs with Wayland (Wayland Gnome)

## Note
> ### 
> ### Some steps can break the VM(such as incorrect naming, resolution, etc), so use at your own risk
> ### May take several reboots to work
> ### Does not require your monitor to explicitly support / have in EDID to support the resolution but this may break the display
> ### 

## Steps
1. Find the display name using `xrandr` command in the terminal. Result should have a line that goes `Virtual-1 connected primary...`. In this case `Virtual-1` is the display name(case sensitive)
2. Open the Grub settings via `sudo nano /etc/default/grub`
3. Look for the `GRUB_CMDLINE_LINUX_DEFAULT` line. It should look like this (in 24.04):

    ```
    # If you change this file, run 'update-grub' afterwards to update
    # /boot/grub/grub.cfg.
    # For full documentation of the options in this file, see:
    #   info -f grub -n 'Simple configuration'

    GRUB_DEFAULT=0
    GRUB_TIMEOUT_STYLE=hidden
    GRUB_TIMEOUT=0
    GRUB_DISTRIBUTOR=`( . /etc/os-release; echo ${NAME:-Ubuntu} ) 2>/dev/null || echo Ubuntu`
    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
    GRUB_CMDLINE_LINUX=""

    ...
    ...
    ...
    ```

4. Add `video=<Display Name>:<Width>x<Height>@<Refresh Rate>` to the line. In my case, I want to add a non-standard resolution that I know is supported by my screen: `video=Virtual-1:2880x1920@60`
5. The line should now be `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash video=Virtual-1:2880x1920@60"`
6. Save file via `Ctrl + O`(the letter O), then `Enter`. `Ctrl + X` to exit.
7. Update Grub via `sudo update-grub`
8. Reboot




## Alternative for step 1:
If step 1 doesn't work, you may try to run `ls /sys/class/drm` in the terminal
```
~$ ls /sys/class/drm
card1  card1-Virtual-1  renderD128  version
```
You may see an alternative representation of the display name here. You can try this name if the name from step 1 doesn't work



###### Source:
1. [Set custom display resolution on Ubuntu 22.04](https://www.youtube.com/watch?v=dLVHz7rrP8U)
2. [Freedesktop Wayland Documentation](https://wayland.freedesktop.org)