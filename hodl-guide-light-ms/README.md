[ **Guide** ] -- [ [Bonus](https://github.com/HelgeHunding/guides/blob/master/hodl-guide/hodl-guide_60_bonus.md) ]

---

# The Hodl Guide Light, Multi Sig

---

#### *This is a draft, all feedback is appreciated!*

This is a guide for anyone who wants to start taking control of their bitcoin holdings. Maybe you want to improve your cold storage even more by creating a multi signature wallet. This is an excellent next step if you've followed [Hodl Guide Light] (https://github.com/HelgeHunding/guides/edit/master/hodl-guide-light/README.md) or if you have some experience with hardware wallets.

This is a guide for cold storage and not for a wallet used for “day to day spending”.

After you’ve completed this guide, you’ll have a secure storage solution that doesn't rely on one hardware wallet manufacturers wallet. You can later upgrade this setup to an even more complex multi-sig with the full [Hodl Guide](https://github.com/HelgeHunding/guides/blob/master/hodl-guide/README.md).

As always with Bitcoin, I or no one else can be responsible for your bitcoin. You have to trust and hold yourself responsible for everything.


## Requirements

* Two hardware wallets from different manufacturers (Ledger, Trezor,Coldcard etc).
* One internet connected computer.
* Paper of good quality to write your secret seed on (usually included with the hardware wallet).

I have experience with Trezor One and Ledger Nano S, so the guide will follow the procedure on those wallets. But you can of course use another hardware wallet if you like it and trust the manufacturer. You can use an existing hardware wallet if you have one. We are going to create a new wallet in Electrum that won't be linked to your previous wallets. So you don't have to worry about previous privacy leaks.

Electrum supports most popular hardware wallets on the market.

Hardware wallets are great. But their main focus is security, not privacy. We do not know what the future might bring. For example, how governments will treat bitcoin. You won't get much privacy if you use the hardware wallet "out of the box" with the manufacturers wallet. The setup in this guide will give you the possibility to improve your privacy.
Privacy isn’t black or white, it’s a scale. Your privacy can be breached in many ways and every individual leak can be combined to reduce your privacy. We’ll try to avoid some of the worst mistakes.
