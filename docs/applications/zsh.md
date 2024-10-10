# ZSH

Zsh is a shell that's used by default on MacOS and my preferred shell on Linux. This documentation gives some extra information on configuring zsh.

## .zshrc

The main configuration file of zsh is within the `.zshrc`. This file is mostly located within the home directory. Most of this file works in the same way like a `.bashrc` works, it just runs commands at startup of a new session. With this, you can create aliases, change your `$PATH` and run a neofetch on startup.

You can easily define an alias using `alias ..="cd .."`. You can also change your prompt, by changing the `PROMPT` variable like this: `PROMPT="%2~ > "` This uses a lot of different variables, which you can view [here](https://www.tweaking4all.com/software/macosx-software/customize-zsh-prompt/#DynamicPromptElements).