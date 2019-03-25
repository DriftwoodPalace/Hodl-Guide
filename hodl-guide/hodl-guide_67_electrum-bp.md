[ [Intro](README.md) ] -- [ [Preparations]( hodl-guide_10_preparations.md) ] -- [ [First Seeds](hodl-guide_20_first-seeds.md) ] -- [ [Last Seed](hodl-guide_30_last-seed.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Storage](hodl-guide_50_storage.md
) ] -- [ **Bonus** ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

## Electrum best practises

*Difficulty: medium*

You have your cold storage wallet created and you want to start using it. But how do you keep your wallet private? 

This is not black and white. There are many traps that can reduce your privacy. All bitcoin transactions are public so you can leave traces onchain but you can also leave many traces off chain. How much effort you put in should depend on your personal threat level. How much time and effort is it worth to put in to secure your bitcoin the best you can?

If you have taken the time to create a cold storage wallet, I would advise you to at least look at some of the easiest solutions that'll give you most "bang for your bucks".

This is the short version:
* Use Wasabi Wallet as a spending wallet and never use your cold storage wallet to directly send funds to someone else.
* Mix all bitcoins before depositing to your cold storage.
* Top up your spending wallet with whole UTXOs (coins). Do not produce any change in your cold storage wallet.
* If you don't have Electrum connected to your own full node, mix all coins going out of your cold storage wallet.
* Setup Electrum to run over Tor. Or even better connect it to your full node. 
* Do not go and look up your addresses on any block explorers.

The full recommandation would be the following:

Electrum multi-sig wallet > Electrum Client > Electrum Personal Server > Bitcoin Core > Tor

This is the longer version: 

A great start is to have two separate wallets. One spending wallet and one cold storage wallet. 

As a spending wallet I would recommend Wasabi Wallet https://www.wasabiwallet.io/ (Tor link http://wasabiukrxmkdgve5kynjztuovbg43uxcbcxn6y2okcrsg7gb6jdmbad.onion/). This wallet is designed to be a spending wallet. A bitcoin is only an unspent output from a previous transaction (UTXO). Wasabi gives you control of these outputs. It also offers an excelent option to mix your coins with coin. You can find a guide for installation and some best practises [here](hodl-guide_62_wasabi-wallet.md).

When you spend bitcoin, you often link different UTXOs togheter to construct the paymnet. You also usually send some of it back to yourself as change. This can be used to cluster many addresses in your wallet togheter. It's not foolproof, but someone watching the chain can assume that a cluster of addresses belongs to you. If you then for example buy something and ships it to your home or deposit bitcoin to an exchange that use KYC, from one address. Many more addresses can be linked to you.

This analysis can be broken if you use coinjoin. One method is to use Wasabi Wallet (or Joinmarket) to mix all your coins before depositing to cold storage. Keep a few mixed outputs in Wasabi Wallet and use that if you'd like to spend bitcoin. Remember that Wasabi Wallet is a hot wallet. Treat it like cash in your pocket and don't keep larger amounts in it. Then you can top up your Wasabi Wallet as needed. Either by buying more at an exchange (and mix) or depositing from your cold storage.

I would recommend to always try to send whole outputs from your cold wallet. This way, you won't produce any change that you have to keep track of. To do this in Electrum, go to the `Coins` tab. Right click on the address you'd like to spend from. Select `Spend`. Then fill in the receiving address and select "Max" on the `Send` tab. You can send more then one output in the same transaction, but know that they'll be linked togheter. If you want to do this, select multiple outputs by holdning ctrl/cmd and marking the outputs.

If you don't run your own full node and connect Electrum to it with for example Electrum Personal Server, you'd have to mix your outputs again if you'd like to keep your privacy. Electrum uses specialised servers that will know of all your used addresses. Anyone can run a server and you'll be connected to one randomly by default.

Even if you use Tor you are still giving all your addresses to some random server. Tor will hide your real IP, but the server will still know which addresses belongs togheter. If you say, transfer one whole UTXO to Wasabi but doesn't mix. At a later date you deposit this output to an exchange that knows your name. This exchange collaborates with a company that analyse the blockchain. If this company runs an Electrum server that you once connected to, it's trivial to track your deposit back to your wallet. They will know your whole wallet balance and now your name. If you doesn't use Tor (or a VPN), this will be even easier. The server has your IP-address and the exchange can se that you log in with the same IP on their site.

If you mix your coins before depositing, it'll be much much harder to trace it back to your wallet. It'll be like a firewall that protects your cold storage. This will be more effective if you use Tor or a VPN (Tor is better as you will constantly change your IP-address). 

That's why the next recommendation is to configure Electrum to run over Tor. You can find a guide for that [here](hodl-guide_66_electrum-tor.md). That's only if you can't run a full node and connect Electrum to that. With a full node you will download every transaction and every block. No one can know what transactions you are looking for. This will always be a problem with "light wallets". They don't download everything by definition. That means that you are asking someone about some specific information. This can be used to connect your addresses togheter. You can find a guide for setting up Bitcoin Core, [here](hodl-guide_61_bitcoin-core.md), for connecting your full node to Electrum with Elctrum Personal server, you can find a guide for Windows [here](hodl-guide_63_eps-win.md) and for Mac [here](hodl-guide_64_eps-mac.md).

If you use your full node (especially if it use Tor), there really isn't any need to mix your coins when withdrawing. As long as you avoid producing change and always send whole UTXOs out of your wallet. Unless someone has your master public key, it should be very hard to cluster the addresses in your wallet togheter. However, if fees are low and you have the time, there's no harm in mixing again.

Last but not least. Do not go and look up any of your addresses on a block explorer. You will destroy a lot of the hard work you put in. Who else then you would go to a block explorer and look up one of your addresses? Maybe multiple times or right after a transaction with a few updates until the transaction is confirmed. If you do this with your real IP-address, it's a clear indication that the address belongs to you and this will probably be saved somewhere. If you really need to look it up for some reason, use the Tor browser. The block explorer will then know that someone looked up an address. But it can't know who. You could for example use blockstream.info with their onion address http://explorerzydxu5ecjrkwceayqybizmpjjznk5izmitf2modhcusuqlid.onion/ for maximum privacy.

This will take you a long way in keeping your cold storage private.

------

<< Back: [Bonus guides](hodl-guide_60_bonus.md) 
