# Void Linux

Void linux is an independent distribution, which uses the `runit` init system and the `xbps` package manager. It's a rolling release, allowing you to have the most recent packages. I try to document all the information on void linux here in a clean and clear manner.

### XBPS

The xbps package manager is the native package manager in Void Linux. It allows you to install, query and remove packages.

#### Installing

To install packages, you use the `xbps-install <package>` command. You can append multiple packages, by separating them by a space. This means that installing `gimp` and `firefox` can be done with the following:

```bash
xbps-install gimp firefox
```

#### Updating

The update command is really simple, you just use the `xbps-install` command with a few flags. The full command looks like this:

```bash
xbps-install -Su
```

The `S` flag synchronizes the remote repositories, where the `u` flag updates all installed packages to the greatest version in the repositories.

#### Removing

Removing packages can be done with the `xbps-remove <package>` command. To also remove the dependencies that aren't used by other packages, use the `R` flag. To remove orphan dependencies, you can use the `o` flag. The full remove command would look like this:

```bash
xbps-remove -Ro
```

## Runit

Runit is the init system void linux uses. You can use it to run certain applications as daemons in the background. It has the same functionality as systemd, but it's a lot smaller and faster.

#### Enabling a service

#### Starting, stopping and status

You can start and stop services and get their status with the `sv` command. This can be done by running `sv start/restart/stop/status <service>`. Where service can be the full path, like `/var/service/<service>` or the service name, like `dbus`.

If you want to check the status of all services currently you can use the following command:

```bash
sv status /var/service/*
```