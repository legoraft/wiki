# Stow

GNU Stow is a way of managing a lot of symlinks in a single directory. I use `stow` to manage my dotfiles, as the symlinks allow you to only publish certain parts of a directory to a version control system.

## Usage

To use stow, you need to create a directory in your home directory with `mkdir`. You can copy over your config files to that directory and remove the original files. You can also just use the `mv` command. After doing this, you can just run `stow .` in your stow directory and all the files get symlinked to their respective folders.

After creating all the symlinks, check if the symlinks work correctly by running `ls -l` on your original directory. The output should look something like the following:

```
-rwxr-xr-x 1 foo staff  642 Nov 22  2010 executable.sh
lrwxr-xr-x 1 foo staff   36 Aug 29 15:29 example -> ../.config/path/example
```

This doesn't have to be exactly the same, as long as you see the arrow on the files you've symlinked. You can add new links at any point by just moving the folders to your stow directory and running `stow .`.

When all the files are created and stored you can edit both the files in the stow folder and the files in their original location. The changes will synchronize, enabling you to change configuration from and IDE or other text editor.