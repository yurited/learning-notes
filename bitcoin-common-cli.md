
you can try out bitcoin cli api here
https://bitcoin.org/en/developer-reference#bitcoin-core-apis


### Set transaction fee
bitcoin core set transaction fee
bitcoin-cli settxfee BTC/KB

BTC/KB <-> satoshi per byte
1 sat/b = 0.00001 btc/kb
15 sat/b = 0.00015

### bitcoin core fee estimate
bitcoin core fee estimate
bitcoin-cli estimatesmartfee 2
(estimatefee is deprecated in 0.17)
sometime this doesn't work because the code isn't up long enough for get data from mempool: https://github.com/bitcoin/bitcoin/issues/11500


### Send to Address
http://chainquery.com/bitcoin-api/sendtoaddress
