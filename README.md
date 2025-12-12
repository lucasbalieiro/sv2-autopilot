## Overview

The goal of this project is to keep a full **sv2-apps** stack ([https://github.com/stratum-mining/sv2-apps](https://github.com/stratum-mining/sv2-apps)) running **24/7 on signet**, continuously mining new blocks. The mission is simple: let the system run for a long time and see what breaks, behaves weirdly, or slowly falls apart. Classic long-haul stress testing.

I’m currently using **bitcoin-v30** as the template provider via **IPC**. These sessions have already shaken loose a few interesting bugs and edge cases. Recently, for example, the stack uncovered a *possible* memory leak in Bitcoin Core v30 when using IPC (still being poked at).

There’s also a minimal UI you can check out:
**[https://sv2-gs-autopilot.lucasbalieiro.dev/](https://sv2-gs-autopilot.lucasbalieiro.dev/)**
It displays recent logs from each component and the current commit/height under test.
Fair warning: the UI may be down occasionally — it’s running on a very cheap VPS. I’ll upgrade it when more sats find their way into my wallet.

This long-running setup is also handy whenever we do large refactors in sv2-apps — like the recent tproxy and JDC overhauls. It quickly surfaces any regressions that might slip through code review.

---

## Network Rotation Testing

Every now and then, I switch the Bitcoin Core node over to **testnet4** or **mainnet** to make sure the apps don’t panic. It’s a good way to see how the stack behaves under unexpected forks, mempool churn, and general cross-network chaos. If anything is going to lose its mind, this is usually what triggers it.

