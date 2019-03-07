[ [Intro](README.md) ] -- [ [Preparations]( hodl-guide_10_preparations.md) ] -- [ [First Keys](hodl-guide_20_first-keys.md) ] -- [ [Last Key](hodl-guide_30_last-key.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Key storage](hodl-guide_50_key-storage.md
) ] -- [ **Bonus** ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

## Install and optimize Bitcoin Core

*Difficulty: easy*

 Bitcoin Core is the main software implementation of the Bitcoin protocol. Once up and running it will give you a full node that validates all transactions and makes you a first class Bitcoin citizen! 
 
Before starting, you should have a basic understanding about what it means to run a full node.
If you don’t use a VPN or Tor with Bitcoin Core, your IP-address will be exposed to the network. From a privacy standpoint, that should be avoided. It will tell everyone that a Bitcoin full node is running on your IP-address. It’s also possible to connect transactions you do with your full node and your IP-address for someone who’s monitoring the network. This is still an improvement compared to trusting most third-party wallet providers. But it’s a pretty easy fix to improve it even more.

A VPN is an easy solution. This will improve your privacy. You trust the VPN provider to not share any logs. If Bitcoin isn’t illegal in your jurisdiction, that shouldn’t be too big of a deal.
If you´re using a VPN you´ll probably only be able to make outgoing connections (you can't open ports). That won´t affect the validation or broadcasting, but you´ll help the network a bit less since others can't download data from you. 

An even better solution is to run the node over Tor. This’ll make your node very private. Downloading the blockchain over Tor can be very slow. So, it might be a good idea to first download the blockchain (maybe with a VPN) and then configure the node to run over Tor. How to configure Bitcoin Core with Tor will be at the end of this guide.

Start by downloading the latest version of Bitcoin Core at https://bitcoincore.org/.  Make sure that you download SHA256SUMS.asc (should be at the link “Verify release signatures”) and Bitcoin Core Release Signing Keys, laanwj-releases.asc (on the link v0.11.0+).

Before installing, you should always verify the digital signature of the downloaded file. That eliminates many attack vectors.

The easiest way to do this is with the GnuPGP and the command line. For more information on how to download and use GnuPGP, check out the section [First steps]( https://github.com/HelgeHunding/guides/blob/master/hodl-guide/hodl-guide_10_preparations.md#first-steps) where we validate signatures. The process is a little bit different for Bitcoin Core, but the start is the same.

First, we need to change the active directory. This is done with the command “cd”.

To start, we need to change the active directory with `$ cd`. 

*Windows:* Open `Powershell` (search for it or use Win+R, type powershell and hit enter) 

*macOs:* Click the Searchlight (magnifying glass) icon in the menu bar and type `terminal`. Select the Terminal application from the search results. 

*Linux:* Varies, on Ubuntu, press Ctrl+Alt+T 

Change the current directory to the one where the 3 downloaded files are located, for example: 

*Windows* `> cd C:\Users\Downloads` 

*macOS and Linux* `$ cd $HOME/Downloads` 

Import the Bitcoin Core signing key into your local GPG installation:

`$ gpg --import laanwj-releases.asc`

Use the key you imported to verify that the that SHA256SUMS.asc was signed with the right signing key:

`$ gpg --verify SHA256SUMS.asc`

Expected output:
```
gpg: Signature made 12/25/18 09:03:05 W. Europe Standard Time
gpg:                using RSA key 90C8019E36C2E964
gpg: Good signature from "Wladimir J. van der Laan (Bitcoin Core binary release signing key) <laanwj@gmail.com>" [expired]
gpg: Note: This key has expired!
Primary key fingerprint: 01EA 5486 DE18 A882 D4C2 6845 90C8 019E 36C2 E964
```
The important part is that the date`12/25/18`is around the same date as the uploaded file, that it´s a `Good signature` and that the fingerprint is `01EA 5486 DE18 A882 D4C2  6845 90C8 019E 36C2 E964`. You can do a search online and check various sources to control that this is the right signing key. This file is not a detached signature. It contains the hashes of the installation file. You can open the file SHA256SUMS.asc and look at the different hashes (for example, right click and select "Edit with Notepad" in Windows). We now know that this was signed with Wladimir van der Laans key.  

We can now calculate the sha256sum for our installation file and compare the result with the hashes in SHA256SUMS.asc. Write the following to the terminal (change the name of the file to the version you are using):

*Windows:* `> Get-FileHash -a sha256 bitcoin-0.17.1-win64-setup.exe`

*Mac:* `$ shasum -a 256 bitcoin-0.17.1-osx.dmg`

*Linux:* `$ sha256sum bitcoin-0.17.1-x86_64-linux-gnu.tar.gz`

Compare the output to the content in SHA256SUMS.asc for your installation file. If the hashes match (capital letters or not doesn't matter), go ahead and install Bitcoin Core. 

Once the installation is done, run Bitcoin Core. You should see a screen that looks something like this:

![Bitcoin Core](images/61_bitcoin_core.png)

We are going to download a lot of data as you can see. We can do a few optimisations to get a faster initial download and a better user experience overall. Since the size of the blockchain is 220GB and constantly growing you might want to consider storing the blockchain on another disk then your main hard drive. The best solution is an internal hard drive but you could use an external as well (but you’ll have to plug it in every time you run Bitcoin Core). A common setup today is a smaller SSD-disk and a larger mechanical disk, you can then store the blockchain on the mechanical disk.

Another solution is do use a smaller hard drive and use Bitcoin Core in pruned mode. This way you’ll discard old transactions and only have to store ~15 GB of data. You won’t be able to help new nodes with the initial sync, but you’ll still validate all transactions yourself.

Once you’ve decided where to store your blocks, copy the address. For example, in the screenshot above copy `C:\Users\1\AppData\Roaming\Bitcoin`, if you “Use a custom data directory” copy that path, for example `D:\Bitcoin`

Click OK and let the initial sync start. Open a new folder and navigate to the directory you copied the path to. In that folder, create a new file and call it `bitcoin.conf`. For example, on Windows with blocks stored in D:\Bitcoin:

![Bitcoin Core](images/61_bitcoin_folder.png)

We are going modify this file to allocate more RAM to Bitcoin Core. Check how much RAM your computer has (On Windows, Right Click on “This PC” and select “properties”). If you´re not going to run apps that use a lot of CPU during the initial sync, you could probably use 30% (or more) of your RAM without any issues.
Open `bitcoin.conf` with a text editor.

Add the following line: `dbcache=2400`

`2400` is how many MB of your RAM you are allocating to Bitcoin Core (2400MB = 2,4 GB). If you have 8 GB of RAM, this might be a good starting point. If you have more or less RAM, change 2400 to a number that suits you. You can always go back and change this number later. The default allocation is 300 MB so this increase can make the initial download much faster.

If you don’t have 220 GB of space and want to run your full node in pruned mode. Add the following to a new line in bitcoin.conf
`prune=1`

Save and close the file. 

For changes to have effect we need to restart Bitcoin Core. So, shut down the running application. 

Before starting Bitcoin Core again. If you have one SSD and store your blockchain on another mechanical hard drive, there´s one more optimization you can do. Quote from https://en.bitcoin.it/wiki/Splitting_the_data_directory:

"Bitcoin Core's overall speed is significantly affected by the random-access speed of the contents of the chainstate directory; if your data directory is located on a magnetic disk, your chainstate access speed will very probably be the biggest performance bottleneck. You can therefore often massively improve performance by moving just the chainstate directory (which is only a few GB) to an SSD drive."

To move it:
* Make sure that Bitcoin Core is NOT running
* From the data directory (where you added bitcoin.conf), *cut* the chainstate directory (not just its contents, but the directory itself) and *paste* it somewhere on the target SSD drive.

*Windows*: Open Powershell as administrator (search for Powershell, right click and select “Run as Administrator”).
Change the directory to your data directory, for example:

`> cd D:\Bitcoin`

Make a link to where you pasted the folder, in the example below, chainstate is pasted in “documents”:

`> cmd /c mklink /D chainstate C:\Users\1\documents\chainstate`

*Mac/Linux:* Open a terminal in the data directory. On Linux, make sure that permissions allow for Bitcoin Core to read/write the directory and its files at the new location. Make a link to where you pasted the chainstate folder:

`$ ln -s /absolute/path/to/chainstate`. 

For example, if you moved your chainstate so that its new location is `/mnt/ssd/core/chainstate` (ie. within that directory are a bunch of ldb files), you'd run `$ ln -s /mnt/ssd/core/chainstate` from immediately within the data directory.

You should now see a link in your data directory folder (D:\Bitcoin in the example on Windows above)

You can now start Bitcoin Core and the sync should be much faster.

You can sync the blockchain in parts, you don't have to keep your computer on until the full blockchain is synced.

Once up and running, you can start and close Bitcoin Core whenever you like without any issues.


### Running Bitcoin Core over Tor

As we stated earlier, running your Bitcoin Core node over Tor might be a good idea. If you have Tor installed, this is literary only one checkbox. 
If you don’t have Tor installed, go to https://www.torproject.org/projects/torbrowser.html and follow the instructions for your operating system. You can launch the browser (it’s much easier to use then a few years ago) or start Tor.exe (that should be located at `..\Tor Browser\Browser\TorBrowser\Tor`) 
Think about having this process autostart with your computer or put a shortcut to it in your Bitcoin-folder.
In Bitcoin Core, go to Settings>Options
Change the tab to Network and select “Connect through SOCKS5 proxy (default proxy):”
Make sure Proxy IP is `127.0.0.1` and port `9050` (the Tor default port number):

![Bitcoin Core](images/61_bitcoin_network.png)

Restart Bitcoin Core to activate changes.
More information at https://en.bitcoin.it/wiki/Tor


*Optional*: Verify that you are connected over Tor. In Bitcoin Core, go to Help>Debug Window
Change the tab to Console and type `getnetworkinfo` and hit enter.

You should see the following output:

![Bitcoin Core](images/61_tor.png)

Make sure that “proxy” is 127.0.0.1:9050 and that “onion” is reachable. If that’s the case, you are now using Tor.

------

<< Back: [Bonus guides](hodl-guide_60_bonus.md) 
