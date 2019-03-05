[ [Intro](README.md) ] -- [ [Preparations]( hodl-guide_10_preparations.md) ] -- [ [First Keys](hodl-guide_20_first-keys.md) ] -- [ [Last Key](hodl-guide_30_last-key.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Key storage](hodl-guide_50_key-storage.md
) ] -- [ **Bonus** ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

## Install and optimize Bitcoin Core

*Difficulty: easy*

 Bitcoin core is the main software implementation of the Bitcoin protocol. It will give you a full node that validates all transactions.
 
 Before starting, you should have a basic understanding about what it means to run a full node.
If you don’t use a VPN or Tor whit Bitcoin Core, your IP-address will be exposed to the network. From a privacy standpoint, that should be avoided. It’ll tell everyone that a Bitcoin full node is running on your IP-address. It’s also possible to connect transactions you do with your full node and your IP-address for someone who’s monitoring the network. This is still a huge improvement compared to trusting various third-party wallet providers. But it’s a pretty easy fix to improve it even more.

A VPN is an easy solution. This will improve your privacy, but you trust the VPN provider to not share any logs. If Bitcoin isn’t illegal in your jurisdiction, that shouldn’t be too big of a deal.
If you´re using a VPN you´ll probably not be able to open ports. That´s needed if you want to accept inbound connections (so people can download data from you). That won´t affect the validation or broadcasting, but you´ll help the network a bit less. 

An even better solution is to run the node over Tor. This’ll make your node very private. Downloading the blockchain over Tor can be very slow. So, it might be a good idea to first download the blockchain and then configure the node to run over Tor. How to configure Bitcoin Core with Tor will be at the end of this guide.

Start by downloading the latest version of Bitcoin Core at https://bitcoincore.org/.  Make sure that you download SHA256SUMS.asc (should be at the link “Verify release signatures”) and Bitcoin Core Release Signing Keys, laanwj-releases.asc (on the link v0.11.0+).

Before installing, you should always verify the digital signature of the downloaded file. That eliminates many attack vectors.

The easiest way to do this is with the GnuPGP and the command line. For more information on how to download and use GnuPGP, check out this section [Validate signatures]( https://github.com/HelgeHunding/guides/blob/master/hodl-guide/hodl-guide_10_preparations.md#first-steps)

First, we need to change the active directory. This is done with the command “cd”.

To start, we need to change the active directory with `$ cd`. 

*Windows:* Open `Powershell` (search for it or use Win+R, type powershell and hit enter) 

*macOs:* Click the Searchlight (magnifying glass) icon in the menu bar and type `terminal`. Select the Terminal application from the search results. 

*Linux:* Varies, on Ubuntu, press Ctrl+Alt+T 

Change the current directory to the one where the 3 downloaded files are located, for example: 

*Windows* `> cd C:\Users\Downloads` 

*macOS and Linux* `$ cd $HOME/Downloads` 

Import the Bitcoin Core signing key into your local GPG installation:

`$ gpg --import $HOME/Downloads/laanwj-releases.asc`

(change the path to were your file is located and make sure that the name of the .asc file matches the one you downloaded)
Use the key you imported to verify that the “fingerprint file” is legitimate (that the fingerprint file was made by the same person that created the signing key):

`$ gpg --verify SHA256SUMS.asc`

Expected output:
```
gpg: Signature made 12/25/18 09:03:05 W. Europe Standard Time
gpg:                using RSA key 90C8019E36C2E964
gpg: Good signature from "Wladimir J. van der Laan (Bitcoin Core binary release signing key) <laanwj@gmail.com>" [expired]
gpg: Note: This key has expired!
Primary key fingerprint: 01EA 5486 DE18 A882 D4C2  6845 90C8 019E 36C2 E964
```
The important part is that the date`12/25/18`is around the same date as the uploaded file, that it´s a `Good signature` and that the fingerprint is `01EA 5486 DE18 A882 D4C2  6845 90C8 019E 36C2 E964`. You can do a search online and check various sources to control that this is the right signing key.

If everything looks good, go ahead and install Bitcoin Core. 
