[ [Intro](README.md) ] -- [ **Preparations** ] -- [ [Raspberry Pi](raspibolt_20_pi.md) ] -- [ [Bitcoin](raspibolt_30_bitcoin.md) ] -- [ [Lightning](raspibolt_40_lnd.md) ] -- [ [Mainnet](raspibolt_50_mainnet.md) ] -- [ [Bonus](raspibolt_60_bonus.md) ] -- [ [Troubleshooting](raspibolt_70_troubleshooting.md) ]

-------
### Beginner’s Guide to ️⚡Lightning️⚡ on a Raspberry Pi
--------

# Preparations

## Mandatory Hardware Requirements for Full Setup

*	1 USB-drive with 8GB+ memory. Consider buying a new one, used only for this purpose.
*	2 different Hardware-wallets (Trezor, Ledger, Coldcard etc). Make sure the hardware-wallets are from two different manufacturers (e.g. one Trezor and one Ledger). You can use existing devices if you already own some (but they can't be used for other purposes after you're done). If you're buying new ones, make sure to only buy from the official store. It's always sensitive to have Bitcoin-related stuf shipped to your home. Consider having it delivered to a UPS access point or a similar service.
*	1 internet connected computer. Could be your normal computer. Should have at least 1 USB-slot and a camera (for reading QR-codes). If you only use one computer, the computer needs to have a 64-bit processor.
*	1 Smartphone (or digital camera with screen)

## Optional Equipment and Hardware 

* 1 extra computer. This will make the process of working with Tails easier. If you have an old computer lying around, consider using it and making it an eternally quarantined computer. That’s a computer that´s going to be eternally quarantined (only used for this purpose and never used for anything else or connected to the internet again). If you are using an eternally quarantined computer it’s a good idea to format/reinstall the computer to get it as fresh as possible. You can even wipe the operating system of the computer since we are using Tails. Before wiping the OS, try it out with Tails. You might have to update some drivers for it to work. The computer needs 1 USB-slot, a camera and needs to have a 64-bit processor. If you’re not sure or if you’re buying a used computer, you can search for the computer’s processor on http://www.cpu-world.com. “Data width” should be 64 bit. 
*	Home safe, for safe, waterproof and fireproof storage of one of the private keys.
*	TerraSlate paper (https://www.amazon.com/dp/B076JKVNWY/), waterproof, heat resistant and tear-resistant paper.
*	Envelopes to store the private keys in. 
*	Cryptosteel or similar product that stores a private key on a metal plate (then you don´t need TerraSlate).
*	Tamper-resistant seals or tape.

## First steps

An important part of the guide (and a great skill to have) is to know how to validate digital signatures. We are going to do a validation of this guide as a practice (and to control the guide).

To start, download my signature `hundingsbane.asc`, `hodl-guide.pdf` and `hodl-guide.pdf.sig` HERE. It’s simply my digital fingerprint a .pdf file with this guide and a detached signature corresponding to the .pdf file. This ensures that the one controlling the public key hundingsbane.asc (me) signed the document.   

To do this, we need GnuPG (https://gnupg.org/), the implementation of it varies for different OS:

*Windows:* Download and install the latest version of Gpg4win https://www.gpg4win.org. If you don’t want to donate, click bank transfer on the download page to acces the download without donating. You only need to install GnuPG and Kleopatra. Start Kleopatra once finished. 

*macOS:* Download and install the latest version of GPG Suite https://gpgtools.org/ 

*Linux:* GnuPG comes pre-installed with Linux distributions.

An easy way to verify a digital signature is to use the command line (terminal). 
In all examples, what´s written to the command line is everything after the `$` sign (and examples that's specific for on Windows use the symbol `>`). 

For example: `$ cd` 
Means that you´d write `cd` to the command line (cd is a command that changes the active directory). 
Usually you can paste text to a terminal with ctrl+v or with a right click on the mouse. Another useful shortcut is to use the arrows up and down to toggle between previously executed commands. If you´re stuck, you could kill a process with Ctrl+C or Ctrl+Z. 

To start, we need to change the active directory. This is done with the command `cd`. 

*Windows:* Open `Powershell` (search for it or use Win+R, type powershell and hit enter) 

*macOs:* Click the Searchlight (magnifying glass) icon in the menu bar and type `terminal`. Select the Terminal application from the search results. 

*Linux:* Varies, on Ubuntu, press Ctrl+Alt+T 

Change the current directory to the one where the 3 downloaded files are located, for example: 
*Windows* `> cd C:\Users\Downloads` 
*macOS and Linux* `$ cd $HOME/Downloads` 

To be able to verify the signature, import hundingsbane.asc into your local GPG installation: 
`$ gpg --import hundingsbane.asc` 
Now use the “detached signature” to check that the .pdf file was signed with the signing key we imported: 
`$ gpg --verify valaskjalf.txt.sig valaskjalf.txt` 
The expected output should be something like:
```
gpg: Signature made 03/01/19 16:32:53 W. Europe Standard Time
gpg:                using RSA key FF541B4EE4E6D84593011D403D27D7D359A0E4A9
gpg: Good signature from "Helge Hundingsbane" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: FF54 1B4E E4E6 D845 9301 1D40 3D27 D7D3 59A0 E4A9
```

There's three key points to look at when verifying a signature. When the signature was made (`03/01/19` in the example above). It should be around the time that the file was uploaded. That it’s a `Good signature` and what the primary key fingerprint is (in this case `FF54 1B4E E4E6 D845 9301 1D40 3D27 D7D3 59A0 E4A9`. 
To check that the fingerprint indeed seems to belong to me, you could check my Twitter and my Keybase. Signers usually keep their fingerprint in their social profiles. For more critical downloads (like Electrum or Bitcoin Core) it’s a good idea to do a search online on the fingerprint. That should give results on forums etc, that’s hard to fake. 
[Twitter](https://twitter.com/HelgeHunding)
[Keybase](https://keybase.io/helgehunding)

Now we know that this was a good signature made from me. If someone was to change one character in hodl-guide.pdf, it would result in a bad signature. If you get a bad signature when validating something, you should stop and investigate further before doing anything else with the file. You could open hodl-guide.pdf and select a few parts of the text and compare it to what’s written here on Github. If it’s not the same, you should stop and investigate further. The layout is better on Github, so I would recommend that you follow along here.

Now that we have this knowledge, we can start generating private keys! Before moving on, if you don’t have Bitcoin Core installed and synced, you might want to start the process now.

**[P]** Bitcoin Core. We don´t want to go through all this trouble to secure our keys and then rely on trusted third parties for validations. That´s why we´re using Bitcoin Core to validate all transactions. Bitcoin core is the main software implementation of the Bitcoin protocol. By running your own node, you´re also helping the network and making it more decentralized. 
Note, the Bitcoin blockchain size is approaching 300 GB. It could take several days to download the whole blockchain. If storage is an issue, you could use “pruned mode”. That way, you´d discard old transactions and only need to store as little as 15 GB of data. You won’t be able to help new nodes connect, but you´d still validate everything yourself. But if you´re on a limited data plan, downloading 300 GB of data might be an issue. In that case you´d have to rely on third parties for validating and broadcasting transactions and can skip this step. If you don´t have a full node up and running, see the bonus section for how to setup and validate the installation of one. When installed, your node could be running in the background. You won´t notice it on most modern computers and you don´t have to be online all the time. LINK

---
Move on to: [The first keys >>](hodl-guide_20.md)
