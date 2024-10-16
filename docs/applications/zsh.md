# ZSH

Zsh is a shell that's used by default on MacOS and my preferred shell on Linux. This documentation gives some extra information on configuring zsh.

## .zshrc

The main configuration file of zsh is within the `.zshrc`. This file is mostly located within the home directory. Most of this file works in the same way like a `.bashrc` works, it just runs commands at startup of a new session. With this, you can create aliases, change your `$PATH` and run a neofetch on startup.

You can easily define an alias using `alias ..="cd .."`. You can also change your prompt, by changing the `PROMPT` variable like this: `PROMPT="%2~ > "` This uses a lot of different variables, which you can view [here](https://www.tweaking4all.com/software/macosx-software/customize-zsh-prompt/#DynamicPromptElements).

## Plugin manager

You can install a lot of plugins in zsh. You can manage these plugins with a plugin manager. My preferred one is [sheldon](https://github.com/rossmacarthur/sheldon). It's easy to set up and uses a simple `.toml` file to configure everything. For example, to set up the autosuggestions you use the following syntax:

```zsh
[plugins.autosuggestions]
github = "zsh-users/zsh-autosuggestions"
```

You can enter any github repo in this, using the user and repo name. This allows you to install a lot of plugins to customize the prompt, add suggestions, autocompletion etc.

## Suggestions

Zsh has a great [suggestion](https://github.com/zsh-users/zsh-autosuggestions) system. It shows the suggestions a bit darker than the foreground and allows you to autocomplete. You can install this through a [plugin manager](#plugin-manager).