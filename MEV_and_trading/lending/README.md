## lending

<br>

### tl; dr

<br>

* alice and bob deposit funds into a lending contract (e.g., aave, maker, compound). while bob leaves his original collateral locked in the protocol, he can withdraw ~50% or more (depending on the protocol and asset) at some algorithmic rate that gets paid to alice (for providing the funds). 
* bob can then create a short position, reinvest for a levered long position, or withdraw money (without selling the underlying and being taxed). alice, on the other hand, generates a return on her capital.
* liquidation is paid to the address that flags loans that crossed collateralization threshold (anyone monitoring the mempool and external oracles).

<br>

---

### in this dir

<br>

* [protocols](protocols)
* [collateralized](collateralized.md)
* [uncollateralized](uncollateralized.md)
* [composable leverage](composable.md)

<br>

---

### resources

<br>

* [survey of defi lending](https://timroughgarden.github.io/fob21/reports/r5.pdf)
* [leveraged lending, by defillama](https://defillama.com/yields/loop)
