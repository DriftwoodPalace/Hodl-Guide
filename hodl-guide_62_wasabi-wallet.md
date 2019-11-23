---
layout: default
title: Wasabi
parent: Bonus Section
nav_order: 11
has_toc: false
---

# Wasabi Wallet

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

Wasabi Wallet is a bitcoin wallet designed with privacy in mind. The wallet gives the user control of different "UTXOs". A UTXO is simply an unspent transaction output and is often referred to as "coin" (and is what makes up individual bitcoins). UTXOs are associated with bitcoin addresses and can be traced on the blockchain. This can be used to track users and try to determine who owns what. The most common heuristics for tracking users can be broken if you "mix" your UTXOs with other peoples UTXOs (and use the same amounts). The method is often referred to as "coinjoin" as is a service Wasabi Wallet offers as well.

Most implementations of coinjoin (sometimes called mixers) is by third parties that control the whole process. That means that they can steal your funds and destroy your privacy if they like (you have to trust them). This is not the case with Wasabi Wallet. The only central part is a "coordinator" that constructs the transactions and that you connect to with Tor to ensure anonymity. You control your own private keys during the whole process.

Mixing bitcoin is extra important if you bought them at an exchange that use KYC (know your customer). In that case, you'll have your name and maybe even address attached to a set of UTXOs and you can never know who has that information. This might later get mixed with funds in another wallet you control and parts, or all, of those funds might be linked to you. This can to a large degree be fixed if you use Wasabi Wallet.

Unfortunately I don't have time to keep up with everything happening in this project. There's many more qualified people for that task.

I'll leave you with links to the download https://www.wasabiwallet.io/ and if you use Tor browser, use http://wasabiukrxmkdgve5kynjztuovbg43uxcbcxn6y2okcrsg7gb6jdmbad.onion/
The link to the official documentation https://docs.wasabiwallet.io/using-wasabi/ and a great forum post https://www.reddit.com/r/WasabiWallet/comments/c7w7ua/user_guide_faq_and_10_commandments/


### Best practises to handle mixed outputs

*This information might be outdated, but might be worth reading through anyway*

Depending on how much you mix and what anonymity set you settle for, you´ll end up with a lot of smaller outputs. If you deposit 1 bitcoin and mix to the smallest denominator, you’ll end up with 10 0,1-bitcoin outputs.

So, how should you handle withdrawals to cold storage and mixing in general? If you mix larger amounts, don’t withdraw all your mixed bitcoins in the same transaction. The key is to be unpredictable. Chain analysis companies are looking for patterns. So, avoid depositing and withdrawing the same amount. If you deposit 1 bitcoin and mix it, don't combine all the mixed outputs to transfer 1 bitcoin out in the same transaction. You would still have improved your anonymity from the mixing but you can improve it even more if you deposit 1 bitcoin, mix it and withdraw in batches of say 0,3, 0,5 and 0,2 bitcoin during different times. Some guidelines:

* Be unpredictable. If you have 5 bitcoins, deposit it in uneven chunks (and generally, don’t put 5 bitcoins in a hot wallet). For example, start by depositing 1 bitcoin, then 0,7 then 1,2 and so on. Do the transactions at different times during the day.
* Aim for an anonymity set of at least 50. This’ll be visible at each separate UTXO in Wasabi Wallet.
* If you’ve mixed 5 bitcoins, you'll probably end up with 50 outputs of 0,1 bitcoin. If you were going to transfer all out individually, you’d have to do 50 different transactions and would end up with many smaller UTXOs (that could give you larger fees down the line). Is it safe to combine some of the outputs when withdrawing? Again, the key is unpredictability. You can probably combine 5-10 outputs of 0,1 bitcoin without reducing your privacy too much. But, make sure to change your behaviour (sometimes transfer 0,3 bitcoin, next time 0,5 and so on). Do the transfers at different times during the day and never deposit to old addresses (addresses you've used before).

---

<< Back: [Bonus guides](hodl-guide_60_bonus.md)
