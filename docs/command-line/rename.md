# Rename

Rename is a commandline tool that let's you rename files in bulk. It isn't installed by default on most distributions, so you'll need to install the `rename` package for your distro.

## Replace string

It's syntax utilizes regex, which is quite easy to find out with [regex101](https://regex101.com/). To get simple find and replace functionality, you can use this command:

```bash
rename 's/foo/bar/g' *.txt
```

This command has a certain syntax after the `rename` command, which I'll break down:

- `s` indicates that you're substituting
- `foo` can be replaced by any string you'd want to search for
- `bar` is the string that replaces `foo`
- `g` indicates that it won't stop after the first hit.
- `*.txt` can be replaced by any filename or extension to filter the replacements.

## Replace characters

Rename also has another mode with which you can replace characters or a string of characters. The syntax for this is as follows:

```bash
rename 'y/abc/xyz/g' *.txt
```

In this, the `y` indicates that you want to translate character for character. In this example, every "a" will be replaced by an "x", every "b" for a "y" and so on.
