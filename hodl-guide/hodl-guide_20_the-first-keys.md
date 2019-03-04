[ [Intro](README.md) ] -- [ [Preparations](raspibolt_10_preparations.md) ] -- [ **The First Keys** ] -- [ [Lightning](raspibolt_40_lnd.md) ] -- [ [Mainnet](raspibolt_50_mainnet.md) ] -- [ [Bonus](raspibolt_60_bonus.md) ] -- [ [Troubleshooting](raspibolt_70_troubleshooting.md) ]

---

# Generating the first two keys

A few things to keep in mind when generating your private keys. This is valuable information and a lot of devices are “spying” on us in one way or the other. If possible, generate all private keys in a room where other electronic devices connected to the internet are turned off. Make sure that your actions aren´t visible from windows or doors and that no home security camera records your actions.

Try to keep smartphones turned off and/or in another room during the process. They are hard to secure and can record sound/video without you noticing(computers can of course do the same). Generally, use your common sense to make sure that no one can record your actions.

### Generate keys with Hardware Wallets A and B

The first two keys are generated with your two hardware wallets. Make sure that the hardware wallets are from two different manufacturers. In that case, if a fatal flaw is found in one of the wallets, your funds are still safe. You could simply move your funds to a new multi-sig contract and replace the flawed key. 


Follow the setup procedure recommended from each manufacturer. Protect the devices with a pin that you can remember (use two different pins for the two devices) and use a passphrase with your hardware wallet. 

The method for how to use a passphrase is different for each manufacturer, check their guides. Most vulnerabilities that’s been detected in hardware wallets would’ve been stopped with a passphrase. We humans are pretty terrible at generating random passwords. So, it’s probably safer to use a password generator on your computer then trying to come up with a password yourself. You could use Lastpass, KeypassX or a similar service. A password manager is a great place to store moderately sensitive information in (like public keys and even more sensitive information like the password that protects the seed, but never put your seed on a "hot" computer). If you are given the possibility use a password without symbols that can be confused (big o and zero etc)


I would recommend a password containing symbols from (0-9, a-z, A-Z) and with a length of at least 15 characters. That would give you a password with ~80-bit entropy (on average, it would require 2^80 guesses to crack the password). 
Use two different passphrases for your two different hardware wallets. 
If you already have two old hardware wallets with seeds that you’re sure has been setup in a secure manner, you could use those. But make sure they’re protected with a strong passphrase (preferably use a new passphrase for this setup). 

We are calling the first Hardware wallet, Hardware wallet A (protected with passphrase A) and the second one Hardware wallet B (protected with passphrase B)

Apart from the private keys, we are going to create 3 different information packages on a different piece of paper (if you don’t use a password manager you need 4 info packages). If you want more detail on exactly why, look at [Store your keys]. 

On each information package, write a short instruction for how to access the funds, someting like this:

`Hodlers guide to cold storage, multi-sig 2 of 3`

That should give enough information to do a search online for how to retrieve funds in case of an emergency.

If you are using 4 infp packages, mark the first one `A`.
The other info packages should be marked `B`, `D` (not C) and `E` (you don’t need package `A` if you use a password manager).

If using, on `info package A`, write `your_password_A` and `your_password_B`

On `info package B`, write `Key 2`

On `info package D`, write `Key 2`, `your_password_B` and the pin to hardware wallet B `PIN_B`.

Make sure to be extra careful with symbols that can be confused (like big o and 0, I and small L, etc).

On `info package E` write `Key 3`, `your_password_A` and the pin to hardware wallet A `PIN_B`.

You should now have:
* Hardware wallet A and its private key (that we are calling private key 2, we are creating private key 1 in Tails later)
* Hardware wallet B and its private key (private key 3)
* Info package “B”, “D” and “E”
* A secure note,or similar in a password manager, containing your_password_A and your_password_B (never put anything else from your seed on a computer connected to internet). Or Info package "A"

Store all information in a secure way during the rest of the process (don't leave your notes lying around visibly).

---
Next up: [Last key >>](hodl-guide_40_last-key.md)


