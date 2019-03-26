[ [Intro](README.md) ] -- [ [Preparations](hodl-guide_10_preparations.md) ] -- [ **First Seeds** ] -- [ [Last Seed](hodl-guide_30_last-seed.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Storage](hodl-guide_50_storage.md
) ] -- [ [Bonus](hodl-guide_60_bonus.md) ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

# Generating the first two seeds

Time to generate the first seeds! 

A few things to keep in mind when generating your seeds. This is valuable information. If someone gets access to your seeds, they get access to your funds. A lot of devices are “spying” on us in one way or the other. If possible, generate all seeds in a room where other electronic devices connected to the internet are turned off. Make sure that your actions aren´t visible from windows or doors and that no home security camera records your actions.

Try to keep smartphones turned off and/or in another room during the process. They are hard to secure and can record sound/video without you noticing (computers can of course do the same). Generally, use your common sense to make sure that nothing can record your actions.

## Generate seeds with Hardware Wallets A and B

You should have the following at hand:

* Hardware Wallet A, it doesn't matter which one is Hardware Wallet A. But, select one and remember which one you select.
* Hardware Wallet B from a different manufacturer then Hardware Wallet A.
* 2 notes to write your seeds on (you can use the paper often provided with the wallets).  
* 3 notes to create your information packages. Can be of the same size as the notes you write your seeds on.

Make sure to update the firmware on the hardware wallets if you don't have the latest version. If you have a Ledger and a Trezor, you do this by using Ledger Live or Trezor wallet.

The first two seeds are generated with your two different hardware wallets. This adds extra security. If a fatal flaw was found in one of the wallets, your funds are still safe. You can simply move your funds to a new multi-sig contract and replace the compromised seed.

Follow the setup procedure recommended from each manufacturer. At the end you should end up with one seed from each wallet. Mark the seed from `Hardware Wallet A` with an `A` and the seed from `Hardware Wallet B` with an `B`.

Protect the devices with a pin (use two different pins for the two devices). We are going to write down the pins on information packages later, so use PINs you can remember yourself. The pin is only to protect you if someone gets physical access to the device and isn't super important (but don´t use 0000 as pin because of that..).

We are going to protect the seed in our hardware wallets by encrypting it with a passphrase/password. This adds extra security and gives us more flexibility when we are going to store everything later on.

We humans are pretty terrible at generating random passphrases. So, it’s safer to generate a passphrase with a password manager then trying to come up with one yourself.

You can generate and store the passphrases with a password manager like [LastPass](https://www.lastpass.com/). Or if you don't want to use a third party server, a great open source alternative is [Keepass](https://keepass.info/) where you store everything yourself.. If you are given the option, generate a passphrase without symbols that can be confused (big o and zero etc). If you don't want to use a password manager, you could use an encrypted secure note stored on a USB instead. The important part is that this information should be available if your house burns down. We are referring to this as the `digital note` from now on.

I would recommend a passphrase containing symbols from (0-9, a-z, A-Z) and with a length of at least 15 characters. That would give you a passphrase with ~80-bit entropy (on average, it would require 2^80 guesses to crack the passphrase).
Use two different passphrases for your two different hardware wallets.
If you already have two old hardware wallets with seeds that you’re sure has been setup in a secure manner, you could use those. But make sure they’re protected with a strong passphrase (preferably use a new passphrase for this purpose).

 So, go ahead and generate two different passphrases. `Passphrase A`for `Seed A` and `Passphrase B` for `Seed B`. In your `digital note`, store the passphrases like this:

```
PFA: your_passphrase_A
PFB: your_passphrase_B
```

*Optional:* Depending on your memory, add hints so you can remember the PINs to the digital note.

We will use the passphrases in Electrum later and can leave them for now.

## Create information packages

Before moving on, we are going to create 3 physical information packages on 3 different pieces of paper. If you want more detail on exactly why we are doing this and how they are being used, look at [Storage](hodl-guide_50_storage.md).

On each information package, write a short instruction for how to access the funds. Something like this:

`Hodl Guide Github, multi-sig 2 of 3`

That should give enough information for someone else to do a search online for how to retrieve funds in case of an emergency.

Mark the three info packages `A`, `B` and `C` .

While writing down critical information, make sure to be extra careful with symbols that can be confused (like big o and 0, I and small L, etc). The best solution is to not use them at all.

On `info package A`, write the pin to hardware wallet A `PIN_A: pin_hw_a`.

On `info package B`, write your the passphrase for seed A `PFA: your_passphrase_A` and the pin to hardware wallet B `PIN_B: pin_hw_b`.

On `info package C`, write the passphrase for seed B `PFB: your_passphrase_B`

Store all information in a secure way during the rest of the process (don't leave your notes lying around visibly).

---
Next up: [Generate the last seed with Tails >>](hodl-guide_30_last-seed.md)
