[![js-semistandard-style](https://img.shields.io/badge/code%20style-semistandard-brightgreen.svg?style=flat-square)](https://github.com/standard/semistandard)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)

# Local Signing Manager

Polymesh SDK compatible signing manager that stores private keys in memory.

## Usage

```typescript
import { LocalSigningManager } from '@polymeshassociation/local-signing-manager';
import { Polymesh } from '@polymeshassociation/polymesh-sdk';

const mnemonic = 'upper bundle acid isolate mechanic crunch regular reject please foot immune decrease'

// setup
const signingManager = await LocalSigningManager.create({
  accounts: [
    {
      mnemonic,
    },
    {
      mnemonic,
    /*
     (optional) `derivationPath` is an advanced option which allows for multiple accounts to be derived from one secret. This allows for distinct accounts to be used publicly while limiting the amount of mnemonics that need to be secured.

     A path is composed of alpha numeric segments and are separated by a combination of `/` for "soft" and `//` for "hard" derivations. e.g. `//1/2`

     A "soft" derivation (e.g. '/1') allows the derived private key to recover the original secret and for the derived account to be linked with the initial account.

     A "hard" derivation (e.g. '//1') will generate an account that appears separate is generally recommended

     More details can be found in the [polkadot derivation docs](https://wiki.polkadot.network/docs/learn-account-advanced#derivation-paths)

     For example a scheme `//a//b/c` can be used where:
       - `a` is the application id
       - `b` is the customer id
       - `c` is an account id
     */
      derivationPath: '//1//2/3'
    },
  ],
});

const polymesh = await Polymesh.connect({
  nodeUrl,
  signingManager,
});
```
