[ [Intro](README.md) ] -- [ [Preparations](raspibolt_10_preparations.md) ] -- [ **The First Keys** ] -- [ [Lightning](raspibolt_40_lnd.md) ] -- [ [Mainnet](raspibolt_50_mainnet.md) ] -- [ [Bonus](raspibolt_60_bonus.md) ] -- [ [Troubleshooting](raspibolt_70_troubleshooting.md) ]

---

# Generate the last key with Tails

We are generating the last key with Electrum on a computer booted with Tails, https://tails.boum.org/. Tails is a live operating system that´s built upon Debian (a Unix-like operating system). 
It´s booted from a USB-stick and only uses the computers RAM-memory which means that all sensitive information is erased when the USB is ejected (and your computer will start with your usual operating system like nothing happened). 

## Starting on Tails
Go to https://tails.boum.org/install/index.en.html and choose your operating system. If you don´t have an old copy of Tails, select “Install from {Your operating system}”. 
Select “Let´s go” and download the USB image at step 1.1 to a directory on your computer. At the download page, make sure to download `tails-signing.key` and `tails-amd64-3.12.1.img.sig` (at the “OpenPGP signature for the Tails 3.12.1 USB image” link, the exact name should change for future versions) and place the files in the same directory as the .img file. 
Wait until the USB image is downloaded.

### Verify signatures

We need to verify what we have downloaded (and that´s why we downloaded the last two files). As we are verifying the download ourselves, skip step 1.2 “Verify your download using your browser”. The browser extension is probably fine, but it´s a great practice to do it yourself as the process can be used for other downloads as well. And browser extensions always comes with a risk of leaking personal information, so always be cautious with browser extensions (no idea if this particular extension does that, probably not). 

It’s the same procedure as before (check the [Preparations](raspibolt_10_preparations.md) for more information about validating signatures). 

Change the current directory to the one where the 3 downloaded files are located: 
`$ cd $HOME/Downloads`

To be able to verify the signature, import the Tails-signing key into your local GPG installation: 

`$ gpg --import tails-signing.key`

Now use the “detached signature” to check that the .img file was signed with the signing key we imported:

`$ gpg --verify tails-amd64-3.12.1.img.sig tails-amd64-3.12.1.img` (make sure to change the file name on both places if using a newer version). The verification can take a while. 

