[ [Intro](README.md) ] -- [ [Preparations]( hodl-guide_10_preparations.md) ] -- [ [First Seeds](hodl-guide_20_first-seeds.md) ] -- [ [Last Seed](hodl-guide_30_last-seed.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Storage](hodl-guide_50_storage.md
) ] -- [ **Bonus** ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

# Wasabi Wallet

Wasabi Wallet is a bitcoin wallet that you can use to mix your bitcoin with other users. Unlike many other mixers, you control your own bitcoin during the whole process. This is important to keep your privacy. It’s extra crucial if you bought your bitcoin on an exchange with KYC. The nature of the open blockchain makes it easy to track bitcoin. If you buy bitcoin on a exchange and doesn’t mix the coins, it’s like have your name and address attached to all your addresses. You can never know who has that information. The heuristic that’s used to track coins can be broken by combining your transaction with other people.
It's usually called "Coinjoin" and is a technique used by Wasabi Wallet.

To download and install the wallet, go to https://www.wasabiwallet.io/ and download the latest version for your OS. If you use Tor, use this address http://wasabiukrxmkdgve5kynjztuovbg43uxcbcxn6y2okcrsg7gb6jdmbad.onion/
Make sure that you download the detached signature as well so we can verify the download.
To verify the signature, you need GNUPgp and the signing key from nopara73.
If you don’t have GNUPgp, you can find a guide and some basic instructions [Here]( https://github.com/HelgeHunding/guides/blob/master/hodl-guide/hodl-guide_10_preparations.md#first-steps). 

You can find nopara73’s key on https://github.com/zkSNACKs/WalletWasabi/blob/master/PGP.txt. Click Raw and hit Ctrl+S and save the key in the same folder as your downloaded files. 
Open a new terminal window

*Windows*: Open Powershell (search for it or use Win+R, type powershell and hit enter)

*macOs*: Click the Searchlight (magnifying glass) icon in the menu bar and type terminal. Select the Terminal application from the search results.

*Linux*: Varies, on Ubuntu, press Ctrl+Alt+T

Change the current directory to the one where the 3 downloaded files are located, for example:

*Windows*  `> cd C:\Users\Downloads`

*macOS and Linux* `$ cd $HOME/Downloads`

Import PGP.txt to your local GPG installation:

`$ gpg --import pgp.txt`

Now use the “detached signature” (.asc) to check that the installation file you downloaded was signed with the signing key we imported (change the name of the files if you use a different version):

`$ gpg --verify Wasabi-1.1.1.msi.asc Wasabi-1.1.1.msi`

Make sure to change the names so they match the once you downloaded.
The expected should be something like:
```
gpg: Signature made 02/12/19 10:44:50 W. Europe Standard Time
gpg:                using RSA key 21D7CA45565DBCCEBE45115DB4B72266C47E075E
gpg: conversion from 'utf-8' to 'CP437' failed: Illegal byte sequence
gpg: Good signature from "Fics≤r ┴dßm <adam.ficsor73@gmail.com>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 21D7 CA45 565D BCCE BE45 115D B4B7 2266 C47E 075E
```
We can see that the signature was made close to the release (by checking the date) and that it´s a `Good signature`. The fingerprint matches the one written on https://github.com/zkSNACKs/WalletWasabi/blob/master/WalletWasabi.Documentation/Guides/InstallInstructions.md#gpg-verification

We can go ahead and install Wasabi Wallet.

Once finished, run Wasabi Wallet. Generate a new wallet according to the instructions on screen. Remember, this is a hot wallet. Never put to much bitcoin in a hot wallet.

Open your wallet and change tab to CoinJoin:

![Wasabi 1](images/62_wasabi_1.png)

When you deposit funds to Wasabi Wallet, you’ll see the unspent outputs that you can queue for mixing here. 
Select the outputs you want to mix, enter your password and Click `Enqueue Selected Coins`.
Anonymity set means how many other outputs of the same amount you mix our coins with (if 50 people participate in the coinjoin, the anonymity set is 50). The lowest amount available to mix right now is 0,1 bitcoin. If you mix larger amounts, the change will be mixed as well and improve your anonymity set. 

Depending on how much you mix and what anonymity set you settle for, you´ll end up with a lot of smaller outputs. If you deposit 1 bitcoin and mix to the smallest denominator, you’ll end up with 10 0,1 bitcoin outputs. We need a best practice for how to handle this.

## Best practise to handle mixed outputs

This is based on the discussion at https://www.reddit.com/r/WasabiWallet/comments/avxbjy/combining_mixed_coins_privacy_megathread/

It’s targeted for how to handle transfers to cold storage. You can safely transfer bitcoin from WasabiWallet to your cold storage. WasabiWallet doesn’t use your full node but automatically use Tor and a version of Neutrino that makes it a lot better for privacy then most other light wallets.

But you don’t want to transfer all your bitcoin in the same transaction. The key is to be unpredictable. Chain analysis is looking for patterns. If you deposit 1 bitcoin and mix it and then combine all the outputs and transfer 1 bitcoin out, you can make the assumption that it’s the same bitcoin and the mixing is wasted. The best practise is based on an environment with low transaction fees.

* Be unpredictable. If you have 5 bitcoins, deposit it in uneven chunks (and don’t put 5 bitcoins in a hot wallet). For example, start by depositing 1 bitcoin, then 0,7 then 1,2 and so on. Do the transactions at different times during the day. This can seem like a lot of work. But, if you do the mixing well, this is the only time you have to do it. If you do it poorly, you might have to go back later and do it again. 
* Aim for an anonymity set of at least 50. This’ll be visible at each separate output in Wasabi Wallet.
* If you’ve mixed 5 bitcoins then you might end up with 50 outputs of 0,1 bitcoin. If you were going to transfer all out individually, you’d have to do 50 different transactions and would end up with a lot of different addresses. Is it safe to combine some of the outputs when withdrawing? Again, the key is unpredictability. You can probably combine up to 5-10 outputs of 0,1 bitcoin without reducing your privacy. Make sure you change your behaviour (sometimes transfer 0,3 bitcoin, next time 0,5 and so on). Do the transfers at different times during the day and never send to any old addresses you control. 
* *Advanced:* If you mix some of your outputs more the once it will sort of grow your anonymity set exponentially and make tracking much harder. This won’t cost much and makes you more unpredictable. The easiest solution is to change the `config.json` file. The default location is on *Windows* `C:\Users\{User}\AppData\Roaming\WalletWasabi\Client\Config.json` and on *Linux/macOS* `~/.walletwasabi`. Open the file with a text editor and change the line `MixUntilAnonymitySet` from `50` to a number of `100` or more. To be even more unpredictable, change this number from time to time. Restart Wasabi Wallet for the new changes to effect.

------

<< Back: [Bonus guides](hodl-guide_60_bonus.md) 
