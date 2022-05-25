# DigiNode Tools

## Install and monitor your own DigiByte & DigiAssets Node

These tools have been designed to make it as easy as possible to setup and monitor your own DigiNode on your Linux hardware of choice. 

The recommended setup for this is a **Raspberry Pi 4 8Gb** running **Raspberry Pi OS Lite 64-bit**.

For more information, visit: https://diginode.digibyte.help

## Disclaimer

These tools are provided as is. Use at your own risk. Make sure you always have a backup of your wallet file. 

WARNING: This script is still under development and should only be used for testing purposes at this time.


## DigiNode Setup

Script to help you setup and manage your DigiNode - installs and configures a DigiByte Node and DigiAsset Node. It will also upgrade an existing install with any updates.

- Intuitively walks you though the process of installing a DigiByte Node and DigiAsset Node.
- Almost no linux experience required. It does all the work for you. It's as plug-and-play as possible.
- Automatically checks hardware and OS at launch - it lets you know if your system is compatible.
- Detects compatible Raspberry Pi hardware (if present).
- Creates a swap file on low memory devices, and checks if any existing swap file is large enough.
- Installs or upgrades DigiByte and DigiAssets Node software with the latest releases from GitHub.
- Creates or updates a digibyte.conf settings file with optimal settings.
- Creates digibyted.service file to keep the DigiByte Node running 24/7.
- Creates or updates an DigiAsset config file with RPC settings. 
- Optionally, creates a 'digibyte' user and sets system hostname to 'diginode'.
- Enables zeroconf networking (Bonjour) so you can access your node at http://diginode.local - i.e. no need to remember the IP address.


## DigiNode Status Monitor

Let's you monitor your DigiNode from the terminal.

- Monitor your DigiNode on your local machine via the terminal. I also works remotely over SSH.
- Displays live DigiByte and DigiAsset data including:
    + Connection Count
    + Block Height (with Sync Progress)
    + IP addresses (local and external)
    + Web UI address 
    + Node uptime
    + Disk, RAM and swap usage
- Periodically checks for software updates (not more than once every 24 hours) and helps you install them.


## Additional Features

Once your DigiNode has been installed, you can access additional features from the DigiNode Setup menu by entering: ```diginode-setup```

- Backup/Restore: This will help you to backup your DigiByte wallet and/or your DigiAsset Node settings to an external USB stick. It is advisable to choose a USB stick that you do not use for anything else, and to store it somewhere secure when you are done. The blockchain and/or digiasset data will not be backed up. Find this in the 'DigiNode Setup' menu.


## Instructions

- To get started, run DigiNode Setup by entering the following command in the terminal:

# curl -sSL diginode-setup.digibyte.help | bash


## Advanced Users Only

These features are for advanced users and should be used with caution:

- Unattended Mode

This is useful for installing the script completely unattended. Run this only having customized the unattended install settings in the ~/.digibyte/diginode.settings file. The settings file will be created the first time you run DigiNode Setup. To run in unattended mode, use the --unattended flag at launch.

Example: 
```curl -sSL diginode-setup.digibyte.help | bash -s -- --unattended```

- Reset Mode

This will reset and reinstall your current installation using the default settings. It will delete digibyte.conf, diginode.settings and main.json and recreate them with default settings. It will also reinstall DigiByte Core and the DigiAsset Node. IPFS will not be re-installed. Do not run this with a custom install or it may break things. For best results, run a standard upgrade first, to ensure all software is up to date, before running a reset. Software can only be re-installed if it is most recent version. You can perform a Reset via the DigiNode Setup main menu by entering ```diginode-setup```. You can also use the --reset flag at launch.

Example:
```curl -sSL diginode-setup.digibyte.help | bash -s -- --reset``` or
```diginode-setup --reset```

- Skip OS Check

The --skiposcheck flag will skip the OS check at startup in case you are having problems with your system. Proceed with caution.

Example: 
```curl -sSL diginode-setup.digibyte.help | bash -s -- --skiposcheck```

- Uninstall

The --uninstall flasg will uninstall your DigiNode. Your DigiByte wallet will be kept. This can also be accessed from the main menu.

Example: 
```curl -sSL diginode-setup.digibyte.help | bash -s -- --uninstall``` or
```diginode-setup --uninstall```

- Verbose Mode

This provides much more detailed feedback on what the scripts are doing - useful for troubleshooting and debugging. Set variable at top of either script. This can be overwridden using the --verboseon or --verboseoff flags.

Example: 
```curl -sSL diginode-setup.digibyte.help | bash -s -- --verboseon```

## Compatibility

- A device with at least 8Gb RAM is strongly recommended. DigiNode requires >5Gb to run. 4Gb RAM will work with a SWAP file but performance will suffer considerably. Fine for testing, not recommended for long term use. Less than 4Gb RAM is not recommended. (DigiByte Core's memory requirements exceed that of Bitcoin due to multi-algo.) 
- When using a Raspberry Pi, booting from an SSD is highly recommended. Using a microSD is inadvisable.
- A 64bit Linux OS is required - the latest Ubuntu Server LTS version is recommened.

DigiNode has been tested and known to work with the following systems:

| **Hardware**          | **Operating System**             | **Notes**                                                                                                   |
|-----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------|
| Raspberry Pi 4 8Gb    | Ubuntu Server 22.04 LTS          | This is the recommended configuration. Booting from an SSD, rather than microSD, is highly recommended.     |
| Raspberry Pi 4 8Gb    | Raspberry Pi OS 64-bit           | This is the recommended configuration. Booting from an SSD, rather than microSD, is highly recommended.     |
| Raspberry Pi 4 4Gb    | Ubuntu Server 22.04 LTS          | Requires swap file. Runs slowly.                                                                            |
|                       |                                  |                                                                                                             |


## Release History

v0.0.6 - 2022-05-xx Test Release
- Reboot is no longer required after first install
- diginode.settings variables now get reset during an uninstall

v0.0.5 - 2022-05-19 Test Release
- USB Backup feature now backs up DigiAsset settings as well as DigiByte Wallet
- DigiAsset Settings are backed up locally when uninstalling, if desired. This fixes the bux in v0.0.4
- Fixes to diginode.settings to better store variables
- Any changes made to the RPC credentials (user/password/port) are now updated in the DigiAssets main.json file during an Update
- Countless bug fixes and improvements

v0.0.4 - 2022-05-10 Test Release
- Fixed several bugs relating to the Status Monitor being able to check for software updates
- Install URL has changed to diginode-setup.digibyte.help
- Implemented backup feature for prelimanry testing
- Renamed every mention of "DigiNode Installer to "DigiNode Setup"
- WARNING: There is currently a bug with the DigiAsset Node updater that will erase you configuration. I  am currently working to fix this.

v0.0.2 - 2021-11-14
- Test Release