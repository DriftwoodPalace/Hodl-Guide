[ [Intro](README.md) ] -- [ [Preparations](raspibolt_10_preparations.md) ] -- [ **The First Keys** ] -- [ [Lightning](raspibolt_40_lnd.md) ] -- [ [Mainnet](raspibolt_50_mainnet.md) ] -- [ [Bonus](raspibolt_60_bonus.md) ] -- [ [Troubleshooting](raspibolt_70_troubleshooting.md) ]

---

# Generate the last key with Tails

We are generating the last key with Electrum on a computer booted with Tails, https://tails.boum.org/. Tails is a live operating system that´s built upon Debian (a Unix-like operating system). 
It´s booted from a USB-stick and only uses the computers RAM-memory which means that all sensitive information is erased when the USB is ejected (and your computer will start with your usual operating system like nothing happened). 

### Install Tails
Go to https://tails.boum.org/install/index.en.html and choose your operating system. If you don´t have an old copy of Tails, select “Install from {Your operating system}”. 
Select “Let´s go” and download the USB image at step 1.1 to a directory on your computer. At the download page, make sure to download `tails-signing.key` and `tails-amd64-3.12.1.img.sig` (at the “OpenPGP signature for the Tails 3.12.1 USB image” link, the exact name should change for future versions) and place the files in the same directory as the .img file. 
Wait until the USB image is downloaded.

We need to verify what we have downloaded (and that´s why we downloaded the last two files). As we are verifying the download ourselves, skip step 1.2 “Verify your download using your browser”. The browser extension is probably good, but it´s a great practice to do it yourself as the process can be used for other downloads as well. Browser extensions always comes with a risk of leaking personal information, so always be cautious with browser extensions (no idea if this particular extension does that, probably not). 


---
Next up: [Generate the last key with Tails >>](hodl-guide_30_last-key.md)


