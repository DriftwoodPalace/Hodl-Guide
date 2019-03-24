[ **Guide** ] -- [ [Bonus](https://github.com/HelgeHunding/guides/blob/master/hodl-guide/hodl-guide_60_bonus.md) ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

# The Hodl Guide Ultralight

---

#### *This is a draft, all feedback is appreciated!*

This is a guide for anyone who wants to start taking control of their bitcoin holdings. Maybe you have your bitcoin on an exchange, in a web wallet or in a “hot wallet” on your computer. Or maybe you already have one or more hardware wallets but use the providers own wallet.
This is a guide for cold storage and not for a wallet used for “day to day spending”.
After you’ve completed this guide, you’ll have a foundation that you can keep building on. You can later use your new knowledge and wallet and upgrade it to a more secure multi-sig with [Hodl Guide Light]( https://github.com/HelgeHunding/guides/blob/master/hodl-guide-light/README.md) or go all the way with the more complex [Hodl Guide]( https://github.com/HelgeHunding/guides/blob/master/hodl-guide/README.md).
As always with Bitcoin, I or no one else can be responsible for your bitcoin. You have to trust and hold yourself responsible for everything.
The guide will use one hardware wallet. I have experience with Trezor One and Ledger Nano S, so the guide will follow the procedure on those wallets. But you can use another hardware wallet if you like it and trust the manufacturer.
Hardware wallets are great. But their main focus is security, not privacy. We do not know what the future might bring. For example, how governments will treat bitcoin. It’s better to be safe then sorry and keep your holdings private.
Privacy isn’t black or white, it’s a scale. Your privacy can be breached in many ways and every individual leak can be combined to reduce your privacy. We’ll try to avoid some of the worst mistakes.
Start by ordering a hardware wallet. As this is specialised hardware used for storing cryptocurrencies on, consider having it shipped to a UPS access point or a similar service to not reveal your real address.
Setup the hardware wallet with the manufacturer’s instructions. Make sure no cameras can see you when you write your seed down. Use the manufacturers wallet software to upgrade the firmware on the device to the latest version.  If you use a Ledger Nano S, you can use an easier PIN. We are going to change that later. If you use a Trezor One, pick a strong PIN that you can remember.
### Download and install Electrum
We are not going to use the manufacturers wallet to store our bitcoin.  We are using the much more flexible Electrum Wallet.
Electrum is a wallet that has been around for many years. It offers great usability (support for multi-sig, hardware wallets etc) and you can connect it to your Bitcoin Core full node. 
Go to https://electrum.org/#download and download the installer for your operating system. We are going to verify the download with the detached signature as well (the link is next to the installer). So, download that as well.

We need the signing key of Electrum developer Thomas Voegtlin to verify the signatures. Scroll down to the bottom of the page and click on the “Public Key” link (you can skip this on Linux and use gpg --import ThomasV.asc):

![Electrum 10](images/40_electrum_10.png)

That should take you to a page with the public key, use `Ctrl+S` and save the file `ThomasV.asc` on your computer (preferably in the same location as the downloaded installer).

Once downloaded we need to verify the signatures to make sure the developers signed this release. This is an important step. This would catch a scenario where electrum.org was compromised or where you went to the wrong site to download a malicious version (100s of bitcoin has probably been lost because of this).

To verify what we downloaded, we need GnuPG (https://gnupg.org/). The implementation varies for different OS:

*Windows:* Download and install the latest version of Gpg4win https://www.gpg4win.org. If you don’t want to donate, click bank transfer on the download page to acces the download. You only need to install GnuPG and Kleopatra. Start Kleopatra once finished. 

*macOS:* Download and install the latest version of GPG Suite https://gpgtools.org/ 

*Linux:* GnuPG comes pre-installed with Linux distributions.

An easy way to verify a digital signature is to use a terminal (the command line). 
In all examples, what´s written to the terminal is everything after the `$` sign (and examples that's specific for Windows uses the symbol `>`). 

For example: `$ cd` 
Means that you´d write `cd` to the command line (cd is a command that changes the active directory). 
Usually you can paste text to a terminal with ctrl+v or with a right click on the mouse. Another useful shortcut is to use the arrows up and down to toggle between previously executed commands. If you´re stuck, you can usually kill a process with Ctrl+C or Ctrl+Z. 

To start, we need to change the active directory with `$ cd`. 

*Windows:* Open `Powershell` (search for it or use Win+R, type powershell and hit enter) 

*macOs:* Click the Searchlight (magnifying glass) icon in the menu bar and type `terminal`. Select the Terminal application from the search results. 

*Linux:* Varies, on Ubuntu, press Ctrl+Alt+T 

Change the current directory to the one where the 3 downloaded files are located, for example: 

*Windows* `> cd ~Downloads` 

*macOS and Linux* `$ cd ~/Downloads` 

Import the signing key from ThomasV into your local GPG installation: 

`$ gpg --import ThomasV.asc` 

Start by verifying the appimage. Use the .asc-file to check that the file was signed with the signing key we imported: 

`$ gpg --verify electrum-3.3.4-x86_64.AppImage.asc`

(make sure to change the file name if using a different version). 

The verification can take a while. 

The output should be something like:
```
gpg: assuming signed data in 'electrum-3.3.4-x86_64.AppImage'
gpg: Signature made 02/13/19 23:08:30 W. Europe Standard Time
gpg:                using RSA key 6694D8DE7BE8EE5631BED9502BD5824B7F9470E6
gpg: Good signature from "ThomasV <thomasv1@gmx.de>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 6694 D8DE 7BE8 EE56 31BE  D950 2BD5 824B 7F94 70E6
```
The signing was made the same day as the release was uploaded (should be around the same time), you can see the dates here https://download.electrum.org/.

It´s a `Good signature`. 

A search online on `6694 D8DE 7BE8 EE56 31BE D950 2BD5 824B 7F94 70E6` seems to confirm that this key belongs to Thomas V. We are good to go. Install Electrum and follow the instructions on screen.

If you are using Windows or macOs, go ahead and verify that file as well. For example on Windows:

`$ gpg --verify electrum-3.1.3-setup.exe.asc` 

The output should be almost the same, for example:
```
gpg: assuming signed data in 'electrum-3.3.4-setup.exe'
gpg: Signature made 02/13/19 23:08:30 W. Europe Standard Time
gpg:                using RSA key 6694D8DE7BE8EE5631BED9502BD5824B7F9470E6
gpg: Good signature from "ThomasV <thomasv1@gmx.de>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 6694 D8DE 7BE8 EE56 31BE  D950 2BD5 824B 7F94 70E6

WORK IN PROGRESS


---
Get started: [Preparations >>](hodl-guide_10_preparations.md)



