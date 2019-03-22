[ [Intro](README.md) ] -- [ [Preparations]( hodl-guide_10_preparations.md) ] -- [ [First Seeds](hodl-guide_20_first-seeds.md) ] -- [ [Last Seed](hodl-guide_30_last-seed.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Storage](hodl-guide_50_storage.md
) ] -- [ **Bonus** ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

## Electrum best practises for private Cold Storage

*Difficulty: medium*

You have your cold storage wallet created and you want to start using it. But how do you keep your wallet private? Yo do not want that anyone else knows exactly which bitcoin you control.

There are many traps that can reduce your privacy. All bitcoin transactions are public so you can leave traces onchain but you can also leave many traces off chain. 

A great start is to have two seperate wallets. One spending wallet and one cold storage wallet.  
Some of the most worst cases is when you buy something with your real name. That can be something that's shipped to your home or if you transfer bitcoins to an exchange that uses KYC.


WORK IN PROGRESS


![Electrum tor 6](images/40_electrum_tor_6.png)

Close the network dialog. The circle in the bottom right corner should now be blue and not green. You have now configured Electrum to run over Tor. Electrum won’t connect to anyone unless Tor is running (even if you restart it). You still rely on third parties for validation and broadcasting, but they won't see your real IP-address.

*Troubleshooting:* If you aren't getting a blue circle or any connections try changing the port to `9150`. Tor can sometimes use this port on Windows.

------

<< Back: [Bonus guides](hodl-guide_60_bonus.md) 
