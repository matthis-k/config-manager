# How it works
## `get-config <path>`
Looks up what files to include in `path/included` and copies it to `path/home` if it is a subdirectory of `$HOME` and to`path/root` otherwise.  

## `deploy-config <path>`
Finds the configuration and first removes all files and directories listed in `path/included` and then copies the directory `path/home` into `$HOME` and `path/root` to your systems root `/`.  
WARNING: Watch out what the configuration puts in here, unless you trust the source.

## `install-needed-packages <path>`
Looks for `path/packages` and installes them with [paru (bin)](https://aur.archlinux.org/packages/paru-bin/). It will automatically install `paru-bin` if it is not installed on the system, feel free to change it to yay or something you prefer by simply replacing `paru` with your packagemanager of choice, change the installation command and removing the installation section for `paru`.  

## `full-install <path>`
 1. executes `$path/prerequisites` if it exists
 2. executes `install-needed-packages $path`
 3. executes `deploy-config $path`
 4. executes `$path/post-configuration` if it exists

# What to put in a config?
In case you want to create your own configuration, you can put the following files in there:  

1. `included`: This contains all directories or files you want to include in your configuration, one on each line. The `~` character will be replaced with your `$HOME` variable.
2. `packages`: This contains all packeges you need for the configuration, one per line. For example a configuration for [i3wm](https://i3wm.org/) would put i3 in here.
3. `prerequisites`: Executable/script with things that need to be done before the configuration is deployed. For example install `base-devel` if you have packages that need it to install.
4. `post-confituration`: Executable/script with things to do after the deployment and the installation of the packages. For example enable system services.

WARNING: Watch out what is in the executables/scripts unless you fully trust the source.
NOTE: `prerequisites` and `post-configuration` is not manditory, it just helps to set your configuration up on a freshly installed system. optimally you just have to execute `full-install` and it works out of the box.

[Here](https://github.com/matthis-k/config/tree/master) you can find my current configuration as an example.
