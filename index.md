---
layout: default
title: Intro
nav_order: 
---
---
**Update 2020-10-01: This guide has been discontinued and is no longer maintained. This is because, in my opinion, a better guide has been released (by Michael Flaxman). You can find that guide at https://btcguide.github.io/ 
For the old guide see [HODL-GUIDE V1.0](https://github.com/DriftwoodPalace/guides/)**
# The Hodl Guide v2.0
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Multi-sig Cold storage

Welcome to the Hodl Guide version 2.0.

Version 2.0 is an updated version of the Hold-Guide v1.0. The setup is still a **2 of 3 multi-signature wallet**. The main change is that we are using 3 hardware wallets (instead of 2 hardware wallet and one cold computer). The logic behind this decision is that we were already trusting 2 hardware wallets anyway. So not worth the small possible gains a cold computer might bring when it’s easier to do the setup with 3 hardware wallets (as long we use 3 different manufacturers).

I’ve also cleared up the guide a bit. It’s more direct with less options. You can of course modify the guide to fit your situation. But I believe it’s easier to follow if it’s one solution from start to finish.  

The old version of the guide that used 2 hardware wallets and one key created on an offline computer with “Tails” can be found [here](https://github.com/DriftwoodPalace/guides){:target="_blank"} (not updated anymore). The old guide offered an option for single sig and 2 of 2 multi-sig as well, this will not be described in this guide.

If you are here to recover funds from a wallet created by someone else, see [Recovery](hodl-guide_68_recover.md){:target="_blank"}.

## Background

Bitcoin offers the possibility to store value in ways earlier generations only could dream about. If done right, a common man can store value in a more secure and trust minimized way then any king throughout history.

I wrote this guide in my own quest of becoming a first-class Bitcoin citizen. A first-class Bitcoin citizen has control of his own keys, runs his own full node to validate all transactions and does this in a secure and private way. I’m no technical expert myself, so this guide only uses tools that’s been properly battletested throughout the years. The goal of the guide is to find a middle ground in the constant battle between usability and security. More bitcoin has probably been lost because of a complicated process of securing private keys then has been stolen. This guide uses HD-wallets (hierarchical deterministic wallet) with mnemonic seeds (24 regular English words). This reduces the risk of fatal mistakes and improves privacy since you don't have to reuse addresses. In the end of the guide, you'll hopefully have a reliable and secure **cold storage**!

## Who is this for?

The guide is for everyone who wants to store their bitcoin in a secure way. You don’t need any specific technical knowledge, but it doesn't hurt if you are somewhat "tech-savvy".

It's good to have an basic understanding of what a seed that you can generate private keys from is and why it´s important to store it in a secure way. You can read more about secret seeds [Here](https://en.bitcoin.it/wiki/Seed_phrase){:target="_blank"}, we are using a passphrase to encrypt our seeds.

The full setup uses three different hardware wallets. The full setup should take no more then 2-3 hours, excluding download and sync-times (it could be done in 15 minutes if you know what you are doing). The guide is written for with a "normal individual" in mind. You have to know your own specific threat level and adjust accordingly.

## Privacy

The guide tries to keep focus on the privacy of your storage solution as well. Those parts doesn’t directly affect the security of your seeds. But they reduce the risk of being the victim of a targeted attack (virtual or physical). The privacy parts are marked with a **[P]** and you could skip those if you feel that it's overkill for your personal threat level.

Remember, the best security for your bitcoin holdings is probably that no one knows that you own anything in the first place.
If you want more reading on why privacy matters, check out [https://en.bitcoin.it/wiki/Privacy](https://en.bitcoin.it/wiki/Privacy){:target="_blank"} and [https://medium.com/human-rights-foundation-hrf/privacy-and-cryptocurrency-part-i-how-private-is-bitcoin-e3a4071f8fff](https://medium.com/human-rights-foundation-hrf/privacy-and-cryptocurrency-part-i-how-private-is-bitcoin-e3a4071f8fff){:target="_blank"}


## Cold Storage

This is a guide for Cold Storage. Only put funds that you don’t need to access frequently in cold storage. A good starting point could be to store 70-90% in cold storage, 10-30% in a single hardware wallet and 0-10% in a hot wallet on your phone or computer (lightning etc).

At the end of this guide, you’ll have a set of 3 seeds, 3 information packages, 3 hardware wallets and a plan to store all this in a secure way. That includes the possibility for people you trust to access them (if they collaborate which each other) in case of an emergency.

I, or no one else, can be responsible for your funds. I'm just one person. There might be errors in this guide and you'll have to verify and perform all steps yourself. But, this guide hopefully gives you the tools to create a secure storage. In the end, only you are responsible for your bitcoin. That's the beauty of it, grow a spine and start loving it!

## Issues, errors or improvements

If you have trouble following the guide, see any errors or have suggestions for improvements; open an issue [here](https://github.com/DriftwoodPalace/Hodl-Guide/issues){:target="_blank"}. If it's critical or private information, try contacting me at Twitter ([@DriftwoodPalace](https://twitter.com/DriftwoodPalace){:target="_blank"}, warning I'm not very active). Your first alternative should be to open an issue on Github. That way other people can help and your question might help other people.

## More Reading

For more reading and different solutions for cold storage. Take a look at:

[https://github.com/rustyrussell/bitcoin-storage-guide](https://github.com/rustyrussell/bitcoin-storage-guide){:target="_blank"}

And for even more depth (great info on side-channel attacks here):

[https://glacierprotocol.org/](https://glacierprotocol.org/){:target="_blank"}

Or if you need help, you could look at solutions from companies like (I haven't tried any personally):

[https://keys.casa/](https://keys.casa/){:target="_blank"}

[https://www.unchained-capital.com/](https://www.unchained-capital.com/){:target="_blank"}

## Contributions

Thanks to [@jakobalexander](https://github.com/jakobalexander){:target="_blank"} and [@justinmoon](https://github.com/justinmoon){:target="_blank"} for early feedback and reviews of the guide. As always, feedback does not constitute endorsement of the content.

If you like to contribute financially to the guide, feel free to send some sats to `bc1qd5rspp2rdncd2vnj4p9pmvscsa970fs2y6kzmv` or with [Bottle Pay](https://pay.bottle.li/send/social/bottle/qeYFDgq4voZ85tEjZTVjTraxriEhfRhxj88GyFs4sUBK?a=https%3A%2F%2Fcdn.bottle.li%2Fuserimg%2F47eb9b6e8939f39289bdd8fc108ec60273f8dc1cbd7bf5f1bd2fbc34d40d40de.jpg&d=Driftwood%20Palace){:target="_blank"}. This'll help keeping the guide updated with new hardware wallets etc in the future.

## Validation

If you want to validate the guide. all changes are signed with my signing key. You can go to [commits](https://github.com/DriftwoodPalace/Hodl-Guide/commits/master/){:target="_blank"} and check the commits. Every commit after version 1.0 (after mars 31 2019) should be signed with my key with fingerprint `FF54 1B4E E4E6 D845 9301 1D40 3D27 D7D3 59A0 E4A9`.  You'll see the last 16 characters on Github. You can verify that it's my signature by checking it on [Twitter](https://twitter.com/DriftwoodPalace){:target="_blank"} or on my profile here at Github.

---
Get started: [Preparations >>](hodl-guide_10_preparations.md)
