# clone-lin-gmx-v2-collateral-sum

Experimental LIN clone of GMX V2 `applyDeltaToCollateralSum` (uint64-scale unsigned collateral sum: reject-negative then always-on `maxCollateralSum`).

- **Upstream:** [gmx-io/gmx-synthetics](https://github.com/gmx-io/gmx-synthetics) `contracts/market/MarketUtils.sol` commit `a85ea3491c19c93bb4b5a002d9b358fb769b7849` (GPL-2.0-or-later after BUSL Change Date 2026-08-31).
- **LIN kernel:** [`src/lin_gmx_v2_collateral_sum.lin`](src/lin_gmx_v2_collateral_sum.lin)
- **C11 oracle copy:** [`test/oracles/gmx_v2_collateral_sum_c11.c`](test/oracles/gmx_v2_collateral_sum_c11.c)
- **Proofs (lin-open only):** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/gmx_v2_collateral_sum/` and `python3 test/prove_gmx_v2_collateral_sum_external.py`
- **Class:** EXPERIMENTAL. Not Arbitrum GMX V2 uint256. Not a production replacement. Not `applyDeltaToOpenInterest` (max-on-increase + swap-only + signed VI) and not `applyDeltaToVirtualInventoryForSwaps` (unsigned pair, floor-at-zero).

Named goldens (uint64-scale, sum=1e8 max=2e8 unless noted): long +3e7 → **130000000** (short side is the same; `isLong` is a key, not a sign flip) vs position-style flip **70000000**; 1e8+3e7 vs max 1.2e8 **ok=0** vs no-max **130000000**; decrease 1.5e8-2e7 still over max 1.2e8 **ok=0** vs OI-style max-on-inc **130000000**; 1e8-1.5e8 **ok=0** vs bounded floor **0/ok=1** vs signed **-50000000**; max=0 disables any positive next; swap-only index=0 **ok=1** vs OI reject **ok=0**; getter /2 **65000000**; 7e18+3e18 fail-closes vs naive i64 wrap **-8446744073709551616**.
