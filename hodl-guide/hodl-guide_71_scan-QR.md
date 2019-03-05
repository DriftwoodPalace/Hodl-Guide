[ [Intro](README.md) ] -- [ [Preparations](raspibolt_10_preparations.md) ] -- [ [The First Keys] ](hodl-guide_20_first-keys.md) -- [ [The Last Key] ](hodl-guide_30_last-key.md) -- [ Multi-Sig Wallet ] -- [ [Bonus](raspibolt_60_bonus.md) ] -- [ **Troubleshooting** ]

---

# Scan QR-code with Electrum

If you try to scan a QR-code with Electrum and get the following error:

![Error 1](images/40_error_1.png)

You’ll probably need to install “Zbar” (or launch it if it’s installed). It’s available at http://zbar.sourceforge.net/ and you can view the source code at https://github.com/ZBar/ZBar. (Only availble on Windows and Linux, on Mac scroll down to other solutions). It’s generally a good idea to not download random programs from file hosting sites. But Zbar has been around a long time and we can try to ensure it’s a legit copy. If you still don’t want to use Zbar, scroll down to “other solutions”- Otherwise go to https://sourceforge.net/projects/zbar/files/zbar/0.10/. Make sure that “Modified” is 2009-10-XX:

![Zbar](images/40_zbar.png)

Download the file for your operating system (.exe for Windows and tar.gz or tar.bz2 for Linux). No digital signatures are provided, so we are going to generate the SHA256-checksum of the file. Open a new terminal and change the directory to where the file is located:

`$ cd $HOME/Downloads` 
Generate the checksum:
*on Windows* `> Get-FileHash -a sha256 zbar-0.10-setup.exe`
You should get the following output: 
![Zbar hash](images/40_zbar_hash.png)
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

![Zbarcam](images/40_zbarcam.png)

Scan the QR-code in Electrum. It should read your xpub key and Electrum should automatically show it. 

Other solutions:
If you can’t launch or don’t want to use Zbar, you could use a workaround. 

Option 1 is to simply download another QR-reader on your computer (or check if you have one installed) and scan the QR-code. Copy the scanned result to Electrum. 

Option 2, use a QR-code reader on your smart-phone. Load the photo to the QR-code reader, connect to internet and send the text to your computer with a secure messaging app. 

Option 3, use an online-service like https://webqr.com/index.html. Know that you risk to leak your public key to a third party (which reduces your privacy but isn’t terrible in this case since it’s only 1 of 3 needed keys). Copy the result to Electrum.


------

<< Back: [Create multi-sig wallet](https://github.com/HelgeHunding/guides/blob/master/hodl-guide/hodl-guide_40_multi-sig.md#create-the-multi-sig-wallet) 
