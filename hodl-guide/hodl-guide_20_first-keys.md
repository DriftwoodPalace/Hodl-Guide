[ [Intro](README.md) ] -- [ [Preparations](hodl-guide_10_preparations.md) ] -- [ **First Seeds** ] -- [ [Last Seed](hodl-guide_30_last-key.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Storage](hodl-guide_50_key-storage.md
) ] -- [ [Bonus](hodl-guide_60_bonus.md) ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

# Generating the first two seeds

Time to generate the first seeds! 

A few things to keep in mind when generating your seeds. This is valuable information. If someone gets access to your seeds, they get access to your funds. A lot of devices are “spying” on us in one way or the other. If possible, generate all seeds in a room where other electronic devices connected to the internet are turned off. Make sure that your actions aren´t visible from windows or doors and that no home security camera records your actions.

Try to keep smartphones turned off and/or in another room during the process. They are hard to secure and can record sound/video without you noticing (computers can of course do the same). Generally, use your common sense to make sure that nothing can record your actions.

## Generate seeds with Hardware Wallets A and B

The first two seeds are generated with your two different hardware wallets. Make sure that the hardware wallets are from two different manufacturers. In that case, if a fatal flaw is found in one of the wallets, your funds are still safe. You can simply move your funds to a new multi-sig contract and replace the compromised seed. 

Follow the setup procedure recommended from each manufacturer. Protect the devices with a pin (use two different pins for the two devices). We are going to write down the pins on information packages later. The pin is only to protect you if someone gets physical access to the device and isn't super important (but don´t use 0000 as pin because of that..). Use PINs you can remember yourself.

Update the firmware on the hardware wallets if you don't have the latest version. 

We are going to protect the seed in our hardware wallets with different passwords/passphrases.
The method for how to use a password with your seed is different for each manufacturer, check their guides (for example [Ledger](https://support.ledger.com/hc/en-us/articles/115005214529-Advanced-passphrase-security)). On Ledger it needs to be setup on the device (you can use a temporary passphrase since we wont use it much) and with Trezor you can do it in Electrum later. You don't need to set it up on the devices now, generate the passwords now and put it into the devices when we construct the multi-sig wallet.

Most vulnerabilities that’s been detected in hardware wallets would’ve been stopped with a strong password. We humans are pretty terrible at generating random passwords. So, it’s probably safer to generate a password with a password manager on your computer then trying to come up with a password yourself. You could use Lastpass, KeypassX or a similar service. A password manager is a great place to store moderately sensitive information in (like public keys and even more sensitive information like the password that protects the seed, but never put your seed on a "hot" computer). If you are given the option, generate a password without symbols that can be confused (big o and zero etc). If you don't want to use an online service like Lastpass, you could use an encrypted secure note stored on a USB instead. The important part is that this information should be availible if your house burns down. We are referring to this as the `digital note` from now on.

I would recommend a password containing symbols from (0-9, a-z, A-Z) and with a length of at least 15 characters. That would give you a password with ~80-bit entropy (on average, it would require 2^80 guesses to crack the password). 
Use two different passphrases for your two different hardware wallets. 
If you already have two old hardware wallets with seeds that you’re sure has been setup in a secure manner, you could use those. But make sure they’re protected with a strong passphrase (preferably use a new passphrase for this purpose). 

We are calling the first Hardware wallet, `Hardware wallet A` (used with `password A`) and the second one `Hardware wallet B` (used with `password B`). It doesn't matter which wallet is which, but make sure to keep track of what you select so you don't mix them later and make sure you know which seed belongs to which wallet (you can mark the seeds with "A" and "B"). In your `digital note`, store the passwords like this:
```
PWA: your_password_A
PWB: your_password_B
```
*Optional:* Depending on your memory (add hints so you can remember the PINs).

## Create information packages

Apart from the seeds, we are going to create 3 physical information packages on a different piece of paper. If you want more detail on exactly why we are doing this and how they are being used, look at [Storage](hodl-guide_50_key-storage.md). 

On each information package, write a short instruction for how to access the funds. Something like this:

`The Hodl Guide Github, multi-sig 2 of 3`

That should give enough information for someone else to do a search online for how to retrieve funds in case of an emergency.

Mark the three info packages `A`, `B` and `C` . 

While writing down critical information, make sure to be extra careful with symbols that can be confused (like big o and 0, I and small L, etc). The best solution is to not use them at all.

On `info package A`, write the pin to hardware wallet A `PIN_A: pin_hw_a`.

On `info package B`, write your first password for the seed `PWA: your_password_A` and the pin to hardware wallet B `PIN_B: pin_hw_b`. 

On `info package C`, write the second password for the seed `PWB: your_password_B`

You should now have:
* `Hardware wallet A` and its seed (`seed A`).
* `Hardware wallet B` and its seed (`seed B`).
* Info package `A`, `B` and `C`.
* A `digital note` in a password manager or on a USB (that´s going to be store in another location), containing `your_password_A` and `your_password_B` (never put anything else from your seed on a computer connected to internet). 

Store all information in a secure way during the rest of the process (don't leave your notes lying around visibly).

---
Next up: [Generate the last seed with Tails >>](hodl-guide_30_last-key.md)


