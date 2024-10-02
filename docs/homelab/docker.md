# Docker

Docker is containerization software that's widely used within self-hosting nowadays. You can easily run full stacks with `docker-compose` and with scripting launch a lot of self-hosted apps.

## Installation

This installation is for Debian installations. It uses the docker repository to easily download `docker` and `docker-compose`. Start by updating the system and installing the `ca-certificates` and `curl` packages.

```
sudo apt install ca-certificates curl
```

Next, install the keyrings with the following commands:

```
sudo install -m 0755 -d /etc/apt/keyrings
```

Download the gpg keys, next:

```
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
```

Next, ensure that every user can read the gpg key:

```
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Next, add the repository to the apt `sources.list`.

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Lastly, run `apt update` to update the new repository and install the correct docker packages. This can be done with the following command:

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

You also download the `docker-compose-plugin` with this, so you can immediately use your docker compose files. If you want to make the setup more secure, ensure your non-privileged user is part of the `docker` group. This can be done with the following command:

```
sudo usermod -aG docker <user>
```