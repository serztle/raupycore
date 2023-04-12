# Raupycore

This repository helps you to setup up [AshamaneCore (legion = 7.3.5.26972)](https://github.com/AshamaneProject/AshamaneCore/tree/legion).
It automates nearly all steps that are described in [Trinitycore Wiki](https://www.trinitycore.info/).
Look at that guide for details.

This setup is mostly inspired by [Azerothcore](https://www.azerothcore.org), which makes setting up version 3.3.5a of the game version very easy.

We do not make any source code changes, provide fixes or database updates.
That is why we call this project "Raupycore" (Yes, we replaced the normal ASCII banner with "RAUPYCORE").
A non epic name for a non epic setup project.

## Requirements

### General

* Client with the version (7.3.5.26972)
* `git`

### Windows

You need to install Docker For Windows or install a Linux distribution in a Virutal Maschine (VM).

1. [Install Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install)
1. [How to run an Ubuntu Desktop virtual machine using VirtualBox 7](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview)

*Hint*: Using Docker under Windows is not a smooth experience (keyword:
vmmem.exe high memory usage), at least it was in our case, we recommand using a
VM. If you use a VM you should forward the following ports to your Host:

- TODO
- TODO
- TODO
- TODO
- TODO
- TODO

### Linux

Arch linux based distributions:

* Install `docker` with `pacman -S docker docker-compose`.
* Start with `systemctl start docker`.

## Setup

Open the `.env` file and add the path to your client folder, otherwise the first `docker compose` command will fail.

```sh
$ git clone http://TODO/TODO/raupycore
$ cd raupycore
$ docker compose build worldserver # Depending on your computer, this will take around 20 minutes
$ docker compose up extract        # This will take over 1 hour
$ docker compose up                # The first time, this will take around 10 minutes
```

Follow the instruction under
[https://www.trinitycore.info/install/Client-Setup](Master). Start your client
and login with user `test@test` and password `test`.
