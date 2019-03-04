[ **Intro** ] -- [ [Preparations](raspibolt_10_preparations.md) ] -- [ [Raspberry Pi](raspibolt_20_pi.md) ] -- [ [Bitcoin](raspibolt_30_bitcoin.md) ] -- [ [Lightning](raspibolt_40_lnd.md) ] -- [ [Mainnet](raspibolt_50_mainnet.md) ] -- [ [Bonus](raspibolt_60_bonus.md) ] -- [ [Troubleshooting](raspibolt_70_troubleshooting.md) ]

---
# The Hodler’s Guide to Cold Storage
---

Bitcoin gives you the possibility to store value in ways earlier generations only could dream about. A common man can have a more secure storage then any king throughout history. If done right, no one even needs to know what you own.

I wrote this guide in my own quest to becoming a first-class Bitcoin citizen. A first-class Bitcoin citizen has control of his own keys, runs his own full node to validate all transactions and does this in a secure and private way. I’m no technical expert myself, so this guide only uses tools that’s been properly battletested throughout the years. The goal of the guide is to find a great middle ground in the constant battle between usability and security. More bitcoin has probably been lost because of a complicated process with paper wallets then has been stolen. This guide uses HD-wallets with mnemonic seeds (12-24 regular English words) for your private keys that reduce the risk of fatal mistakes.

The guide is for everyone (you don’t need any technical knowledge) but you should have a basic understanding of what a private key is and why it´s important to store it in a secure way. The guide is flexible and can be utilized in different ways. The full setup is with two different hardware wallets and one backup key created with the Tails operating system. The most time consuming (and most technical) part is related to Tails. You could skip that part for an easier (but less secure) setup. If you don’t trust, or want to buy, hardware wallets you could do the whole setup with 3 keys in Tails. The guide will describe the full setup. The time for the full setup should be 2-3 hours, excluding download and sync-times.  

The guide focusses a lot on privacy as well. Again, those parts are optional (but recommended). They don’t directly affect the security of your private keys. But they reduce the risk of being the victim of a targeted attack (virtual or physical). Those parts are marked with a [P]. Privacy isn’t black and white, so at least try a few of the methods. It’ll probably payoff in the long run. The best security for your bitcoin is probably that no one knows you own them in the first place.

At the end of the guide, you’ll have a set of private keys and a plan to store those in a secure way. That includes the possibility to access them for trusted loved ones in case you’re suddenly hospitalized or worse.

Remember, this is Cold Storage. That means that you shouldn’t be able to access your funds from one place. It should be inconvenient for you (and anyone else) to spend the funds. Only put funds that you don’t need to access frequently in cold storage. If you have more then a few $1000 worth of bitcoin a good starting point could be to store 70-90% in cold storage, 10-30% in a hardware wallet and 0-10% in a hot wallet on your phone or computer (lightning etc). 

I or no one else is responsible for your funds, this guide hopefully gives you a great foundation. But only you are responsible for your bitcoin. Grow a spine and start loving it!

For more reading on private keys and other approaches for cold storage, see 
https://github.com/rustyrussell/bitcoin-storage-guide
or for even more depth, take a look at
https://glacierprotocol.org/
