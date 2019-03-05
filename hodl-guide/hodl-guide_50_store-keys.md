[ [Intro](README.md) ] -- [ [Preparations](raspibolt_10_preparations.md) ] -- [ [The First Keys] ](hodl-guide_20_first-keys.md) -- [ [The Last Key] ](hodl-guide_30_last-key.md) -- [ [Multi-Sig Wallet](hodl-guide_40_multi-sig.md) ] -- [ **Store your keys** ] -- [ [Bonus](hodl-guide_60_bonus.md) ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

# Store your keys

You should now have the following information:
* Package A
  * Hardware Wallet A (containing private key 2)  
  * If you don’t use a password manager, information package A (with master public key 1 and 3 and password A and B)
* Package B
  * Hardware Wallet B (containing private key 3)
  * Information package B (with Master Public key 1 and the instructions for Electrum)
* Package C
  * Private key 1
* Package D
  * Private key 2
  * Information package D (with Password B and the pin to Hardware Wallet B)
* Package E
  * Private key 3
  * Information package E (with Password A, the pin to hardware wallet A and master public key 2)

Since you’ve duplicated two of your private keys, this is almost like a 2 of 5 signature scheme (not exactly since you could lose two of the same keys). This means that you could lose 2-3 pieces and still be able to restore your funds. So how should you handle this information? The key concept is to not store 2 pieces of information at the same place. Then you’d risk losing two keys at the same time and a thief could force you to spend your bitcoin. So, how you’ll store your information depends on your situation.
A base case could be:
1.	Hardware Wallet 1 at your home (preferably in a safe), this could be used to double check deposits to the cold storage (check the deposit address on the device) without accessing anything else. Optionally stored with information package A.
2.	Hardware Wallet 2 and its corresponding information package B at someone you trust (person 1). 
3.	Private Key 1 in a vault or safe deposit box at a bank or specialized company (this is the backup key).
4.	Private Key 2 and its information package D at someone you trust (person 2)
5.	Private Key 3 and its information package E in another vault or safe deposit box or at someone you trust (person 3)
You can of course modify this to fit your situation.
If this is too much work, you can reinstall/flush one of the hardware wallets and only have 4 keys to distribute. If you do this, you’d have to put your seed into a hardware wallet or cold computer in case of a withdrawal from the cold storage.

This is a solid setup. The persons you trust can’t access your funds or even see your balance. You only need one other key apart from the one in your home (that’s protected with a PIN). But the keys stored in other places needs to be combined with 2 other keys to spend. So, a malicious actor would need 3 of those keys to access your funds.   

If you are giving your keys to another person. Try to deliver them yourself, never put anything in an e-mail. In the worst case, mail the key with snail mail and make sure the keys are delivered. Tell the other person what it is and who they need to contact in case of an emergency when they need to access the funds.

It’s a good idea to store everything in envelopes and seal with tape (so you notice if it’s been open). Avoid writing “Bitcoin” or something on the envelopes, they should look as normal as possible. Control your keys from time to time (like once a year), move to a new multi-sig if one of the keys are lost.

Everything is now set to start to HODL!


