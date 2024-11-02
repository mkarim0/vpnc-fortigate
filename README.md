# VPNC Fortisgate

`vpnc` patched to work with Fortisgate.

The revision hosted in this repository is `550`. The latest version can be found at http://svn.unix-ag.uni-kl.de/vpnc/trunk/.

Patch is [here](https://github.com/hekar/vpnc-fortisgate/commit/36f53e3374fbe7dc0d8562cf186cde6974688b18). Patch was original taken from [Fortigate Ipsec Linux Networkmanager](http://www.justdailynotes.com/fortinet/linux/vpn/2015/02/14/Fortigate-IPSec-Linux-NetworkManager/)

## Quick Install

__Please read the source before blindly executing a shell script: [quick-setup.sh](./quick-setup.sh).__

```
sh -c "$(curl -fsSL https://raw.github.com/hekar/vpnc-fortisgate/master/setup.sh)"
```


### Fedora

#### Dependencies
```
sudo dnf install -y libgcrypt-devel gnutls-devel
```

### Ubuntu

#### Dependencies
```
sudo apt install  libgcrypt20-dev libgnutls28-dev python-is-python3
```

## Manual Setup

```
git@github.com:hekar/vpnc-fortisgate.git
cd vpnc-fortisgate/vpnc
make
```

Optionally it can also be installed. This is not recommended, as it will overwrite the vpnc client provided by your distribution and may not connect to other vpn providers. It is recommended that you save this patched version in `/opt` or elsewhere.

```
sudo make install
```

## Run

If installed, you run this in the same manner you would run the standard `vpnc` (usually through NetworkManager.)

Not being a fan of NetworkManager, I prefer to run `vpnc` from the shell.

1) Create a configuration file and save it in your home directory "~/.vpnc-default":
```
IPSec gateway my.vpn.gateway
IPSec ID my.ipsec.id
IPSec secret mysecret
```

2) Start vpnc with the correct configuration file
```
sudo ./vpnc/vpnc ~/.vpnc-default
```

3) Disconnect using `sudo ./vpnc/vpnc-disconnect` or `kill -9 <PID>`

4) Add to $PATH

## Notes
In case of this error 
```
vpnc: quick mode response rejected:  (ISAKMP_N_INVALID_MESSAGE_ID)(9)
```
It means that there is a mismatch between client configuration and server configuration, for example PFS can be disabled on client but enabled on the server, and vice versa
Or mismatched DH groups

## Credit

[Tulio Munhoz - JustDailyNotes](http://www.justdailynotes.com/fortinet/linux/vpn/2015/02/14/Fortigate-IPSec-Linux-NetworkManager/) for the patch.
