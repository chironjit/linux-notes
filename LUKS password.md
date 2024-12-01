## Adding, changing & Removing LUKS(crypdata) passwords
The following are steps to add and remove passwords when you have full disk encryption on. You can have up to 8 passwords for your LUKS encryption at one time. These have been tested in Ubuntu distros.

## Add password

1. Run `lsblk` in your terminal to get your partitions. You should see something like this:
   ```
    zram0               16G     0 disk  [SWAP]
    nvme0n1             1.8T    0 disk  
    ├─nvme0n1p1         1022M   0 part  /boot/efi
    ├─nvme0n1p2         4G      0 part  /recovery
    └─nvme0n1p3         1.8T    0 part  
    └─cryptdata         1.8T    0 crypt 
        ├─data-root     1.7T    0 lvm   /
        └─data-swap     64G     0 lvm   [SWAP]

   ```

2. Add a password using `sudo cryptsetup luksAddKey /dev/[your-partition-name]`. In the example above, run `sudo cryptsetup luksAddKey /dev/nvme0n1p3`
   
3. Follow the steps, usually it will ask for your current LUKS password, then ask you for your new LUKS password, and then confirm the new LUKS password.
   
4. You can check how many passwords you have via `sudo cryptsetup luksDump /dev/nvme0n1p3`

## Removing passwords
1. Check how many keys you have via `sudo cryptsetup luksDump /dev/[your-partition-name]`. You will see a numbered list of available hashes
   
2. Enter `sudo cryptsetup luksRemoveKey /dev/[your-partition-name]`. You will be asked to enter the passphrase to be deleted.
   
3. Once passphrase entered, it will be deleted.

## Adding passwords when switching keyboard layouts
Assuming your device has LUKS with a US keyboard, but you are using a new keyboard layout. Add the password in the new layout via:

1. Ensure you have the US and new keyboard layout. Start with the new keyboard layout here.
   
2. Run `lsblk` in your terminal to get your partitions. Using the example in **Adding password**, we would see that the LUKS is on `nvme0n1p3`.
   
3. Run `sudo cryptsetup luksAddKey /dev/nvme0n1p3`. Enter a current LUKS password when prompted.
   
4. When prompted for the new password, first switch your keyboard layout settings to US.
   
5. Now enter the new password, but using the keys of your new layout. For clarity:
   
   > Assume you are now adding the password `comik` in Dvorak layout.
   >
   > You would be typing `comik` in the Dvorak layout, but the actual password entered will be `ismgv`.

6. Now when you need to enter the LUKS password on start, you can type the password using the new layout(though the actual input is still US)


###### *Steps not given for changing the actual language, because more likely than not, you may need (or go back to using) the original layout*

   