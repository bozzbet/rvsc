# Running Verus Coin Mining on Mobile Phones (Android)
Quick installation of CCminer on Android Phones

## Github cloning and customizing
This is a fork from the OINK70 repository --> https://github.com/Oink70/Android-Mining.  Modifications are made to reflect my own accounts.  
Clone this repository to your own github account and modify as necessary.

Key Changes to be made: (These are taken from OINK70's instructions.)
1. Change the URL's on the README.md to reflect your own account.
2. Replace `QR/mcvim_install.png` with your own.
3. **Important**: Change the SSH key on line 13 of `install.sh` to reflect your own SSH key.
4. Change lines 47 and/or 51 to reflect your own github link.
5. Adjust the `config.json` to your address and mining details. ("user":<verus wallet address>.<custom name>)
6. Optional: Update "api-allow": of your `config.json` to your own LAN IP range.
7. Optional: Update "api-bind": of your `config.json` to the LAN IP your phone uses.

## No Support will be provided

## Prerequisites
- A basic understanding of Linux is required — take an online course if needed.
- You must know how to use Linux screen for session management.
- Familiarity with SSH and SCP is strongly recommended.
- A stable Wi‑Fi or cellular connection is essential for installation and operation. Expect to troubleshoot your own network issues when they arise.

## Installation instructions for Android:
- This method specifically uses TERMUX in Android devices.  Install TERMUX on your mobile phone.
- Install package for Ubuntu Environment.  This is included in the install-termux.sh.
```bash
    pkg install proot-distro
    proot-distro install ubuntu
```
- Log into Ubuntu
```bash
    proot-distro login ubuntu
```

## Verify Architecture is 64-bit:
```bash
lscpu
```
If the output doesn't show `Architecture: aarch64` or `CPU op-mode(s): 32-bit, 64-bit`, then do not bother to continue. Your phone is not running a 64-bit OS.

## Installation
These are the instructions to run to install the miner with shell scripts.

Installer on ARM/non-Android(raspberry):
```bash
curl -o- -k https://raw.githubusercontent.com/bozzbet/rvsc/mcvrsc/install.sh | bash
```
Installer on ARM/Android(mobile phones):
```bash
curl -o- -k https://raw.githubusercontent.com/bozzbet/rvsc/mcvrsc/install-termux.sh | bash
```

For quick access on phones:
![install.sh](QR/mcvim_install.png) (To be updated.....)

After the installation, you need to update the config.json:
Adjust pools, mineraddress+workername, and network settings for the API.
```bash
nano config.json
```
Exit with `<CTRL>-X` followed by `y` and an `<ENTER>`

Sample config.json file:
```bash
{
	"pools":[
	{
		"name": "<pool_name>",
        "url": "stratum+tcp://<pool>:<port>",
		"timeout": 150,
		"disabled": 0
	},
	{
		"name": "<pool_name>",
        "url": "stratum+tcp://<pool>:<port>",
		"timeout": 60,
		"time-limit": 600,
		"disabled": 0
	}],
	"user": "wallet_address.miner_name",
	"algo": "verus",
	"threads": 8,
	"cpu-priority": 1,
	"retry-pause": 5,
	"api-allow": "192.168.0.0/16",
	"api-bind": "0.0.0.0:4068"
}
```

## Usage:
Start the ccminer by running this script `~/vrsc/ccminerd/start.sh`

Starting the miner:
`~/vrsc/ccminerd/start.sh`

Monitoring the miner:
- `screen -x CCminer`
- Exit with `CTRL-a` key combination followed by `d`.

Terminating the miner:
`screen -X -S CCminer quit`

## Monitoring your miners (on a linux host):  
(Follow instructions from OINK70's Github Repo)

Check [MONITORING](/monitoring/MONITORING.md).

WARNING: The scripts installs my own public SSH key. You may want to remove that from your `~/.ssh/authorized_keys` file and replace it with your own for passwordless access.

### I accept no warranties or liabilities on this repo. It is supplied as a service.
### Use at your own risk!!!
