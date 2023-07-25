## gmx

<br>

### tl; dr

<br>



* gmx is a decentralized spot and perpetual futures exchange built on arbitrum and avalanche chains. it exploded after the ftx fall, and just this week it seems to have become the top defi project on fee profit, and one of the top projects by fee and revenue in defillama. they are winning by offering perks such as no slippage, low swap fees, and zero price impact trades (i.e., large trades are set at the mark price).

* gmx offers zero slippage on trades via an oracle price update system (chainlink + aggregate of prices from leading volume exchanges), while amms rely on arb bots to balance prices in the pools.

* gmx’s swap trades are performed based on a combination of two oracles:
  - the primary oracle is fed by chainlink, and it takes the last three samples (picking the worst price for the user).
  - the secondary oracle is the “fast price feed”, which overrides the price whenever it is within 2.5% of the primary oracle price value.

* gmx enables traders to open up to 50x leverage swaps for long or short positions by borrowing from glp, a multi-asset pool containing $btc, $eth, $uni, $link, and stablecoins. the vault allows swapping of the tokens it holds. funds are deposited into the vault by minting glp tokens and can be withdrawn by burning these tokens. glp works as the counterparty in the protocol, as it accrues values when traders loses, and devalues when traders win. glp is also emerging as a form of collateral, with lending protocols integrating this liquidity provider token into their product offerings (e.g., rage, unami, sentiment).

* gmx’s native token, $gmx, functions as a governance, utility, and value-accrual token. glp accrues 70% of all trading fees, while stakers of gmx earn 30%. a floor price fund helps ensure liquidity in the glp pool, plus a reliable stream of $eth rewards for $gmx stakers.

* the protocol's revenues come from swap fees, trading fees, execution fees, liquidation fees, and borrow fees.


<br>

----

### in this dir

<br>

* [tokenomics](tokenomics.md)
* [oracle abuse](oracle_abuse.md)
* [delta neutral and vaults](glp_vaults.md)


<br>

---

### resources

<br>

* [gmx docs](https://gmxio.gitbook.io/gmx/)
* [gmx stats](https://stats.gmx.io/)
* [gmx hedge](https://www.gmxhedge.com/)
* [building gmx and synths, by coinflipcanada](https://alphapls.substack.com/p/the-buildooooooor-coinflipcanada)
* [gmx general dune board](https://dune.com/gmxtrader/gmx-dashboard-insights)
* [post on x4 protocol](https://medium.com/@gmx.io/x4-protocol-controlled-exchange-c931cd9a1ae9)
* [gmx in-depth dune board](https://dune.com/lako/lako-labs-gmx)
* [gmx trader bias dune board](https://dune.com/steinkirch/gmx-trading-bias)
* [synapse bridge](https://synapseprotocol.com/)
* [contracts](https://gmxio.gitbook.io/gmx/contracts)
* [gmx, by flood capital](https://twitter.com/FloodCapital/status/1562856005259902976)
* [gmx oracle, by pressiemoomboy](https://twitter.com/PressieMoonBoy/status/1562905337723748352)
* [gmx transfer account](https://app.gmx.io/#/begin_account_transfer)
* [pirex gmx, by redacted](https://mirror.xyz/0xE90c74145245B498fef924fAdC7bb34253c7cF90/H15743T6tNvIW1xzOcL5_JBkQilZLdWgdqhD5AZPryI)
* [magicglp, by abracadaba](https://mirror.xyz/0x5744b051845B62D6f5B6Db095cc428bCbBBAc6F9/EUr60EjAX6h4muLqUxeygljMWTmi5b9pxJWlX7Qt3yc)

