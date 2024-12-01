# Wipe claen your hard drive using the Shrid tool
Use the Shred tool to erase a hard drive by running this command.

> ### 🛑 *Stop and read the warning*
> ### ⚠️ *Warning: This will wipe clean the selective drive*
> ### *Please take every precaution to ensure you're wiping the correct drive*

1. Run `lsblk` to find the drive name of the drive you would like to wipe clean. It will usually be in the form `sdX` such as `sda`, `sdb`, etc.
2. Use the command `sudo shred -vfz /dev/[your-drive-name]` to start the shredding process (for example, if its `sdc`, you would call `sudo shred -vfz /dev/sdc`).
3. This process will take a long time. It is best to let it run overnight. 
4. This specific instance of the terminal will not be able to accept inputs until the process is complete.

## Notes on options used:
- `v` : verbose mode - shows the progress while shredding
- `f` : force mode - changes file permissions if necessary to allow writing
- `z` : adds a final pass with zeros to hide the shredding




