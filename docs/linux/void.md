# Void Linux

Void linux is an independent distribution, which uses the `runit` init system and the `xbps` package manager. It's a rolling release, allowing you to have the most recent packages. I try to document all the information on void linux here in a clean and clear manner.

### Installation

To install Void Linux, you need to have a valid install medium and boot into the drive. After the boot, you can log in with the username `root` and the password `voidlinux`. The simplest way to start the installation is by using the script. You can start the script by running `void-installer`.

Most of the installer is quite straightforward. There are a few things that are smart to select during install, documented here.

#### Source

In Source, you configure the installation source of the packages. If you want the most up-to-date packages, select network install.

#### Root

It's best to avoid a root user, it isn't that secure and an admin account is enough for administrator rights.

#### Partitioning

The easiest tool for doing the partitioning is `cgdisk`. For UEFI systems, it's best to create a `gpt` partition table. The partitions you should create are as follows:

- An EFI partition with the `EFI System` type. This partition should be between 200MB and 1GB.
- If you have low RAM, you can also add a swap partition. Refer to the table to select your swap amount. This partition can be `Linux Filesystem`.
- For the rest of the filesystem, you should partition the rest of the available space. This partition also should have the `Linux Filesystem` type.

| RAM   | Swap amount  |
| ----- | ------------ |
| < 2GB | 2x RAM       |
| 2-8GB | Same as RAM  |
| 8GB+  | At least 4GB |

#### Mounting

Mounting the partitions is also something that should be done in the correct way. Your EFI partition should have the `vfat` filesystem and be mounted at `/boot/efi`. The swap partition should have the `swap` filesystem, which is enough. The general file system should have the `ext4` filesystem and be mounted at `/`.

## XBPS

The xbps package manager is the native package manager in Void Linux. It allows you to install, query and remove packages.

#### Installing

To install packages, you use the `xbps-install <package>` command. You can append multiple packages, by separating them by a space. This means that installing `gimp` and `firefox` can be done with the following:

```
# xbps-install gimp firefox
```

#### Updating

The update command is really simple, you just use the `xbps-install` command with a few flags. The full command looks like this:

```
# xbps-install -Su
```

The `S` flag synchronizes the remote repositories, where the `u` flag updates all installed packages to the greatest version in the repositories.

#### Removing

Removing packages can be done with the `xbps-remove <package>` command. To also remove the dependencies that aren't used by other packages, use the `R` flag. To remove orphan dependencies, you can use the `o` flag. The full remove command would look like this:

```
# xbps-remove -Ro
```

## Runit

Runit is the init system void linux uses. You can use it to run certain applications as daemons in the background. It has the same functionality as systemd, but it's a lot smaller and faster.

#### Enabling and disabling

All daemons for services you've downloaded, are stored in `/etc/sv/<service>`. To enable a service, you create a symbolic link between this directory and `/var/service`. This can be done with the following command:

```
# ln -s /etc/sv/<service> /var/service/
```

To disable the service, you just have to remove the link. This can be done with the `rm` command.

```
# rm /var/service/<service>
```

#### Starting, stopping and status

You can start and stop services and get their status with the `sv` command. This can be done by running `sv start/restart/stop/status <service>`. Where service can be the full path, like `/var/service/<service>` or the service name, like `dbus`.

If you want to check the status of all services currently you can use the following command:

```
# sv status /var/service/*
```