# Colored Coins Full Node

## Introduction
This repository is a collection of systems required for a Colored Coins "Full Node", all packaged together to run via Docker.
They come preconfigured so that you can easily run the full stack, without having to install and configure each component separately.

## Services
**Coloredcoinsd** - An API to create Colored Coins transactions. Use the *Block Explorer* for UTXO data.

**Block Explorer** - This service parses the bitcoin blockchain for all Colored Coins transactions, and exposes an API that allows querying the current state.

**MongoDB** - Stores data for the *Block Explorer*.

## Note on parsing optimizations
The *Block Explorer*'s parser is not optimized, and we're planning major improvements to the way it works. However, for now parsing is pretty slow - around 2 weeks to parse the *mainnet* chain, or 1-2 days to parse *testnet*. Space requirements are also not optimized yet (but will be!): *mainnet* requires around *2TB* and *testnet* around *200GB*.

## Requirements
**Disk space**: *1.3TB* for mainnet, *200GB* for testnet (as of January 2017). This doesn't include the space required for Bitcoin Core (not included).

**RAM**: 8GB+

**OS**: Tested mainly on Ubuntu Linux 16.04, should work on Windows and macOS as well, but not supported.

**Bitcoin Core**: Also required is a synced-up Bitcoin Core client. We do not currently include this in that package as we assume most users will already be running one. You should use the following `bitcoin.conf` file:
```
server=1
rpcuser=USER
rpcpassword=PASSWORD
txindex=1
```
You may also add `testnet=1` if using testnet (also see note in `Configuration`). If you already have a synced Bitcoin Core client, but you are now adding `txindex` which wasn't on before, you'll have to use the `-reindex` flag the first time you run Bitcoin Core again. You may either use `bitcoind` or the Bitcoin Core GUI (but we recommend `bitcoind`).

**Docker**: You should install `docker` and `docker-compose`. Use the following instructions: https://docs.docker.com/compose/install/

## Installing
Simply clone this repository.

## Configuration
You should configure the *coloredcoinsd* and *Block Explorer* services to use your Bitcoin Core instance:

**In `ccd/var.env`**, change `BITCOIND_HOST`, `BITCOIND_PORT`, `BITCOIND_USER`, and `BITCOIND_PASS` to the correct values.

**In `explorer/var.env`**, change `BITCOINNETWORK`, `BITCOINPORT`, `RPCUSERNAME` and `RPCPASSWORD` to the correct values.

*The variable names are different between the 2 services for legacy reasons. We plan to consolidate them in the future*.

You may also change `PORT` in each of this files to change the port used by each service. By default, the `Block Explorer` is on port 8081, and `coloredcoinsd` is on port 8180.

To use testnet, you should change `NETWORK` in `explorer/var.env` to `testnet`.

## Running
Just `cd` into `compose-apps` and run `docker-compose up -d` to run the node in `detached` mode (or remove the `-d` if you want logs to be printed to the console). You might need to use `sudo`.

## Using
See the [Colored Coins API docs](http://coloredcoins.org/documentation/) for *coloredcoinsd* endpoints.

The *block explorer*'s API isn't fully documented yet, but you can get a good idea of what's possible from its source code:  [GET endpoints](https://github.com/Colored-Coins/Colored-Coins-Block-Explorer/blob/master/routes/GET-public.json) and [POST endpoints](https://github.com/Colored-Coins/Colored-Coins-Block-Explorer/blob/master/routes/POST-public.json).

Remember to use the correct port numbers for each, as defined in the `Configuration` step.

## License

[Apache-2.0](http://www.apache.org/licenses/LICENSE-2.0)
