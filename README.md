# Raupycore

This repository helps you to setup up [AshamaneCore (legion = 7.3.5.26972)](https://github.com/AshamaneProject/AshamaneCore/tree/legion).
It automates most steps that are described in [Trinitycore Wiki](https://www.trinitycore.info).
Look at that guide for details.

This setup is mostly inspired by [Azerothcore](https://www.azerothcore.org), which makes setting up version 3.3.5a very easy.

We do not make any source code changes, provide fixes or database updates.
That is why we call this project "Raupycore" (Yes, we replaced the normal ASCII banner with "RAUPYCORE").
A non epic name for a non epic setup project.

## Requirements

### General

* Client (enUS) with the version (7.3.5.26972)
* `git`
* `docker`

### Windows

You need to install Docker For Windows or install a Linux distribution in a Virutal Maschine (VM).

1. [Install Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install)
1. [How to run an Ubuntu Desktop virtual machine using VirtualBox 7](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview)

*Hint*: Using Docker under Windows is not a smooth experience (keyword:
vmmem.exe high memory usage), at least it was in our case, we recommand using a
VM. If you use a VM you should forward the following ports to your Host:

TODO: There is a problem: How to get the game files into the VM, without copying them? Use a shared folder?

- TODO
- TODO
- TODO
- TODO
- TODO
- TODO

### Linux

Arch linux based distributions:

* Install `docker` with `pacman -S docker docker-compose`.
* And starting it with `sudo systemctl start docker`.

## Setup

Open the `.env` file and add the path to your client folder, otherwise the first `docker compose` command will fail.

```sh
$ git clone http://TODO/TODO/raupycore
$ cd raupycore                     # Do not change the directory name, otherwise "raupycore" in the last command must be changed to the new name!
$ docker compose up                # The first time:
                                   # - it will build the core (depending on your computer, this will take around 20 minutes),
                                   # - it will extract all game files (this will take over 1 hour) and
                                   # - populate the database (this will take around 2 minutes)
$ # After awhile the prompt `TC>` will show up in the output of the worldserver.
$ # Then execute the following command and enter the following two lines after `TC> `.
$ docker attach raupycore-worldserver-1
TC> bnetaccount create admin@admin admin
TC> account set gmlevel 1#1 3 -1
```

If a steps fails you can execute `git clean -fdx` and try again.

Now start your client and login with `admin@admin` with password `admin`.
