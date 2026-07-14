**NOTICE:** This is a fork of [@wharfkit/resources](https://www.npmjs.com/package/@wharfkit/resources), adapted for the **VEXANIUM** blockchain.

If you were previously using `@wharfkit/resources`, you can now use `@pixelgeniusid/resources` for full compatibility with VEXANIUM. To update your codebase, remove the `@wharfkit/resources` library and add `@pixelgeniusid/resources`, then replace all imports of `@wharfkit/resources` with `@pixelgeniusid/resources`.

# @pixelgeniusid/resources

Library to assist in Antelope-blockchain resource calculations (RAM, CPU/NET via REX and PowerUp), forked from `@wharfkit/resources` with a configurable system contract account.

## Why this fork exists

`PowerUpAPI`, `RAMAPI`, and `REXAPI` all hardcode `'eosio'` as the account hosting the system contract (`powup.state`, `rammarket`, `rexpool` tables). Some Antelope chains rename this account — VEX uses `vexcore` — which made all three queries fail outright on those chains with no way to override it from the consuming application. This fork adds a `systemAccount` option to the `Resources` constructor (defaults to `'eosio'`, so existing consumers on EOS/Jungle/WAX etc. are unaffected).

```ts
import { Resources } from '@pixelgeniusid/resources'

const resources = new Resources({
    api: myApiClient,
    sampleAccount: 'vex.reserv', // VEX's equivalent of eosio.reserv/greymassfuel/b1
    systemAccount: 'vexcore',    // VEX's system contract account, instead of 'eosio'
})

const powerup = await resources.v1.powerup.get_state() // now queries vexcore, not eosio
```

## Installation

```
yarn add @pixelgeniusid/resources
# or
npm install --save @pixelgeniusid/resources
```

## Usage

See the upstream [@wharfkit/resources](https://github.com/wharfkit/resources) documentation — the API surface is unchanged except for the added `systemAccount` option above.

## Developing

You need [Make](https://www.gnu.org/software/make/), [node.js](https://nodejs.org/en/) and [yarn](https://classic.yarnpkg.com/en/docs/install) installed.

Clone the repository and run `make` to checkout all dependencies and build the project. See the [Makefile](./Makefile) for other useful targets. Before submitting a pull request make sure to run `make lint`.

---

Originally made with ☕️ & ❤️ by [Greymass](https://greymass.com); VEX compatibility fork maintained by pixelgenius-id.
