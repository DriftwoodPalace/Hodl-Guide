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
Since two of your private keys are both on paper and in hardware wallets, this is almost like a 2 of 5 signature scheme. This means that you could lose 3 pieces and still be able to restore your funds (as long as you have your secure note). So how should you handle this information? One option is to make the funds unavailable to access from one place only. Then you'd need to store the packages at five locations. We are going with a more flexible setup in our base case where you always can access your funds from home.

Base case for storage:

**1.**	`Package 1` (private Key 1 and information package A) at someone you trust. This package is a little bit more important then the other two as it's easier to restore funds with this package. 

**2.**	`Package 2` (private Key 2 and information package B) at someone else you trust or in a different location then your home. 

**3.**	`Package 3` (private Key 3 and information package C) in a vault or a safe deposit box at a bank or at a specialized company. 

**4.**	Hardware Wallet A and Hardware Wallet B in your home (preferably in a safe). This gives you the possibility to spend from your cold storage at any time. 

**5.** Digital note, encrypted and stored on a server you can access away from your home or on a USB stored in another location then your home.

You can of course modify this to fit your situation (only use persons you trust, only use vaults etc). But you shouldn't store the private keys in the same building or store more then your two hardware wallets at home.

This is a solid setup. The persons you trust can’t access your funds or even see your balance. You can control your funds from your home. If one hardware wallet breaks, you only need one other key to access your funds. If someone steals your hardware wallets, they would still need both of your PINs and the master public key for the last key to spend anything. The keys stored in other locations needs to be combined with 2 other keys to spend. 

If you are giving your packages to other persons. Try to deliver them yourself, never put anything in an e-mail. In the worst case, mail the packages one at a time with snail mail and confirm that they are delivered properly. Tell the persons that are holding the packages what it is and who they need to contact in case of an emergency where they need to access the funds.

It’s a good idea to store everything in envelopes and seal with tape (so you'd notice if it’s been open). Avoid writing “Bitcoin” or something on the envelopes, they should look as normal as possible. Control your keys from time to time (like once a year). Move your funds to a new multi-sig wallet if one of the keys are lost or compromised.

Finish up by sealing the USB you used for Tails with tape (so you don't use it for something else) and if you used an eternally quarantined computer, put a tape on the ethernet-port and mark it so you or, someone else, don't use it by accident.

Everything is now set to start to HODL with a peace of mind!

## Worst case scenarios

So, what are the worst case scenarios? How vulnerable are you to theft or loss and how are your trusted persons going to access your funds in case of an emergency?

Your funds are most vulnerable to "the $5 wrench attack":

![Wrench](images/50_wrench.png)
_$5 wrench attack by https://xkcd.com/538/ _

That means, if someone breaks into your house and threatens you until you give them your bitcoins amd this is why:

![First Rule](images/50_first_rule.png)

Feel free to talk about Bitcoin, but never talk about how much bitcoin you own (that's not very classy anyways). That's the best defence against this type of attack. Even if you couldn't access your funds from your home, an attacker could hold you hostage until you pay. You could use multiple wallets and different PINs on your hardware wallets to reduce the risk of losing your main stash in an attack.

Another bad case is if your computer is compromised. If an attacker got access to your secure note or your wallet file in Electrum, they would be able to derive all your addresses. If they had this access, it's very possible that they could be able to get your name and address as well. If this attacker attacks you in your home, multiple wallets wouldn't help since the attacker would know how much you owned. This is truly a worst case scenario and we do what we can to reduce this risk. If you use Tor and/or your full node you reduce the risk compared to simply giving remote servers a lot of this information. But it's still a risk we need to acknowledge. 

Important to remember, your funds aren't at risk only because your computer is compromised. As long as one of the hardware wallets do what they are designed to do (not leak the private key) and the last private key was generated properly in Tails, your funds are safe. An attacker would need you to give them access to the funds (physical attack or social engineering). 

If the people you trust with your packages were going to collude against you, they would need all 3 packages. If the ones holding package 1 and 2 tried to spend, they wouldn't have password B. If person 1 got access to package 3 she wouldn't have password A and if person 2 had access to package 3 she wouldn't have the public key for key 1 (needed to construct the multi-sig).

What if someone needed to access your funds in case you are hospitalized or worse?

The worst case would be if your house burned down and you and your hardware wallets with it. All three keys stored in other places would then be needed to access your funds. The multi-sig contract could be reconstructed by combining all private keys (+ the seed passwords) or two private keys and the last master public key (in the right order).

If you are in a coma or die (without your house burning down) and a trusted person needs to access your funds, access to package 1 is needed. If we assume that the person can get access to your hardware wallets (drill the safe or whatever is needed). The person can combine its package with either package 2 and the hardware wallets or package 3 and the hardware wallets. They can of course combine it with package 2 and 3 and get access as well.

What about loss of keys?

If your house burns down with your hardware wallets in it, but you survive, you can construct the multi-sig wallet with your secure note and any 2 of the private keys.

If your computer crashes and you lose access to your electrum wallet file and you somehow lose your secure note, you can reconstruct the wallet with your hardware wallets and package 1 or 3.

## **[P]** Improvements

To be a true Bitcoin first class citizen you need to run your own Bitcoin full node and validate all transactions yourself. That way you don't rely on trusted third party servers and as a bonus improves your privacy.

If you run a Bitcoin Core node you can use “Electrum Personal Server” to connect it with Electrum. This can be a little bit tricky for a non-technical user (especially on Windows and Mac). I’ve created guides for users on Windows and Mac in the bonus section. You can find the guides here: [Windows](hodl-guide_63_eps-win.md), [Mac](hodl-guide_64_eps-mac.md). Linux user can watch a tutorial here: https://www.youtube.com/watch?v=1JMP4NZCC5g (not my tutorial) or follow the official documentation. You can read more about the project on https://github.com/chris-belcher/electrum-personal-server. Once done you can use Electrum as usual, but without relying on someone else for verifying and broadcasting transactions. You can use it for more “day-to-day” spending as well. You can connect a hardware wallet to Electrum or use a hot-wallet (private key stored on the computer) and verify all transactions yourself.

The second-best option is to use your Bitcoin full node to add watch addresses. You simply add all addresses you want to keep track off and your node checks for any activity on those addresses. If you have a full node running, this is very simple. Check the bonus section for how to [add watch addresses in Bitcoin Core](hodl-guide_65_watch-address.md). You’d still have to connect to random Electrum servers to broadcast transactions, but that isn't terrible if you use Tor or a VPN. The crucial part is to validate every transaction you receive.

Another very important aspect of privacy is what traces you leave on chain. A very common example is that you buy bitcoin on an exchange that use KYC (know your customer). They then have all your personal information. If you then transfer your funds directly from the exchange to your cold storage, they would still know what bitcoin you most likely own. There are multiple other ways your funds can be linked to you and you never know who has this information. An easy way to break this link is to mix your coins with a technique called coinjoin. This has often been done by central parties, I would advice against those services. You put your trust in them, both with your privacy and with your keys as they could steal your bitcoin. A better alternative is to use a service that never control our keys. Two alternatives are [Joinmarket](https://github.com/JoinMarket-Org/joinmarket) and Wasabi Wallet. You can find a guide and best practises for [Wasabi Wallet](hodl-guide_62_wasabi-wallet.md) in the bonus section.

*Note:* Some exchanges treat coins involved in coin join transactions as suspicious. If you do a coin join transaction and then tries to transfer the coins to an exchange, they might reject your deposit. You have to decide yourself about privacy vs ease of selling. 

---

For more improvments check out: [Bonus >>](hodl-guide_60_bonus.md)
