[ [Intro](README.md) ] -- [ **Preparations** ] -- [ [First Seeds](hodl-guide_20_first-seeds.md) ] -- [ [Last Seed](hodl-guide_30_last-seed.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Storage](hodl-guide_50_storage.md
) ] -- [ [Bonus](hodl-guide_60_bonus.md) ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

-------

# Preparations

## Mandatory Hardware Requirements for Full Setup

* 2 USB flash-drives. One with 8GB+ memory. Consider buying new ones, used only for this purpose.
* 2 different Hardware-wallets (Trezor, Ledger, Coldcard etc). Make sure the hardware-wallets are from two different manufacturers (for example one Trezor and one Ledger). You can use existing devices if you already own some (but they shouldn't be used for other purposes after you're done). If you're buying new ones, make sure to only buy from the official store. It's always sensitive to have Bitcoin-related stuff shipped to your home. Consider having it delivered to a UPS access point or a similar service.
* 1 internet connected computer. Could be your normal computer. Should have at least 1 USB-slot and a camera (for reading QR-codes). If you only use one computer, the computer needs to have a 64-bit processor and 2 USB-slots.
* 1 Smartphone (or digital camera with screen)

## Optional Equipment and Hardware

* 1 extra computer. This will make the process of working with Tails easier. If you have an old computer lying around, consider using it and making it an eternally quarantined computer (or buy a cheap used computer). That’s a computer that´s going to be eternally quarantined (only used for this purpose and never used for anything else or connected to the internet again). If you are using an eternally quarantined computer it’s a good idea to format/reinstall the computer to get it as fresh as possible. You can even wipe the operating system of the computer since we are using Tails. Before wiping the OS, try it out with Tails. You might have to update some drivers for it to work.
  * The computer needs 2 USB-slots, a camera and a 64-bit processor. If you’re not sure check the computers properties or if you’re buying a used computer, you can search for the computer’s processor on [CPU World](http://www.cpu-world.com). “Data width” should be 64 bit.
* Home safe. For safe, waterproof and fireproof storage for one of the Hardware Wallets.
* [TerraSlate paper](https://www.amazon.com/dp/B076JKVNWY/), waterproof, heat resistant and tear-resistant paper.
* Envelopes to store sensitive information in.
* Tamper-resistant seals or tape.

## [P] Bitcoin Core

If you are looking for a really private and secure solution, there's really only one option. Running your own full node by using Bitcoin Core. Bitcoin core is the main software implementation of the Bitcoin protocol. By using your own node to validate transactions, you´re also helping the network and making it more decentralized.
Check out the bonus guide, [Install and optimize Bitcoin Core](hodl-guide_61_bitcoin-core.md) for how to install and setup a node.

*Note*, the Bitcoin blockchain size is approaching 300 GB. It could take several days to download the whole blockchain. If storage is an issue, you could use “pruned mode”. That way, you´d discard old transactions and only need to store a few GB of data. You won’t be able to help new nodes connect, but you´d still validate everything yourself. If you´re on a limited data plan, downloading 300 GB of data might still be an issue. In that case you´d have to rely on third parties for validating and broadcasting transactions and can skip this step.

-------
Move on to: [Generate the first two seeds >>](hodl-guide_20_first-seeds.md)
