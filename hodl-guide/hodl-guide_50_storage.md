[ [Intro](README.md) ] -- [ [Preparations]( hodl-guide_10_preparations.md) ] -- [ [First Seeds] ](hodl-guide_20_first-seeds.md) -- [ [Last Seed] ](hodl-guide_30_last-seed.md) -- [ [Multi-Sig Wallet](hodl-guide_40_multi-sig.md) ] -- [ **Storage** ] -- [ [Bonus](hodl-guide_60_bonus.md) ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

# Store your information

You've now created all necessary information. You can add the seeds and the information packages into envelopes (mark them `A`, `B` and `C`) so you have the following setup:

* **Envelope A:**
  * `Seed A`
  * `Information package A` containing `PIN_A: pin_hw_a` and `MPK3: master_pub_key_3`
* **Envelope B:**
  * `Seed B`
  * `Information package B` containing `PFA: your_passphrase_A` and `PIN_B: pin_hw_b`
* **Envelope C:**
  * `Seed C`
  * `Information package C` containing `PFB: your_passphrase_B` and `MPK2: master_pub_key_2`
* **4:**
  * `Hardware Wallet A` (containing seed A)  
* **5:**
  * `Hardware Wallet B` (containing Seed B)
* **6:**
  * `Digital note` containing: 

  ```
  PFA: your_passphrase_A
  PFB: your_passphrase_B
  MPK1: master_pub_key_1
  MPK2: master_pub_key_2
  MPK3: master_pub_key_3
  ```

Since two of your seeds are both on paper and in hardware wallets, this is almost like a 2 of 5 signature scheme. As long as you have your digital note, you can lose 3 pieces and still be able to restore your funds (unless the only 2 pieces left is one hardware wallet and its corresponding seed). So how should you handle this information? One option is to make the funds unavailable to access from one place only. But this isn't our base case. In the base case you'll be able to access the funds from your home by using the two hardware wallets + the digital note.

Base case for storage:

**1.** `Envelope A` (Seed and information package A). Store it with someone you trust. This package is a little bit more important then the other two as it's slightly easier to restore funds with this package.

**2.** `Envelope B` (Seed and information package B). Store it with someone else you trust or in a different location then your home (bank, second location you control etc).

**3.** `Envelope C` (Seed and information package C). Store it in a vault or a safe deposit box at a bank or with a specialized company.

**4.** Hardware Wallet A and Hardware Wallet B in your home (preferably in a safe). This gives you the possibility to spend from your cold storage at any time. You can use it for double checking addresses when depositing to your cold storage as well.

**5.** Digital note, encrypted and stored on a server you can access away from your home. Alternatively stored on your computer with a backup on an USB flash drive stored in another location then your home.

You can of course modify this to fit your situation (only use persons you trust, only use vaults etc). But you shouldn't store any seeds in the same building or store more then your two hardware wallets at home.

This is a solid setup. The persons you trust can’t access your funds or even see your balance. You can control your funds from your home. If one hardware wallet breaks, you only need one other seed to access your funds. If someone steals your hardware wallets, they would still need both of your PINs, the passphrases and the master public key for the last cosigner to spend anything. The packages stored in other locations needs to be combined with 2 other packages to spend anything.

If other people store information for you. Try to deliver the information yourself, never put anything in an e-mail. In the worst case, mail the packages one at a time with snail mail and confirm that they are delivered properly. Tell the persons that are holding the packages what it is and who they need to contact in case of an emergency where they need to access the funds.

If you are using envelopes, seal them with tape (so you'd notice if it’s been open). Avoid writing “Bitcoin” or something on the envelopes, they should look as normal as possible. Move your funds to a new multi-sig wallet if one of the packages gets lost or compromised.

*Optional:* Inspect the packages stored in other locations once a year. Make sure that no seals are broken. If something looks compromised, create a new multi-sig wallet and move your funds.

Finish up by sealing both the USB you used for and with Tails with tape (so you don't use it for something else by accident). If you used an eternally quarantined computer, put a tape on the ethernet-port and mark it so you or, someone else, don't use it by accident.

Everything is now set to start to HODL with a peace of mind!

For guidelines on how to handle deposits, withdrawals and more with Electrum. Check out [Electrum best practises](hodl-guide_67_electrum-bp.md) in the Bonus section.

## Worst case scenarios

So, what are the worst case scenarios? How vulnerable are you to theft or loss and how are your trusted persons going to access your funds in case of an emergency?

### Theft by random attacker

Your funds are most vulnerable to "the $5 wrench attack":

![Wrench](images/50_wrench.png)

*$5 wrench attack by [xkcd](https://xkcd.com/538/)*

Try keeping your bitcoin holdings as secret as possible. Never talk about how much bitcoin you own or how early you bought bitcoin (that's not very classy anyways). That's the best defence against this type of attack. Even if you couldn't access your funds from your home, an attacker could hold you hostage until you pay. You could use multiple wallets and different PINs on your hardware wallets to reduce the risk of losing your main stash in case of an attack.

A truly worst case scenario is if an attacker knows about some, or all, bitcoin you own and attack you. Decoys would then be a useless. That could happen if they got access to all your master public keys and your name or address. It could also happen if you where deanonymized because of bad privacy practises.

For example, if an chain analysis company manages to tie a certain cluster of addresses to your identity. The attacker could be the government that demands that you reveal your addresses for some reason. This risk is reduced a lot if you use your own full node over Tor and follow some best practises when handling funds. Even without all those precautions, it's still an huge improvement compared to status que where a random bank employee can get access to all your financial information with a few clicks.

Important to remember, your funds aren't at risk only because your computer is compromised. As long as one of the hardware wallets do what they are designed to do (not leak the seed) and the last seed was generated properly in Tails, your funds are safe. An attacker would need you to give them access to the funds (physical attack or social engineering).

### Theft by trusted persons

If the people you trust with your information where going to collude against you, they would need all 3 packages to steal anything. If the ones holding package 1 and 2 tried to spend, they wouldn't have passphrase B. If person 1 got access to package 3 she wouldn't have passphrase A and if person 2 had access to package 3 she wouldn't have the public key for cosigner 1 (needed to construct the multi-sig).

### Access in case of an emergency

What if someone needs to access your funds in case you are hospitalized or worse?

The worst case would be if your house burned down and you and your hardware wallets with it. All three packages stored in other places would then be needed to access your funds. The multi-sig contract could be reconstructed by combining all seeds (+ the seed passphrases) or two seeds and the last master public key (in the right order).

*The following information is incorrect, you'll need all packages to restore in this situation, updated guide coming soon.*
*If you are in a coma or die (without your house burning down) and a trusted person needs to access your funds, access to Envelope A is needed. If we assume that the person can get access to your hardware wallets (drill the safe or whatever is needed). The person can combine Envelope A with either Envelope B and the hardware wallets or Envelope C and the hardware wallets. They can of course combine it with Envelope B and C and get access as well.*

What about loss of seeds?

If your house burns down with your hardware wallets in it, but you survive, you can construct the multi-sig wallet with your digital note and two of the seeds.

If your computer crashes and you lose access to your electrum wallet file and you somehow lose your digital note, you can reconstruct the wallet with your hardware wallets (if you remember the PINs) and info packages B and C.

---

For more improvements to the guide check out: [Bonus >>](hodl-guide_60_bonus.md)
