## Lightning

Basics: HTLC
[Hashed Timelock Contract](https://en.bitcoin.it/wiki/Hashed_Timelock_Contracts)

Specifications:
BOLTs (rfc = request for comments)
https://github.com/lightningnetwork/lightning-rfc

c-lightning:
https://github.com/ElementsProject/lightning


### LND

LND (written in go)
https://github.com/lightningnetwork/lnd
https://dev.lightning.community/

---
installing of LND on my INTEL NUC Ubuntu 16.04 LTS
installing golang:
according to https://github.com/golang/go/wiki/Ubuntu
> If you're using Ubuntu 16.04 LTS and are unable to install golang-1.10-go, then you can also use the longsleep/golang-backports PPA:

```
sudo add-apt-repository ppa:longsleep/golang-backports
sudo apt-get update
sudo apt-get install golang-go
```
it looks like that sometimes LTS version of ubuntu doesn't get the latest packages by default.

if you encounter this error message while installing `package context: unrecognized import path "context"`, update your go version to at least 1.7.

Start the daemon
```
lnd --bitcoin.mainnet --bitcoin.active
```

Mainnet Lightning Node category
https://1ml.com/node/02f6725f9c1c40333b67faea92fd211c183050f28df32cac3f9d69685fe9665432
