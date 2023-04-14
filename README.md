# Raupycore

This repository helps you to setup up [AshamaneCore (legion = 7.3.5.26972)](https://github.com/AshamaneProject/AshamaneCore/tree/legion).
It automates most steps that are described in [Trinitycore Wiki](https://www.trinitycore.info).
Look at that guide for details.
It is intended for single players who want to have their own world for testing and research.

This setup is mostly inspired by [Azerothcore](https://www.azerothcore.org), which makes setting up version 3.3.5a very easy.

We do not make any source code changes, provide fixes or database updates.
That is why we call this project "Raupycore" (Yes, we replaced the normal ASCII banner with "RAUPYCORE").
A non epic name for a non epic setup project.

## Requirements

### General

* Client (enUS) with the version 7.3.5.26972 *(not provided)*
* `git`
* `docker`

### Windows

You need to install either Docker For Windows or install a Linux distribution in a Virutal Maschine (VM).

* [Install Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install)
* [How to run an Ubuntu Desktop virtual machine using VirtualBox 7](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview)

*Hint*: Using Docker under Windows is not a smooth experience (keyword:
vmmem.exe high memory usage), at least it was in our case, we recommand using a
VM. If you use a VM you should forward the following ports to your Host:

- 1119
- 3443
- 7878
- 8081
- 8082
- 8085
- 8086
- 3306 *(optional)*

TODO: add screenshot from virtualbox
TODO: There is a problem: How to get the game files into the VM, without copying them? Use a shared folder?

### Linux

Arch linux based distributions:

* Install `docker` with `pacman -S docker docker-compose`.
* And starting it with `sudo systemctl start docker`.

## Setup

Copy the file `.env.dist` to `.env`:

```sh
$ cp .env.dist .env
```

And add the path to your client to this line `CLIENT_DIRECTORY=`.
After that execute the following commands:

```sh
$ git clone http://github.com/raupycore/raupycore
$ cd raupycore          # Do not change the directory name, otherwise "raupycore" in the last command must be changed to the new name!
$ docker compose build  # It will build the core (depending on your computer, this will take around 20 minutes)
$ docker compose up     # The first time
                        # - it will extract data from the game (this will take over 1 hour) and
                        # - populate the database (this will take around 2 minutes)
```

After awhile the prompt `TC>` will show up in the output of the worldserver.
Then execute the following command and enter the following two lines after `TC> `.

```sh
$ docker attach raupycore-worldserver-1
TC> bnetaccount create admin@admin admin
TC> account set gmlevel 1#1 3 -1
```

Now start your client and login with `admin@admin` with password `admin`.

If a steps fails you can execute `git clean -fdx` and try again.