Expected output should be something like:
```
gpg: Signature made 01/28/19 18:44:16 W. Europe Standard Time 
gpg: using RSA key FE029CB4AAD4788E1D7828E8A8B0F4E45B1B50E2 
gpg: Good signature from "Tails developers (offline long-term identity key) <tails@boum.org>" [unknown] 
gpg: aka "Tails developers <tails@boum.org>" [unknown] 
gpg: WARNING: This key is not certified with a trusted signature! 
gpg: There is no indication that the signature belongs to the owner. 
Primary key fingerprint: A490 D0F4 D311 A415 3E2B B7CA DBB8 02B2 58AC D84F 
Subkey fingerprint: FE02 9CB4 AAD4 788E 1D78 28E8 A8B0 F4E4 5B1B 50E2 
```
The important part is the date, `Good signature` and Primary key fingerprint `A490 D0F4 D311 A415 3E2B B7CA DBB8 02B2 58AC D84F` 
This ensures that the .img file was signed with a key with the fingerprint A490 D0F4… at a date, not to long before the release. If we do an online search, one of the first matches was [@Tails_live](https://twitter.com/tails_live) on what seems to be a legit Twitter account and who has the fingerprint in the bio. 

Another match is a post from 2015 on the official webpage that announces a change to this key and we can also see several old posts from Reddit. We can be almost certain (not possible to do more) that this release was indeed signed by the developers. This process would catch a scenario were a malicious actor had taken control over the webpage and uploaded a bad file and a bad signing key. If you get a bad signature or another fingerpringt, stop and investigate further before installing anything. 

If everything is good, go ahead and create the boot usb. This is going to be used to create the last private key.  

### Flash Tails to USB

The easiest way is to follow the instructions on https://tails.boum.org/install for your operating system. 

So, insert the USB you are going to use in your computer and follow the instructions at “2/5 Install Tails”. In Mars 2019 that means downloading, running and flashing the USB with Etcher for Windows and macOS and with GNOME Disks for Linux. When step 2/5 is completed, you´ve got two choices. 

If you use one computer. Tails is going to be started on the computer you are reading this on. In that case you´re going to have to print or write down the rest of the of the instructions on this page. You could also bring the instructions up on another device (keep them in flight mode and don’t let any cameras see any screens or private keys). Make sure no other USB drives is connected to the computer.

If you are using two computers. Tails is going to be started on the other computer and you can keep the instructions on the main computer. The other computer could be a normal computer that's going to be used for other things after the process. Or for extra security, an eternally quarantined computer. Make sure no other USB drives is connected to the computer.

## Start computer on Tails

Go ahead and make sure that the USB with Tails is inserted in the right computer. Start (or restart) the computer.

If the computer starts on Tails, the ”Boot Loader Menu” should appear:
![Tails boot loader](images/20_boot_loader.png)
Tails should be selected and start automatically after a few seconds. If it does, follow the instructions on the screen for starting (setting up language and keyboard) and start Tails. 

Otherwise, restart the computer and bring the boot menu up. The key for bringing the boot menu up differs from manufacturer to manufacturer. 
*On PC*, It´s usually Esc or F12 (but could be F8, F9 or F10 as well). Choose the USB-stick with tails in the menu. If that doesn´t work, you might have to change settings in Bios (turn off secure start, change start order, disable fast start etc).

Check the troubleshooting guide at the install page for Tails for more information. There could be issues with certain computers or graphic cards, check the troubleshooting guide to see if there´s an easy fix. 

*On Mac*, Immediately press-and-hold the Option key (Alt key) until a list of possible start-up disks appears. 
If the computer starts on Tails, the Boot Loader Menu appears and Tails starts automatically after 4 seconds. There could be issues with certain computers or graphic cards, check the troubleshooting guide at the install page to see if there´s an easy fix.

When you get past the boot loader menu, follow the instructions on the screen to start Tails.

## Generating the private key with Electrum

Once started, make sure WiFi is disconnected (arrow in upper right corner, should say “Wi-Fi not connected). 

Go to Applicatios (upper left corner) > Internet > Electrum Bitcoin Wallet. Click on `launch` if a window about persistence appears.

The Electrum – Install Wizard should appear. The name of the wallet isn’t important (it will be deleted), so “default_wallet” is ok. Click Next:
![Electrum 1](images/20_electrum_1.png)
On the next step, let “Standard wallet” be selected (we are only interested in generating a seed). Click Next:
![Electrum 2](images/20_electrum_2.png)
On the next step, let “Create a new seed” be selected. Click Next:
![Electrum 3](images/20_electrum_3.png)
On the next step, change “Seed type” to Segwit. Segwit is a newer type of address, so services that´s slow to update might have issues sending to these types of addresses. But it should be possible from most services and it´s a more “modern” address that usually works better with multi-sig in Electrum. Click Next:
![Electrum 4](images/20_electrum_4.png)
You should now see 12 words. Electrum uses 12 words for it´s seed, most hardware wallets uses 24. Today the difference doesn’t really matter, the security is plenty (and we’re going to generate two more keys with 24 words). Write the 12 words you see on your screen down by hand on a piece of paper of good quality. This is your last private key. Then click next:
![Electrum 5](images/20_electrum_5.png)
Confirm your seed by typing all the words you wrote down in the field. When finished, click Next:
![Electrum 6](images/20_electrum_6.png)
You should see a screen asking for a password. We don’t need a password (since everything is deleted once finished), so click Next:
![Electrum 7](images/20_electrum_7.png)

Electrum is now generating addresses, it can take a few seconds before the main window shows up. The key is generated! 

Before moving on, we need the master public key for our multi-sig contract and check what version of Electrum we are running.

Start with the version. Check what version of Electrum that´s running on Tails. For example, Tails 3.12.1 comes with Electrum 3.1.3. Note this on a piece of paper or on your main computer.
![Electrum 8](images/20_electrum_8.png)
Now we only need to copy the master public key. The master public key is used in our multi-sig contract and to derive bitcoin addresses to send fund to. To show the master public key in Electrum, go to `Wallet>Information`. 

We need to copy this to our live system were we´ll construct the multi-signature contract. But we don’t want to put another USB in to our system at this point (reduce any risk of information about our private key leaking). Your public master key doesn´t really affect your bitcoin’s security (no one can steal your funds with a public key). But all your bitcoin-addresses can be generated from the master public key. So, for privacy, it should be treated with care (in a multi-sig you would ne, but it isn´t as sensitive as a private key. The key can be represented as a QR code. In the bottom right corner, click “Show as QR-code”: 
![Electrum 9](images/20_electrum_9.png)
It´s now safe to bring other electronic devices near the computer that generated the private key. So, you can turn your cell phone on, but put it in flight mode so nothing is uploaded to any cloud service (or use a digital camera). We are going to use several cameras, so double check that no private keys are lying around. With your cell phone, taka a photo of the QR-code that represents the master public key. 

If you use one computer, remove the tails boot USB from the slot and restart the computer on your regular OS (you can keep Tails running if you use two computers). 

### Download and verify Electrum

On your main computer (or regular OS) go to https://electrum.org/#download
For our multi-sig to work on both systems, you might need the same version of Electrum as the one used in Tails. But first we need the signing key of Electrum developer Thomas Voegtlin. Scroll down to the bottom of the page and click on the “Public Key” link (you can skip this on Linux and use gpg --import ThomasV.asc):
![Electrum 10](images/20_electrum_10.png)
That should take you to a page with the public key, use `Ctrl+S` and save the file `ThomasV.asc` on your computer.

Go back to https://electrum.org/#download and check what the latest release is. Chanses are that the latest release is newer then the one used in Tails. If that´s the case we need an older release, click “Previous releases”:
![Electrum 11](images/20_electrum_11.png)
That should take you to https://download.electrum.org/. Go to the folder with the same version number as the one in Tails (for example 3.1.3 with Tails 3.12.1). Download the file for your OS (tar.gz for Linux, -setup.exe for Windows and .dmg for macOS) and make sure to download the corresponding .asc file as well. Put the files in the same folder as ThomasV’s signing key:
![Electrum 12](images/20_electrum_12.png)
*Note*, if you´re already using a newer version of Electrum. Downgrading the version might make wallets created with newer versions temporary unusable. Once done with the cold storage, you can upgrade to a newer version of Electrum and everything should work again. Your funds aren´t at risk, you can always recover your funds (or import to an older version) with your recovery seed. 

Once downloaded we need to verify the download in the same way we verified Tails. 
Open a terminal (for example Powershell on Windows).
Change the current directory to the one where the 3 downloaded files are located: 

`$ cd $HOME/Downloads` 

Import the signing key from ThomasV into your local GPG installation: 

`$ gpg --import ThomasV.asc` 

Now use the .asc to check that the Electrum installer was signed with the signing key we imported: 

`$ gpg --verify tails- electrum-3.1.3-setup.exe.asc electrum-3.1.3-setup.exe` (make sure to change the file name on both places if using a newer version). 
The verification can take a while. 

Expected output:
```
gpg: assuming signed data in 'electrum-3.1.3-setup.exe'
gpg: Signature made 04/18/18 17:10:44 W. Europe Daylight Time
gpg:                using RSA key 2BD5824B7F9470E6
gpg: Good signature from "ThomasV <thomasv1@gmx.de>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 6694 D8DE 7BE8 EE56 31BE  D950 2BD5 824B 7F94 70E6
```
The signing was made the same day as the release was uploaded (should be around the same time). 
It´s a `Good signature`. 
A search online on `6694 D8DE 7BE8 EE56 31BE  D950 2BD5 824B 7F94 70E6` seems to verify that this key belongs to Thomas V. We are good to go. Install Electrum and follow the instructions on screen.

### Start creating the multi-sig

Start Electrum. We are going to create a new wallet. If you already have a default Electrum Wallet open, go to `File>New/Restore` (or use Ctrl+N). Otherwise the install wizard should be launched automatically. 

Pick a name for your multi-sig wallet and click Next:
![Electrum 13](images/20_electrum_13.png)
Select "Multi-signature wallet" and hit Next:
![Electrum 14](images/20_electrum_14.png)
Change the first slider to 3 cosigners (with 2 signatures required) and click Next:
![Electrum 15](images/20_electrum_15.png)
Start with the seed you created in Tails. Select “Use a master key”:
![Electrum 16](images/20_electrum_16.png)
Click the QR-code in the bottom right corner:
![Electrum 17](images/20_electrum_17.png)

## Troubleshooting 
If you get the following error:
![Error 1](images/20_error_1.png)
You’ll probably need to install “Zbar” (or launch it if it’s installed). It’s available at http://zbar.sourceforge.net/ and you can view the source code at https://github.com/ZBar/ZBar. (Only Windows and Linux). It’s generally a good idea to not download random programs from file hosting sites. But Zbar has been around a long time and we can try to ensure it’s a legit copy. If you still don’t want to use Zbar, scroll down to “other solutions”- Otherwise go to https://sourceforge.net/projects/zbar/files/zbar/0.10/. Make sure that “Modified” is 2009-10-XX:
![Zbar](images/20_zbar.png)
Download the file for your operating system (.exe for Windows and tar.gz or tar.bz2 for Linux). No digital signatures are provided, so we are going to generate the SHA256-checksum of the file. Open a new terminal and change the directory to where the file is located:

`$ cd $HOME/Downloads` 
Generate the checksum:
*on Windows* `> Get-FileHash -a sha256 zbar-0.10-setup.exe`
You should get the following output: 
![Zbar hash](images/20_zbar_hash.png)
*on Linux*: 
`$ sha256sum zbar-0.10.tar.gz`
Should produce the output:
`575fa82de699faa7bda2d2ebbe3e1af0a4152ec4d3ad72c0ab6712d7cc9b5dd2  zbar-0.10.tar.gz`
And:
`$ sha256sum zbar-0.10.tar.bz2`
Should produce the output:
`234efb39dbbe5cef4189cc76f37afbe3cfcfb45ae52493bfe8e191318bdbadc6  zbar-0.10.tar.bz2`

It’s the best we can do here and Zbar won’t be handling any critical information. If the hashes match, you know that you’ve got the same file that was used in this guide. If you are okey with that, go ahead and install Zbar and follow the instructions on the screen. Go back to Electrum and click the QR-code, you might have to try 2-3 times before it starts. 

If it still doesn’t start, start the program “zbarcam”, pick a video source, click apply and try in Electrum again:
![Zbarcam](images/20_zbarcam.png)

Scan the QR-code in Electrum. It should read your xpub key and Electrum should automatically show it. 

Other solutions:
If you can’t launch or don’t want to use Zbar, you could use a workaround. 

Option 1 is to simply download another QR-reader on your computer (or check if you have one installed) and scan the QR-code. Copy the scanned result to Electrum. 

Option 2, use a QR-code reader on your smart-phone. Load the photo to the QR-code reader, connect to internet and send the text to your computer with a secure messaging app. 

Option 3, use an online-service like https://webqr.com/index.html. Know that you risk to leak your public key to a third party (which reduces your privacy but isn’t terrible in this case since it’s only 1 of 3 needed keys). Copy the result to Electrum. 

Continuing



---
Next up: [Generate the last key with Tails >>](hodl-guide_30_last-key.md)


