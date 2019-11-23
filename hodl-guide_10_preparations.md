---
layout: default
title: Preparations
nav_order: 2
---

# Preparations

## Mandatory Hardware Requirements

* 1 USB flash-drive. Consider buying a new one, or at least format an old one so it is clean.
* 3 different Hardware-wallets. In the guide we are going to use 1 Coldcard, 1 Trezor One and 1 Ledger Nano S (you can use other brands or models as well). The important part is that all 3 hardware-wallets are from different manufacturers as this will make it much harder for any possible attacker. You can use existing devices if you already own one or more. If you're buying new ones, make sure to only buy from the official store and remember, it's always sensitive to have Bitcoin-related stuff shipped to your home. Consider having it delivered to an UPS access point or a similar service.
* 1 internet connected computer. Could be your normal computer, this is where we are setting everything up. If you are going to use Coldcard "cold" it'll need to be able to read SD-Cards.

## Optional Other Equipment

* Home safe. For safe, waterproof and fireproof storage of the things you store at home.
* [TerraSlate paper](https://www.amazon.com/dp/B076JKVNWY/), waterproof, heat resistant and tear-resistant paper for storage of private seeds.
* Envelopes to store sensitive information in.
* Tamper-resistant seals or tape.

## [P] Bitcoin Core

We re using Bitcoin Core to validate any bitcoin we receive in our wallet (this is what's often referred to as "running your own full node"). Bitcoin core is the main software implementation of the Bitcoin protocol. You can use the Hodl Guide without using Bitcoin Core, but it might severely hurt your privacy.

*Note*, the Bitcoin blockchain size is approaching 300 GB. It could take several days to download the whole blockchain. If storage is an issue, you could use “pruned mode”. That way, you´d discard old transactions and only need to store a few GB of data. You won’t be able to help new nodes connect, but you´d still validate everything yourself. If you´re on a limited data plan, downloading 300 GB of data might still be an issue. In that case you´d have to rely on third parties for validating and broadcasting transactions and can skip this step.

Syncing your Bitcoin Core node is the most time consuming part of this guide. So, I would recommend you'll get that process started at first. Check out the bonus guide, [Install and optimize Bitcoin Core](hodl-guide_61_bitcoin-core.md) for how to install and setup a node.

Another option is to buy a "node in a box". That's a very easy way of setting up a full node and often you'll get an Electrum Server at the same time. I haven't tried any of alternative, but two popular options seems to be:

https://shop.nodl.it/en/

https://mynodebtc.com/

If you need help setting up your node, you could try a service like:

https://www.ministryofnodes.com.au/

-------
Move on to: [Creating passphrases >>](hodl-guide_20_passphrasess.md)
