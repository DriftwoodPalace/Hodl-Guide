[ [Intro](README.md) ] -- [ [Preparations]( hodl-guide_10_preparations.md) ] -- [ [First Keys](hodl-guide_20_first-keys.md) ] -- [ [Last Key](hodl-guide_30_last-key.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Key storage](hodl-guide_50_key-storage.md
) ] -- [ **Bonus** ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

# Electrum Personal Server on Windows 10

*Difficulty: medium*

Electrum Personal Server will connect your Bitcoin full node to Electrum. This will make it possible to use all functionality in Electrum with your full node (Hardware Wallet support, easy multi-sig setup and more). 

Before starting, make sure you’ve got a Bitcoin Core full node running and up to sync. If don’t, see [Install and optimize Bitcoin Core](hodl-guide_61_bitcoin-core.md).

You also need Electrum https://electrum.org/#download (you should check the digital signatures before installing, more info on how [Here](https://github.com/HelgeHunding/guides/blob/master/hodl-guide/hodl-guide_40_multi-sig.md#download-and-verify-electrum))

## Download the installation package

Go to https://github.com/chris-belcher/electrum-personal-server and read the intro (before How To) to know what this is and why it’s important. 
To verify the download, we need Chris Belchers signing-key. It can be found here https://github.com/chris-belcher/electrum-personal-server/blob/master/pgp/pubkeys/belcher.asc

Click “raw”:

![Eps Win1](images/63_eps-w_1.png)

Hit `Ctrl+S` and save the key in a folder on your computer (preferably where you download files to).

To verify the signature, we need Gpg4win. If it’s not already installed, go to https://www.gpg4win.org and install the latest release for Windows. We need to start a new terminal. Open “Powershell” (search for it or use Win+R, type powershell and hit enter).

We need to change the working directory to the directory where the file is located. Type in the following (everything after `>`), if you placed the file in downloads:

`> cd downloads`

You can also use the whole path:
`> cd C:\Users\User1\Downloads`

Import Belchers signing key to your local directory:

`> gpg --import belcher.asc`

It’s now imported. Navigate to the release page in Github https://github.com/chris-belcher/electrum-personal-server/releases and download the latest `Source code (.zip)` and the corresponding `.asc` file. For example:

![Eps Win2](images/63_eps-w_2.png)

Once downloaded, make sure that the working directory is the one where the files are located. Enter the following command (of you downloaded another version, change the file names)

`> gpg --verify eps-v0.1.6.zip.asc electrum-personal-server-eps-v0.1.6.zip`

The output should be something similar to this:
```
gpg: Signature made 11/15/18 23:30:04 W. Europe Standard Time
gpg:                using RSA key EF734EA677F31129
gpg: Good signature from "Chris Belcher <false@email.com>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 0A8B 038F 5E10 CC27 89BF  CFFF EF73 4EA6 77F3 1129
```

We can see that the signature was made at a date close to the release. It is a good signature. The Primary key fingerprint is the same as on Github. A search online on the fingerprint shows that it surely was signed by Chris Belcher. We can go ahead an unzip the .zip file.

## Change the config-file

Go into the unzipped folder and make a copy of the file config-cfg_sample and rename the copy to config.cfg (You’ll get a warning about changing the file name extension, select Yes). Make sure that you can see file extensions, it can be changed at “View” in the top-bar. While there make sure “hidden items” is checked as well:

![Eps Win3](images/63_eps-w_3.png)

Right click on the file and edit with a text editor (notepad etc). If you are following the cold storage guide or already have an electrum wallet. Open the wallet in Electrum. Go to `Wallet>Information` and copy the Master Public Key of cosigner 1 . In the config.cfg-file, we are going to change the row
```
# multisig_wallet = 2 xpub……
```
Start by removing `#` (otherwise it’s treated as a comment and skipped by the application). If you are using a 2 of 3 multi-sig, change 2 to `3`. Remove the two example keys and paste your first cosigner 1 key. Go back to Electrum, copy the key for cosigner 2 and paste after cosigner 1s key (on the same row) and go back to Electrum and copy and paste the key for cosigner 3. Your row should look like this (but with your 3 keys):
```
multisig_wallet = 3 xpub661MyMwA… pub6AMQ6ZPNa6... xpub6A2po6ffdf…
```

You can change the name “multisig_wallet” if you like.

*Note:* This is storing your master public keys in cleartext on your computer. A malicious actor could get hold of this and derive all of your bitcoin addresses (your funds are not at risk).

If you want to add more wallets, for example with one key from a hardware wallet. Follow the same procedure. Connect the hardware wallet and create or open an existing wallet in Electrum. Go to Wallet>Information and copy the Master Public Key. Pick a name and paste it to the config.cfg file. 
For example:
```
Hw_wallet1 =  xpubkg4QUp5XpUdNf2uGXvQmnD4zcofZ1MN6Fo8PjqQ…
```
If you’ve moved your Bitcoin data directory (where your blocks and chainstate are stored) you need to add that directory to the line “datadir”. For example:
```
datadir = D:\Bitcoin
```
The best solution is to use a strong (many random characters) `rpcuser` and a `rpcpassword` in Bitcoin Core (not the default).  

You need to add this to `config.cfg` as well. Uncomment (remove `#`) the two lines `rpc_user` and `rpc_password` and add your information. 

To use a rpcuser and rpcpassword you need to add this to your bitcoin.conf file. If you are unsure if you’ve set this or not, look in the default location (C:\Users\User1\AppData\Roaming\Bitcoin\bitcoin.conf). If you’ve moved the installation, Bitcoin Core will try to use the .conf file in the new location. Edit the file at that location. The file also needs to contain the line server=1 (to accept connection from other programs). 

If you don’t have a bitcoin.conf file, simple create a .txt file in your data directory (where you store the blocks) and add the information, save and rename the file to `bitcoin.conf` (make sure to change the extension from .txt to conf). So the file should at least contain the following:
```
server =1
rpcuser=your_user
rpcpassword=your_password
```
## Install with Python

Then, we need Python3 to install the server. Check if it’s installed by going back to Powershell.
Type in :

`> python –version`

If it gives an error, try

`> py –version`

*Note:* `Py` is the Windows Python Launcher and can in some situation work when `python` doesn’t. But try to use `python` and if only `py` works change python to py in the following examples.

If Python is installed, it should give an output with the version like Python 3.7.0. Otherwise go to https://www.python.org/downloads/ and download and install the latest version.

We are going to use `pip` to install the personal server. It should be installed with Python, but make sure you have the latest version by running this in powershell:

`> python -m pip install -U pip`


When it’s done, run the following (and make sure to change the path to where you unzipped the file):

`> python -m pip install --user C:\Users\User1\Downloads\electrum-personal-server-eps-v0.1.6`


You should now have the two scripts electrum-personal-server.exe and electrum-personal-server-rescan.exe in a Python folder in the `%Appdata` location (that’s usually a hidden folder and that’s why we need to show hidden items).

To make sure that everything worked, open a new folder and navigate to the location. If you used Python 3.7, the location should be something like:

`C:\Users\User1\AppData\Roaming\Python\Python37\Scripts`

Copy the full path to electrum-personal-server.exe. *Hint*, right click on the file, select properties, change to the “Security” tab and copy the full path in “Object Name”. 

## Automate the starting of the server

To make life easier in the future, we’re going to create a `.bat` file to automate the start of the server. On your desktop or in any folder of your choice, Right click in a blank area, select `New>Text Document`.

Open the Text Document you created and paste the path to `electrum-personal-server.exe`, keep the document open. Navigate to the folder you unzipped earlier and copy the path to the `config.cfg` file (it might be a good idea to move the whole “electrum-personal-server-eps-v0.1.6” folder out of the Downloads folder it you clean that one from time to time). 

Paste the path to `config.cfg` after the path to `electrum-personal-server.exe`. For example
```
C:\Users\User1\AppData\Roaming\Python\Python37\Scripts\electrum-personal-server.exe C:\Users\User1\Downloads\electrum-personal-server-eps-v0.1.6\config.cfg
```
Rename the new text document to `Electrum-Personal-Server.bat` (make sure to change .txt to .bat). You’ll get a warning about changing the file name extension, select Yes.

Run `Electrum-Personal-Server.bat` by double clicking on it. Electrum Server should now start and import addresses as watch only addresses in your Bitcoin Core node. Wait for the importing to finish. This will detect new transactions to addresses derived from your master public keys. 

### Troubleshooting 1

If the terminal `cmd.exe` starts and quickly exits the server isn’t starting properly. Go to the where Electrum-Personal-Server.bat, right click and select edit. Add `Pause` to a new line in the file. So, the content is something like:
```
C:\Users\User1\AppData\Roaming\Python\Python37\Scripts\electrum-personal-server.exe C:\Users\User1\Downloads\electrum-personal-server-eps-v0.1.6\config.cfg
pause 
```
This should leave cmd.exe open to read any error messages when you run the .bat file. If you get a error message like:
```
WARNING:2019-02-27 09:32:22,102: Unable to find .cookie file, try setting `datadir` config
```

You need to set a `rpc_user` and a `rpc_password` or change `datadir` to the correct path.

If the server starts but you get a `JSON-error`, your rpc_user and/or rpc_password is probably wrong. Try to check if you have multiple -config files (in the default location and in the new location if you moved the installation).

## Start the server

Once the importing is done Electrum Server will exit. If you want to import old transactions, you need to rescan the Bitcoin blockchain. You can do this by making a copy of `Electrum-Personal-Server.bat` rename the copy to `Electrum-Personal-Server-Rescan.bat` , right click on the new file and select edit. Change `electrum-personal-server.exe` to `electrum-personal-server-rescan.exe`. So, the line is something like:
```
C:\Users\User1\AppData\Roaming\Python\Python37\Scripts\electrum-personal-server-rescan.exe C:\Users\User1\Downloads\electrum-personal-server-eps-v0.1.6\config.cfg
```
Run Electrum-Personal-Server-Rescan.bat and enter a date (in the format DD/MM/YYYY) from where you want to start importing addresses (the further back, the longer time it will take) and hit return. You will get a suggestion of a block height to start from. Enter y and hit return. Wait for the rescanning to finish (the server will exit once finished).

Once the rescanning is done, or if you only use new addresses. Run Electrum-Personal-Server.bat again. This will start the server. Wait until the message:
```
Listening for Electrum Wallet ... appears.
```

### Troubleshooting 2

If you get an error with something like:
```
Error with bitcoin json-rpc
```
That means that the server can’t connect to your Bitcoin Core full node. This is likely an issue with your conf-file (either in `config.cfg` or in `bitcoin.conf`). Below is a copy of a standard `config.cfg`-file for Windows 10. It uses `rpcuser` and `rpcpassword` in `bitcoin.conf` (All comments `#`” in this file is removed for readability, can be a good idea to keep those)
```
## Electrum Personal Server configuration file
## Comments start with #

[master-public-keys]
multisig_wallet = 3 xpub661MyMwAqRbcEYS8w7XLSVeEsBXy79zSzH1J8vCdxAZningWLdN3zgtU6LBpB85b3D2yc8sfvZU521AAwdZafEz7mnzBBsz4wKY5e4cp9LB xpub127pc4e5YKw4zsBBznm7zEfaZdwAA125UZvfs8cy2D3b58BpBL6Utgz3NdLWgninZAxdCv8J1HzSz97yXBsEeVSLX7w8SYEcbRqAwMyM9LB xpub7g5pc4e5YKwBL9MyMwAqRbcEYS8w7XLSVeEsBXy79zSzH1J8vCdxAZningWLdN3zgtU6LBpB85b3D2yc8sfvZU521AAwdZafEz7mnzBBsz4wKY5e4cp9LB
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
And my `bitcoin.conf` (you can have other settings as well, this is what’s important for Electrum personal server):
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
Chances are that some other service is using a port you are trying to connect to.
Try another port for electrum server by changing the following line in `config.cfg` file like
```
[electrum-server]
host = 127.0.0.1 
port = 8000
```
Make sure to take use port lower then 40 000 since Windows since risk is that a higher port can be used by another service. Run Electrum-Personal-Server.bat again 

To see error messages check the log file that’s located in `C:\Users\User1\AppData\Local\Temp\electrumpersonalserver.log`

## Setting up Electrum
Now we only need to tell Electrum to listen to our server!

Start Electrum and open a wallet. `Select Tool>Network`

Uncheck Select server automatically and change `Server` to `localhost`:

![Eps Win4](images/63_eps-w_4.png)

If you changed port `50002` in `config.cfg` make sure to change to the same port here. Close this dialaog once finished 

*Pro tip:* Create a shortcut that disables all connections to any other server. In that case you don’t risk connecting to a public server by mistake. If you don’t have a shortcut to Electrum on your desktop or in a folder. Navigate to the folder where Electrum is located, standard is `C:\Program Files (x86)\Electrum`. Right click on the `.exe` file, for example `electrum-3.1.3.exe`. Select Create Shortcut. You’ll get the following message:

![Eps Win5](images/63_eps-w_5.png)

Select Yes

Navigate to the desktop and right click on the shortcut. Select `properties`. In `Target` add the following to the end of the line:

`--oneserver --server localhost:50002:s`

So, the whole line is something like:

`C:\Program Files (x86)\Electrum\electrum-3.1.3.exe" --oneserver --server localhost:50002:s`

If you’ve changed the port from `50002` in the conf-file, make sure to change to the same port here. Use the shortcut to start Electrum (and make sure to only use this shortcut to start it)

Your wallet should now be connected to your bitcoin full node (the circle in the bottom right corner should be green)! 

![Eps Win6](images/63_eps-w_6.png)


------

<< Back: [Bonus guides](hodl-guide_60_bonus.md) 
