# Using CLI Tools in Flatpaks

Flatpaks generally load with minimal environmental variables, and this means custom additions such as runtimes/etc are not loaded from your `.bashrc` or other settings files. Use the following steps to add custom instructions

## General Guide
1. Install Flatseal if your system does not have it installed. It will provide GUI access to these settings
2. Instead of loading the .bashrc file directly (which you can do if you'd like it easy), we will create a separate dotfile in the `Home` folder(as an example, `.runtimepaths`) to only load the runtimes / variables we want.
3. Create / open the file in the terminal via `nano .runtimepaths`
    ```
    $ nano .runtimepaths
    ```
4. Add the required settings, for example:
    ```
    # Cargo
    . "$HOME/.cargo/env"

    # Add path for manual go location
    if [ -d "$HOME/.go/bin" ]; then
        export PATH="$HOME/.go/bin:$PATH"
    fi
    ```
5. Save the file using `Ctrl` + `O` and exit using `Ctrl` + `X`.
6. Open Flatseal and navigate to app
7. Under `Variables`, add Bash env for example `BASH_ENV=/home/user/.runtimepaths`
8. Close and start back your app

## Using Github's `gh` in Flatpaks
1. Install and authenticate gh in your main terminal
2. Once this is done, you can use `git` commands normally in the flatpak app (including cloning from, and pushing to, private repositories)
3. You may be prompted to set git username / email on first use
