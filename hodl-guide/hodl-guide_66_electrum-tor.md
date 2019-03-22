[ [Intro](README.md) ] -- [ [Preparations]( hodl-guide_10_preparations.md) ] -- [ [First Seeds](hodl-guide_20_first-seeds.md) ] -- [ [Last Seed](hodl-guide_30_last-seed.md) ] -- [ [Multi-Sig](hodl-guide_40_multi-sig.md) ] -- [ [Storage](hodl-guide_50_storage.md
) ] -- [ **Bonus** ] -- [ [Troubleshooting](hodl-guide_70_troubleshooting.md) ]

---

## Setup Electrum to run over Tor

*Difficulty: easy*

Electrum uses servers that’s run by volunteers to validate and broadcast transactions. 
Anyone can start a server and if you don’t specify a server, you’ll be connected to one randomly. 
This is bad for privacy (and has been used for phishing attacks). 
If you don’t use Tor or a VPN you’re essentially giving a random server your IP-address and all your bitcoin addresses. 
Your addresses are *hashed* before they are sent to the servers. 
That means that only addresses that's been used at least once are revealed to the servers (as they then can pair the hash you ask for with the hash of an address they have in their database). 
So, they won't know of any your empty addresses in your wallet.

There're several companies that specialises in chain analysis to deanonymize addresses and we can assume that they’re running several Electrum Servers. 
If you bought your bitcoin on an exchange that use KYC (know your customer), you can assume that your private data will be leaked sooner or later. 
If you don't do something about it, risk is that almost every transaction you do can be linked to you. 
A first good step is to use Tor. It uses "onion routing" to hide your real IP-address. 
You can also use a VPN, both solutions will hide your real IP-address from random servers. 
With a VPN, you'll trust the provider (all traffic goes through them) which is probably safe as long as Bitcoin is legal in your jurisdiction (but you never know).

Using Electrum with Tor should be a fairly straightforward process and we might as well do it from the start. If you don't have Tor, go to https://www.torproject.org/projects/torbrowser.html and download the latest version of Tor Browser for your OS. You should now know how to verify digital signatures. So, download the signature (.asc) for the file you download as well. You can import the Tor signing key with the command:

`gpg --keyserver pool.sks-keyservers.net --recv-keys 0x4E2C6E8793298290`

Then use:

`gpg --verify {your_file.asc}`

Make sure the output is similar to this:
```
gpg: assuming signed data in 'torbrowser-install-win64-8.0.6_en-US.exe'
gpg: Signature made 02/12/19 14:26:17 W. Europe Standard Time
gpg:                using RSA key EB774491D9FF06E2
gpg: Good signature from "Tor Browser Developers (signing key) <torbrowser@torproject.org>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: EF6E 286D DA85 EA2A 4BA7  DE68 4E2C 6E87 9329 8290
     Subkey fingerprint: 1107 75B5 D101 FB36 BC6C  911B EB77 4491 D9FF 06E2
```

When Tor is installed, start Tor. That could be done in two ways. You can launch the browser (it’s much easier to use then a few years ago) or only start Tor (like tor.exe on Windows). Only Tor should be located at `.\Tor Browser\Browser\TorBrowser\Tor`. You won't notice anything if you launch Tor without the browser (nothing visible will start).


In Electrum go to `Tools>Network`. Change the tab to `Proxy`. Select "Use Proxy" and make sure `SOCKS5` is `127.0.0.1` and that the port is `9050`:

![Electrum tor 6](images/40_electrum_tor_6.png)

Close the network dialog. The circle in the bottom right corner should now be blue and not green. You have now configured Electrum to run over Tor. Electrum won’t connect to anyone unless Tor is running (even if you restart it). You still rely on third parties for validation and broadcasting, but they won't be able to connect your addresses to your real IP-address.

*Troubleshooting:* If you aren't getting a blue circle or any connections try changing the port to `9150`. Tor can sometimes use this port on Windows.

------

<< Back: [Bonus guides](hodl-guide_60_bonus.md) 
