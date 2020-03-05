# GameSrv-linux BBS Door Game Server

GameSrv-linux is derived from [Rick Parrish's GameSrv](https://github.com/rickparrish/GameSrv). This will allow you to run classic BBS Door Games in Ubuntu 18.04 with a front-end that listens on multiple ports for incoming connections. Please refer to the original GameSrv repository for more details.

This, essentially, includes a couple of small fixes to get things working specifically for modern Ubuntu. The old build had problems with dependencies on deprecated mono libraries.

## Installation

Clone the repo somewhere

```bash
git clone https://github.com/ryanfantus/GameSrv-linux
```

Become root

```bash
sudo su
```

Create the hardcoded (sorry) installation and runtime directory. Change into that directory and unarchive the zip file from this repo

```bash
mkdir /gamesrv
cd /gamesrv
unzip /path/to/cloned/directory/GameSrv-linux.zip
```

Make sure install script is executable and run it

```bash
chmod +x install.sh
./install.sh
```

## Configuration

Look in the config directory and modify the port values in gamesrv.ini to make sure you're binding to non-privileged ports. These ports will be >1024. If you'd rather bind to lower ports, use something like setcap:

```bash
setcap `cap_net_bind_service=+eip` /usr/bin/mono
```

Note that this method is untested in this use case and YMMV. It's also scary-ish from a security perspective.

## Usage

As root (via su or sudo) run the script start.sh. Bury this in a screen or tmux session if you prefer backgrounding it.
