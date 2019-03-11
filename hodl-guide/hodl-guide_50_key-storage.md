[ [Intro](README.md) ] -- [ [Preparations]( hodl-guide_10_preparations.md) ] -- [ [First Keys] ](hodl-guide_20_first-keys.md) -- [ [Last Key] ](hodl-guide_30_last-key.md) -- [ [Multi-Sig Wallet](hodl-guide_40_multi-sig.md) ] -- [ **Key Storage** ] -- [ [Bonus](hodl-guide_60_bonus.md) ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

# Store your keys

You should now have the following information:
* **Package 1:**
  * `Private key 1`
  * `Information package A` containing `PIN_A: pin_hw_a` and `MPK3: master_pub_key_3`
* **Package 2:**
  * `Private key 2`
  * `Information package B` containing `PWA: your_password_A` and `PIN_B: pin_hw_b`
* **Package 3:**
  * `Private key 3`
  * `Information package C` containing `PWB: your_password_B` and `MPK2: master_pub_key_2`
* **4:**
  * `Hardware Wallet A` (containing private key 1)  
* **5:**
  * `Hardware Wallet B` (containing private key 2)
* **6:**
  * `Secure note` containing: 
  ```
  PWA: your_password_A
  PWB: your_password_B
  MPK1: master_pub_key_1
  MPK2: master_pub_key_2
  MPK3: master_pub_key_3
  ```
Since you’ve duplicated two of your private keys, this is almost like a 2 of 5 signature scheme (not exactly since you could lose two of the same keys). This means that you could lose 2-3 pieces and still be able to restore your funds. So how should you handle this information? One option is to make the funds unavailible to access from one place only. Then you'd need to store the packages at five locations. We are going with a more flexible setup in our base case.

Base case for storage:
**1.**	Private Key 1 and information package A at someone you trust (this package is a little bit more important then the other two). 
**2.**	Private Key 2 and information package B at someone else you trust or in a different location then your home. 
**3.**	Private Key 3 and information package C in a vault or a safe deposit box at a bank or at a speicialized company. 
**4.**	Hardware Wallet A and Hardware Wallet B in your home (preferably in a safe). The hardware wallets can be used to check addresses when you deposit funds to the storage. It also gives you the possibility to spend your bitcoin. 
**5.** Secure note, encrypted and stored on a server you can access away from your home or on a USB stored in another location then your home.

You can of course modify this to fit your situation (only use persons you trust, only use vaults etc). But you shouldn't store the private keys in the same building or store more then your two hardware wallets at home.

This is a solid setup. The persons you trust can’t access your funds or even see your balance. You can control your funds from your home. If one hardware wallet breaks, you only need one other key to access your funds. If someone steals your hardware wallets, they would still need both of your PINs and the master public key for the last key to spend anything. The keys stored in other locations needs to be combined with 2 other keys to spend. So, a malicious actor would need all 3 private keys or 2 keys and your hardware wallets to to access your funds.   

If you are giving your keys to another person. Try to deliver them yourself, never put anything in an e-mail. In the worst case, mail the keys one at a time with snail mail and make sure the keys are delivered. Tell the other person what it is and who they need to contact in case of an emergency were they need to access the funds.

It’s a good idea to store everything in envelopes and seal with tape (so you notice if it’s been open). Avoid writing “Bitcoin” or something on the envelopes, they should look as normal as possible. Control your keys from time to time (like once a year), move to a new multi-sig if one of the keys are lost or compromised.

Finish up by sealing the USB you used for Tails with tape (so you don't use it for something else) and if you used an eternally quarantined computer, put a tape on the ethernet-port and mark it so you or, someone else, don't use it by accident.

Everything is now set to start to HODL with a peace of mind!

## Worst case scenarios

So, what are the worst case scenarious? How vulnerable are you to teft or loss and how are your trusted persons going to access your funds in case of an emergency?

Your funds are most vulnerable to "the $5 wrench attack". That means, if someone breaks into your house and threatens you until you give them your bitcoins. This is why

![First Rule](images/50_first_rule.png)

Feel free to talk about Bitcoin, but never talk about how much bitcoin you own (that's not very classy anyways). That's the best defence against this type of attack. Even if you couldn't access your funds from your home, an attacker could hold you hostage until you pay. You could use multiple wallets and different PINs on your hardware wallets to reduce the risk of losing your main stash in an attack.

Another bad case is if your computer is compromised. If an attacker got access to your secure note or your wallet file in Electrum, they would be able to derive all your addresses. If they had this access, it's very possible that they could be able to get your name and address as well. If this attacker attact you in your home, multiple wallets wouldn't help since the attacker would know how much you owned. We do what we can to reduce this risk. If you use Tor and/or your full node you reduce the risk compared to giving remote servers your private information. But it's still a risk that we need to acknowledge. As long as the harware wallets are secure and your private key was generated properly in Tails, your funds aren't at risk only because someone compromises your computer. They would need to physically extort you. 

If the people you trust with your keys was going to collude against you, they would need all 3 keys. If the ones holding key 1 and 2 tried to spend they wouldn't have password B. If 1 and 3 tried they wouldn't have password A and if 2 and 3 tried they wouldn't have the public key for key 1 (needed to constuct the multi-sig).

What if someone needed to access your funds in case you are hospitalized or worse?

The worst case would be if your house burned down and you and your hardware wallets with it. All three keys stored in other places would then be needed to access your funds. 

If you are hospitalized or die and a trusted person needs to access your funds, access to package 1 is needed. If we assume that the person can get access to your hardware wallets (drill the safe or whatever is needed). The person can combine with either package 2 and the hardware wallets or package 3 and the hardware wallets. They can of course combine it with package 2 and 3 and get access as well.

What about loss of keys?

If your house burns down with your hardware wallets in it, but you survive, you can construct the multi-sig wallet with your secure note and any 2 of the private keys.

If your computer crashes and you lose access to your electrum wallet file and you somehowe lose your secure note, you can reconstruct the wallet with your hardware wallets and package 1 or 3.

---

For more improvments check out: [Bonus >>](hodl-guide_60_bonus.md)
