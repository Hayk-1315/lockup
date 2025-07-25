# Sablier Lockup [![Github Actions][gha-badge]][gha] [![Coverage][codecov-badge]][codecov] [![Foundry][foundry-badge]][foundry] [![Discord][discord-badge]][discord] [![Twitter][twitter-badge]][twitter]

[gha]: https://github.com/sablier-labs/lockup/actions
[gha-badge]: https://github.com/sablier-labs/lockup/actions/workflows/ci.yml/badge.svg
[codecov]: https://codecov.io/gh/sablier-labs/lockup
[codecov-badge]: https://codecov.io/gh/sablier-labs/lockup/branch/main/graph/badge.svg
[discord]: https://discord.gg/bSwRCwWRsT
[discord-badge]: https://img.shields.io/discord/659709894315868191
[foundry]: https://getfoundry.sh
[foundry-badge]: https://img.shields.io/badge/Built%20with-Foundry-FFDB1C.svg
[twitter-badge]: https://img.shields.io/twitter/follow/Sablier
[twitter]: https://x.com/Sablier

> ⚠️ **About this fork**
>
> This fork was created for educational and contribution purposes. I worked on two issues from the original Sablier Labs
> repository:
>
> • ✅ [Merged] Created a dedicated README for the `invariant` tests to improve clarity and documentation.  
> • ⏳ [In review] Refactored tests in the `lockup` repo to externalize SVG and token URI data using Foundry’s `vm.readFile`.
>
> All work was done in separate feature branches based on `staging`.  
> This fork reflects my learning process and contributions to a real-world codebase using Foundry.

In-depth documentation is available at [docs.sablier.com](https://docs.sablier.com).

## Background

Sablier Lockup is a token distribution protocol that enables onchain vesting and airdrops. Our flagship model is the
linear stream, which distributes tokens on a continuous, by-the-second basis.

The way it works is that the sender of a payment stream first deposits a specific amount of ERC-20 tokens in a contract.
Then, the contract progressively allocates the funds to the recipient, who can access them as they become available over
time. The payment rate is influenced by various factors, including the start and end times, as well as the total amount
of tokens deposited.

## Install

### Node.js

This is the recommended approach.

Install Lockup using your favorite package manager, e.g., with Bun:

```shell
bun add @sablier/lockup
```

Then, if you are using Foundry, you need to add these to your `remappings.txt` file:

```text
@sablier/lockup/=node_modules/@sablier/lockup/
@openzeppelin/contracts/=node_modules/@openzeppelin/contracts/
@prb/math/=node_modules/@prb/math/
```

### Git Submodules

This installation method is not recommended, but it is available for those who prefer it.

First, install the submodule using Forge:

```shell
forge install --no-commit sablier-labs/lockup
```

Second, install the project's dependencies:

```shell
forge install --no-commit OpenZeppelin/openzeppelin-contracts@v5.0.2 PaulRBerg/prb-math@v4.1.0
```

Finally, add these to your `remappings.txt` file:

```text
@sablier/lockup/=lib/lockup/
@openzeppelin/contracts/=lib/openzeppelin-contracts/contracts/
@prb/math/=lib/prb-math/
```

### Branching Tree Technique

You may notice that some test files are accompanied by `.tree` files. This is because we are using Branching Tree
Technique and [Bulloak](https://bulloak.dev/).

## Usage

This is just a glimpse of Sablier Lockup. For more guides and examples, see the
[documentation](https://docs.sablier.com).

```solidity
import { ISablierLockup } from "@sablier/lockup/src/interfaces/ISablierLockup.sol";

contract MyContract {
  ISablierLockup lockup;

  function buildSomethingWithSablier() external {
    // ...
  }
}
```

## Architecture

Lockup uses a singleton-style architecture, where all streams are managed in the `SablierLockup` contract. That is,
Sablier does not deploy a new contract for each distribution model or stream. It bundles all streams into a single
contract, which is more gas-efficient and easier to maintain.

For more information, see the [Technical Overview](https://docs.sablier.com/reference/overview) in our docs, as well as
these [diagrams](https://docs.sablier.com/reference/lockup/diagrams).

## Deployments

The list of all deployment addresses can be found [here](https://docs.sablier.com/guides/lockup/deployments). For
guidance on the deployment scripts, see the [Deployments wiki](https://github.com/sablier-labs/lockup/wiki/Deployments).

## Security

The codebase has undergone rigorous audits by leading security experts from Cantina, as well as independent auditors.
For a comprehensive list of all audits conducted, please click [here](https://github.com/sablier-labs/audits).

For any security-related concerns, please refer to the [SECURITY](./SECURITY.md) policy. This repository is subject to a
bug bounty program per the terms outlined in the aforementioned policy.

## Contributing

Feel free to dive in! [Open](https://github.com/sablier-labs/lockup/issues/new) an issue,
[start](https://github.com/sablier-labs/lockup/discussions/new) a discussion or submit a PR. For any informal concerns
or feedback, please join our [Discord server](https://discord.gg/bSwRCwWRsT).

For guidance on how to create PRs, see the [CONTRIBUTING](./CONTRIBUTING.md) guide.

## License

The primary license for Sablier Lockup is the Business Source License 1.1 (`BUSL-1.1`), see
[`LICENSE.md`](./LICENSE.md). However, there are exceptions:

- All files in `src/interfaces/` and `src/types` are licensed under `GPL-3.0-or-later`, see
  [`LICENSE-GPL.md`](./LICENSE-GPL.md).
- Several files in `src`, `script`, and `tests` are licensed under `GPL-3.0-or-later`, see
  [`LICENSE-GPL.md`](./LICENSE-GPL.md).
- Many files in `tests/` remain unlicensed (as indicated in their SPDX headers).
