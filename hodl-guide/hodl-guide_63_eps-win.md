[ [Intro](README.md) ] -- [ [Preparations]( hodl-guide_10_preparations.md) ] -- [ [First Seeds](hodl-guide_20_first-seeds.md) ] -- [ [Last Seed](hodl-guide_30_last-seed.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Storage](hodl-guide_50_storage.md
) ] -- [ **Bonus** ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

# Electrum Personal Server on Windows 10

*Difficulty: medium*

Electrum Personal Server will connect your Bitcoin full node to Electrum. This will make it possible to use all functionality in Electrum with your full node (Hardware Wallet support, easy multi-sig setup and more). 

Before starting, make sure you’ve got a Bitcoin Core full node running and up to sync. If don’t, see [Install and optimize Bitcoin Core](hodl-guide_61_bitcoin-core.md).

You also need Electrum https://electrum.org/#download (you should always check the digital signatures before installing, more info on how [Here](https://github.com/HelgeHunding/guides/blob/master/hodl-guide/hodl-guide_40_multi-sig.md#download-and-verify-electrum))

## Download the installation package

Go to https://github.com/chris-belcher/electrum-personal-server and read the intro (before How To) to know what this is and why it’s important. 
Before we install anything, we need Chris Belchers signing-key to verify any downloads. It can be found here https://github.com/chris-belcher/electrum-personal-server/blob/master/pgp/pubkeys/belcher.asc

Click “raw”:

![Eps Win1](images/63_eps-w_1.png)

Hit `Ctrl+S` and save the key in a folder on your computer (preferably where you download files to).

To verify the signature, we need Gpg4win. If it’s not already installed, go to https://www.gpg4win.org and install the latest release for Windows. If you don’t want to donate, click bank transfer on the download page to acces the download. You only need to install GnuPG and Kleopatra. Start Kleopatra once finished.

We need to start a new terminal. Open “Powershell” (search for it or use Win+R, type powershell and hit return).

We need to change the working directory to the directory where the file is located. If you've placed the file in "downloads" type the following (everything after `>`) to the terminal:

`> cd downloads`

You can also use the whole path:

`> cd C:\Users\User1\Downloads`

Import Belchers signing key to your local directory:

`> gpg --import belcher.asc`

It’s now imported. Navigate to the release page at https://github.com/chris-belcher/electrum-personal-server/releases and download the latest `Source code (.zip)` and the corresponding `.asc` file. For example:

![Eps Win2](images/63_eps-w_2.png)

Once downloaded, make sure that the working directory is the one where the files are located. Enter the following command (if you downloaded another version, change the file names):

`> gpg --verify eps-v0.1.6.zip.asc electrum-personal-server-eps-v0.1.6.zip`

The output should be something similar to this:
```
gpg: Signature made 11/15/18 23:30:04 W. Europe Standard Time
gpg:                using RSA key EF734EA677F31129
gpg: Good signature from "Chris Belcher <false@email.com>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 0A8B 038F 5E10 CC27 89BF CFFF EF73 4EA6 77F3 1129
```

We can see that the signature was made at a date close to the release, it's a `Good signature` and the Primary key fingerprint is the same as on Github. We can double check by doing a search online on the fingerprint. That confirms from various sources that the key seems to belong to Chris Belcher. You can go ahead an unzip the .zip file to any location on your computer.

## Change the config-file

Go into the unzipped folder and make a copy of the file `config.cfg_sample` and rename the copy to `config.cfg` (you’ll get a warning about changing the file name extension, select Yes). 

*Note:* Make sure that you can see file extensions, it can be changed at “View” in the top-bar. While there make sure “hidden items” is checked as well:

![Eps Win3](images/63_eps-w_3.png)

Right click on the file and select edit to edit it with a text editor (notepad etc). 

#### For multi-sig wallets

If you are following the hodl-guide or have an electrum multi-sig wallet you'd like to import, open the wallet in Electrum (otherwise, create a new wallet). Go to `Wallet>Information` and copy the Master Public Key of cosigner 1. In the config.cfg-file, we are going to change the row
```
# multisig_wallet = 2 xpub……
```
Start by removing `#` (otherwise it’s treated as a comment and skipped by the application). If you are using a 2 of 3 multi-sig, keep `2` (required-signatures). Remove the two example keys and paste cosigner 1s key. Go back to Electrum, copy the key for cosigner 2 and paste after cosigner 1s key (on the same row) and go back to Electrum and copy and paste the key for cosigner 3. Your row should look like this (but with your 3 keys):
```
multisig_wallet = 2 xpub661MyMwA... xpub6AMQ6ZPNa6... xpub6A2po6ffdf...
```

You can change the name “multisig_wallet” if you like.

*Note:* This is storing your master public keys in cleartext on your computer. A malicious actor could get hold of this and from that derive all of your bitcoin addresses (your funds are not at risk because of this).

#### Single wallet

If you want to add more wallets, or create a new single wallet, for example with one key from a hardware wallet. Follow the same procedure. Open the wallet or connect the hardware wallet and create an existing wallet in Electrum. Go to Wallet>Information and copy the Master Public Key. Pick a name and paste it to the config.cfg file. 
For example:
```
Hw_wallet1 = xpubkg4QUp5XpUdNf2uGXvQmnD4zcofZ1MN6Fo8PjqQ…
```
#### Rest of the config.cfg file

If you’ve moved your Bitcoin data directory (where your blocks and chainstate are stored) you need to add that directory to the line `datadir` (you might need to add this even if you use the default location, default locations can be found here https://en.bitcoin.it/wiki/Data_directory). For example:
```
datadir = D:\Bitcoin
```
You can use the default RPC-verification for Bitcoin Core. In that case Bitcoin Core creates a cookie file for you and you don't have to add anything else to config.cfg

Another alternative is to use a `rpcuser` and a strong (many random chracters) `rpcpassword` with Bitcoin Core. This can be necessary for applications like the lightning network to work. If you are using this you'll need to add this to `config.cfg` as well. Uncomment (remove `#`) the two lines `rpc_user` and `rpc_password` and add your information. If you don't have a user and a password for Bitcoin Core yet, you can create that here and transfer it to Bitcoin Core later.

#### Change the bitcoin.conf file

We need to add the line `server=1` to our Bitcoin configuration file for Bitcoin Core to accepts connections from Electrum Personal Server. If you are unsure if you have a configuration file or not, open Bitcoin Core and go to `Settings>Options` and select `Open Configuration File` on the main tab. That should either create a new file in the right directory or open your existing file.

Make sure to add:
```
server=1
```
to a new line.

If you use a rpcuser and rpcpassword add this to new lines as well. The file should in that case look like this:
```
server =1
rpcuser=your_user
rpcpassword=your_password
```
## Install with Python

We need Python3 to install the server. Check if it’s installed by going back to Powershell.
Type in :

`> python --version`

If it gives an error, try

`> py --version`

*Note:* `Py` is the Windows Python Launcher and can in some situation work when `python` doesn’t. But try to use `python` and if only `py` works change python to py in the following examples.

If Python 3 (not Python 2.7) is installed, it should give an output with the version like `Python 3.7.0`. Otherwise go to https://www.python.org/downloads/ and download and install the latest version.

We are going to use `pip` to install the personal server. It should be installed with Python, but make sure you have the latest version by running this in powershell:

`> python -m pip install -U pip`

When it’s done, run the following (and make sure to change the path to where you unzipped the file):

`> python -m pip install --user C:\Users\User1\Downloads\electrum-personal-server-eps-v0.1.6`

You should now have the two scripts, `electrum-personal-server.exe` and `electrum-personal-server-rescan.exe` in a Python folder in the `%Appdata` location (that’s usually a hidden folder and that’s why we need to show hidden items). 

To make sure that everything worked, open a new folder and navigate to the location. If you used Python 3.7, the location should be something like:

`C:\Users\User1\AppData\Roaming\Python\Python37\Scripts`

Copy the full path to the file `electrum-personal-server.exe`.

*Hint*, right click on the file, select properties, change to the “Security” tab and copy the full path in “Object Name”. 

*Troubleshooting:* If you are getting errors or can't find the scripts, make sure you have the latest version of Python and Pip installed.

## Automate the start of the server

To make life easier, we’re going to create a `.bat` file to automate the start of the server. On your desktop, or in any folder of your choice, right click in a blank area and select `New>Text Document`.

Open the Text Document you created and paste the path to `electrum-personal-server.exe`, keep the document open. Navigate to the folder you unzipped earlier and copy the path to the `config.cfg` file. 

Paste the path to `config.cfg` after the path to `electrum-personal-server.exe`. For example:
```
"C:\Users\User1\AppData\Roaming\Python\Python37\Scripts\electrum-personal-server.exe" "C:\Users\User1\Downloads\electrum-personal-server-eps-v0.1.6\config.cfg"
```
If your path has spaces in it, make sure you add `" "`to your path.

Rename the new text document to `Electrum-Personal-Server.bat` (make sure to change .txt to .bat). You’ll get a warning about changing the file name extension, select Yes.

Run `Electrum-Personal-Server.bat` by double clicking on it. Electrum Server should now start and import addresses from the master public keys you defined in config.cfg as watch only addresses in your Bitcoin Core node. Wait for the importing to finish. 

### Troubleshooting 1

If the terminal `cmd.exe` starts and quickly exits the server isn’t starting properly. Go to Electrum-Personal-Server.bat, right click and select edit. Add `Pause` to a new line in the file. So, the content is something like:
```
"C:\Users\User1\AppData\Roaming\Python\Python37\Scripts\electrum-personal-server.exe" "C:\Users\User1\Downloads\electrum-personal-server-eps-v0.1.6\config.cfg"
pause 
```
Save, exit and run again. This should leave cmd.exe open to read any error messages when you run the .bat file. Another solution is to check the log file that’s located in `C:\Users\User1\AppData\Local\Temp\electrumpersonalserver.log` for error messages. If you get a error message like:
```
WARNING:2019-02-27 09:32:22,102: Unable to find .cookie file, try setting `datadir` config
```

You need to set a `rpc_user` and a `rpc_password` or change `datadir` to the correct path.

If the server starts but you get a `JSON-error`, your rpc_user and/or rpc_password is probably wrong. Check your configuration files and check so you don't have multiple -config files (in the default location and in the new location if you moved the installation). You can also try to change the authentication method. If you use rpcuser and rpcpassword try the cookie method or the other way around.

## Start the server

Once the importing is done Electrum Server will exit. If you want to import old transactions, you need to rescan the Bitcoin blockchain. You can do this by making a copy of `Electrum-Personal-Server.bat` rename the copy to `Electrum-Personal-Server-Rescan.bat` , right click on the new file and select edit. Change `electrum-personal-server.exe` to `electrum-personal-server-rescan.exe`. So, the line is something like:
```
C:\Users\User1\AppData\Roaming\Python\Python37\Scripts\electrum-personal-server-rescan.exe C:\Users\User1\Downloads\electrum-personal-server-eps-v0.1.6\config.cfg
```
Run Electrum-Personal-Server-Rescan.bat and enter a date (in the format DD/MM/YYYY) from where you want to start importing addresses (the further back, the longer time it will take) and hit return. You will get a suggestion of a block height to start from. Enter `y` and hit return. Wait for the rescanning to finish (the server will exit once finished). If you don't do this and open an old wallet, the balance will show 0 (but will show the real balance if you rescan).

Once the rescanning is done, or if you only use new addresses. Run Electrum-Personal-Server.bat again. This will start the server. Wait for this message:
```
Listening for Electrum Wallet ...
```

### Troubleshooting 2

If you get an error with something like:
```
Error with bitcoin json-rpc
```
That means that the server can’t connect to your Bitcoin Core full node. This is likely an issue with one of your conf-files (either `config.cfg` or `bitcoin.conf`). Below is a copy of a standard `config.cfg`-file for Windows 10 where the datadir is changed to D:\Bitcoin. It uses `rpcuser` and `rpcpassword` in `bitcoin.conf` (All comments `#` in this file is removed for readability, can be a good idea to keep those)
```
## Electrum Personal Server configuration file
## Comments start with #

[master-public-keys]
multisig_wallet = 2 xpub661MyMwAqRbcEYS8w7XLSVeEsBXy79zSzH1J8vCdxAZningWLdN3zgtU6LBpB85b3D2yc8sfvZU521AAwdZafEz7mnzBBsz4wKY5e4cp9LB xpub127pc4e5YKw4zsBBznm7zEfaZdwAA125UZvfs8cy2D3b58BpBL6Utgz3NdLWgninZAxdCv8J1HzSz97yXBsEeVSLX7w8SYEcbRqAwMyM9LB xpub7g5pc4e5YKwBL9MyMwAqRbcEYS8w7XLSVeEsBXy79zSzH1J8vCdxAZningWLdN3zgtU6LBpB85b3D2yc8sfvZU521AAwdZafEz7mnzBBsz4wKY5e4cp9LB
[watch-only-addresses]

[bitcoin-rpc]
host = 127.0.0.1
port = 8332
datadir = D:\Bitcoin
rpc_user = user
rpc_password = password

wallet_filename =
poll_interval_listening = 30
poll_interval_connected = 5
initial_import_count = 1000
gap_limit = 25

[electrum-server]
host = 127.0.0.1 
port = 50002
ip_whitelist = *
certfile = certs/cert.crt
keyfile = certs/cert.key
```
And what needs to be in `bitcoin.conf` (you can have other settings as well, this is what’s important for Electrum personal server):
```
server=1
rpcuser=user
rpcpassword=password
```
You need to restart Bitcoin Core for changes in `bitcoin.conf` to have effect.

If you get the following error:
```
OSError: [WinError 10013] An attempt was made to access a socket in a way forbidden by its access permissions
```
The risk is that some other service is using a port you are trying to connect to.
Try another port for electrum server by changing the port for "electrum-server" in `config.cfg` file like:
```
[electrum-server]
host = 127.0.0.1 
port = 8000
```
Make sure to take use port lower then 40 000. Risk is that a higher port can be used by another service. Run Electrum-Personal-Server.bat again 


## Setting up Electrum
Now we only need to tell Electrum to listen to our server!

Start Electrum and open a wallet. `Select Tools>Network`

Uncheck Select server automatically and change `Server` to `localhost`:

![Eps Win4](images/63_eps-w_4.png)

If you changed port `50002` in `config.cfg` make sure to change to the same port here. 

If you use Electrum over Tor you have to disable this (no need to connect to your own server over Tor). Change tab to "Proxy" and uncheck "Use Tor":

![Eps Win7](images/63_eps-w_7.png)

Close the dialaog once finished.

It's still a good idea to use Tor, but you'll have to do it with your Bitcoin Core node now. Check out the guide for [running Bitcoin Core over Tor](https://github.com/HelgeHunding/guides/blob/master/hodl-guide/hodl-guide_61_bitcoin-core.md#running-bitcoin-core-over-tor)

*Pro tip:* Create a shortcut that disables all connections to any other server. In that case you don’t risk connecting to a public server by mistake. If you don’t have a shortcut to Electrum on your desktop or in a folder. Navigate to the folder where Electrum is located, standard is `"C:\Program Files (x86)\Electrum`. Right click on the `.exe` file, for example `electrum-3.1.3.exe`. Select Create Shortcut. You’ll get the following message:

![Eps Win5](images/63_eps-w_5.png)

Select Yes

Navigate to the desktop and right click on the shortcut. Select `properties`. In `Target` add the following to the end of the line:

`--oneserver --server localhost:50002:s`

So, the whole line is something like:

`C:\Program Files (x86)\Electrum\electrum-3.1.3.exe" --oneserver --server localhost:50002:s`

If you’ve changed the port from `50002` in `config.cfg`, make sure to change to the same port here. Use the shortcut to start Electrum (and make sure to only use this shortcut to start it)

Your wallet should now be connected to your bitcoin full node (the circle in the bottom right corner should be green)! 

![Eps Win6](images/63_eps-w_6.png)


------

<< Back: [Bonus guides](hodl-guide_60_bonus.md) 
