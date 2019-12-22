# Charity Foundation TON Smart Contract
## Idea
Charity Foundation TON Smart Contract implements simple Foundation model where each incoming payment will be multiplied by specified campaign factor and sent to the destination.

## Build and run

The main Fift-script `foundation.fif` is a entry point that the Foundation owner/administrator should use in the following manner:
```
    $ fift -s foundation.fif <command> <options>
```

`foundation.fif` provides detailed help information to usage.


Notice that you have to set the `FIFTPATH` environment variable to `<source-directory>/crypto/fift/lib:<source-directory>/crypto/smartcont` (of TON distribution) due to some imports, and add into the `PATH` environment variable fift and func compiler paths. For example:
```sh
export FIFTPATH=~/Projects/ton/crypto/fift/lib:~/Projects/ton/crypto/smartcont
export PATH=$PATH:~/Projects/ton-build/crypto
```

`charity-code.fc` contains a source code of the given smart contract. `foundation_init.fif` imports this smart contract code by including `code.fif` which is a generated version by FunC compiler. Note that  the `charity-code.fc` uses `stdlib.fc` functions (which is part of TON distribution), so this file should also be presented.

To recompile FunC source code:
```sh
    $ func -PSR stdlib.fc charity-code.fc -ocode.fif
```

## How user can send gram to the specific campaign?
Smart contract Owner/Administrator must take care of the quality of the charity campaign and then register it.
After that she can publish the user payload file that defines a given charity campaign:
```sh
    $ fift -s foundation.fif payload <campaign-id>
```

This produces a boc-file that user can attach into regular payment. User sends to the fund, and the fund automatically sends multiplied value to the campaign destination.
