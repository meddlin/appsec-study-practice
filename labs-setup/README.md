# Labs Setup

Collection of tips, links, scripts to get a basic "lab" setup for AppSec research. The
term "lab" is being used loosely here. The first version of this document is intended
to make the most use of consumer hardware (no off-lease server stuff yet), to make 
this most approachable to newcomers.

## Host Machine

Here are the specs I'm using. Any x86 PC with comparable hardware should work just fine.

Desktop PC

- AMD CPU
- 16GB RAM
- 500GB NVME

## Virtualization/Hyper-visor

Windoows Hyper-V

### Bridge Network Switch (Hyper-V)

This is necessary to communicate with any VMs from outside the Hyper-V host machine.

- [https://www.how2shout.com/how-to/how-to-create-bridge-network-on-hyper-v-windows-10-step-by-step.html](https://www.how2shout.com/how-to/how-to-create-bridge-network-on-hyper-v-windows-10-step-by-step.html)



## Server Administration (Ubuntu)

### Install Docker

Docker docs: -> 

Install Docker from a script

As always, ***you should read a script before executing it on your machine!***

```bash
> curl -fsSL get.docker.com -o get-docker.sh
> sudo sh get-docker.sh
```

- [https://subscription.packtpub.com/book/cloud-and-networking/9781788626866/1/ch01lvl1sec06/installing-docker-on-linux-with-an-automated-script](https://subscription.packtpub.com/book/cloud-and-networking/9781788626866/1/ch01lvl1sec06/installing-docker-on-linux-with-an-automated-script)

### Setting environment variables

There are multiple ways of doing this. We want something this is: (1) system-wide, 
(2) permanent. We don't want to deal with a shell reloading, or needing a reboot, 
and losing our environment variables.

- Setting environment variables
  - [https://unix.stackexchange.com/questions/117467/how-to-permanently-set-environmental-variables](https://unix.stackexchange.com/questions/117467/how-to-permanently-set-environmental-variables)

- Reload after setting `/etc/environment`
  - Log off/on again after setting environment variables. The PAM runs on logon which will reload `/etc/environment`, thus reloading environment variables.
  - [https://superuser.com/questions/339617/how-to-reload-etc-environment-without-rebooting](https://superuser.com/questions/339617/how-to-reload-etc-environment-without-rebooting)
  