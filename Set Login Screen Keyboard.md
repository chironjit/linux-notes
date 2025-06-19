# Set Login Screen Keyboard
Set a diffefent keyboard layout for login

## Steps
1. Check current status for keyboard using `localectl status` in youf terminal. You will get this:
```
System Locale: LANG=en_AU.UTF-8
    VC Keymap: us-colemak
   X11 Layout: us
    X11 Model: microsoftpro
  X11 Variant: colemak
  X11 Options: terminate:ctrl_alt_bksp
```
2. Login page layout is under `VC`
3. Get your layout using `localectl list-keymaps`. Scroll through the options by pressing `Enter`. You can exit the list using the `q` key
4. Set your keymap using `localectl set-keymap <keymap>`, ie, `localectl set-keymap us-colemak`
5. Logout / reboot to implement / test

##### Use `man listectl` to see options

###### Source:
1. Localectl manpage - `man localectl`
2. [Adding keyboard variant](https://www.reddit.com/r/linuxquestions/comments/1drfzbx/adding_a_variant_to_the_english_keyboard_layout/)
3. [Setting keyboard layout - Gnome](https://help.gnome.org/admin/system-admin-guide/stable/keyboard-layout.html.en)



