[ **Intro** ] -- [ [Preparations]( hodl-guide_10_preparations.md) ] -- [ [First Seeds](hodl-guide_20_first-seeds.md) ] -- [ [Last Seed](hodl-guide_30_last-seed.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Storage](hodl-guide_50_storage.md
) ] -- [ [Bonus](hodl-guide_60_bonus.md) ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

# The Hodl Guide v1.0

---

Bitcoin gives you the possibility to store value in ways earlier generations only could dream about. A common man can store value in a more secure and trust minimized way then any king throughout history. If done right, no one even needs to know what you own.

I wrote this guide in my own quest to become a first-class Bitcoin citizen. A first-class Bitcoin citizen has control of his own keys, runs his own full node to validate all transactions and does this in a secure and private way. I’m no technical expert myself, so this guide only uses tools that’s been properly battletested throughout the years. The goal of the guide is to find a middle ground in the constant battle between usability and security. More bitcoin has probably been lost because of a complicated process with paper wallets then has been stolen. This guide uses HD-wallets (hierarchical deterministic wallet) with mnemonic seeds (12-24 regular English words). That reduce the risk of fatal mistakes and improves privacy since you don't have to reuse addresses. In the end of the guide, you'll have a reliable and secure **cold storage**!

## Who is this for?

The guide is for everyone who wants to store their bitcoin in a secure way (you don’t need any specific technical knowledge).

However, it might be overwhelming if you are new to storing your bitcoin on hardware wallets or using Linux and the terminal to enter simple commands. In that case, I would recommend that you start with [Hodl Guide Light](https://github.com/DriftwoodPalace/guides/blob/master/hodl-guide-light/README.md) or [Hodl Guide Light, Multi Sig](https://github.com/DriftwoodPalace/guides/blob/master/hodl-guide-light-ms/README.md). You can always upgrade your storage at a later date.

You should have a basic understanding of what a seed that you can generate private keys from is and why it´s important to store it in a secure way. You can read more about secret seeds [Here](https://en.bitcoin.it/wiki/Seed_phrase), we are using a passphrase to encrypt our seeds.

The full setup uses two different hardware wallets and one backup seed created with the Tails operating system. The most time consuming, and slightly more technical, part is related to Tails. The full setup should take 2-3 hours, excluding download and sync-times. The guide is meant for normal users and not high profile individuals that might be targeted for specific attacks (but they can probably use parts of the guide).  

## Privacy

The guide gives you the opportunity to create a very private storage solution as well. Those parts are optional (but recommended). They don’t directly affect the security of your seeds. But they reduce the risk of being the victim of a targeted attack (virtual or physical). The privacy parts are marked with a **[P]**. Privacy isn’t black and white and every situation is different. I would recommend to at least try a few of the methods that might work for you. It’ll probably payoff in the long run. The best security for your bitcoin is probably that no one knows that you own them in the first place.
If you want two deep dives about why privacy is very important, check out https://medium.com/human-rights-foundation-hrf/privacy-and-cryptocurrency-part-i-how-private-is-bitcoin-e3a4071f8fff and https://en.bitcoin.it/wiki/Privacy.

At the end of the guide, you’ll have a set of 3 seeds, 3 information packages, 2 hardware wallets and a plan to store those in a secure way. That includes the possibility for people you trust to access them (if they collaborate which each other) in case of an emergency.

## Cold Storage

This is a guide for Cold Storage. Only put funds that you don’t need to access frequently in cold storage. A good starting point could be to store 70-90% in cold storage, 10-30% in a hardware wallet and 0-10% in a hot wallet on your phone or computer (lightning etc). 

I, or no one else, is responsible for your funds. This guide gives you the tools, but you have to evaluate and perform all the steps yourself. Only you are responsible for your bitcoin. Grow a spine and start loving it!

## More Reading

For more reading on cold storage, see:

https://github.com/rustyrussell/bitcoin-storage-guide

And for even more depth, take a look at:

https://glacierprotocol.org/

## Contributions

This guide has one goal. To create a solid cold storage. Any critique or improvement proposal to the guide is highly appreciated. Feel free to open a pull request or contact me on Github or Twitter ([@DriftwoodPalace](https://twitter.com/DriftwoodPalace)).

Thanks to [@jakobalexander](https://github.com/jakobalexander) and [@justinmoon](https://github.com/justinmoon) for early feedback and reviews of the guide. As always, feedback does not constitute endorsement of the content.

## Changelog and validation

If you are coming back to the guide at a later date. Start by checking the [Changelog](changelog.md) for any major changes to the guide.

If you want to validate the guide. all changes are signed with my signing key. You can go to [commits](https://github.com/DriftwoodPalace/guides/commits/master/hodl-guide) and check the commits. Every commit after version 1.0 (after mars 31 2019) should be signed with my key with fingerprint `FF54 1B4E E4E6 D845 9301 1D40 3D27 D7D3 59A0 E4A9`.  You'll see the last 16 characters on Github. You can verify that it's my signature by checking it on [Twitter](https://twitter.com/DriftwoodPalace) or on my profile here at Github.

---
Get started: [Preparations >>](hodl-guide_10_preparations.md)
