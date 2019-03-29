

## Testnet experimentations

Testnet Genesis Files can be found [HERE](https://github.com/cosmos/testnets)

Validators Chat can be found in [HERE](https://riot.im/app/#/room/#cosmos-validators:matrix.org)

### Quick Setup

```
rm $HOME/.gaiad/config/addrbook.json $HOME/.gaiad/config/genesis.json

gaiad unsafe-reset-all

cd $GOPATH/src/github.com/cosmos/cosmos-sdk

git fetch --all && git checkout master

make update_tools install

gaiad init Bity.com

```

Copy genesis file, define seed nodes and set testnet property to latest testnet genesis file folder name

```
mkdir -p $HOME/.gaiad/config

testnet=gaia-13k
curl https://raw.githubusercontent.com/cosmos/testnets/master/$testnet/genesis.json > $HOME/.gaiad/config/genesis.json

nano ~/.gaiad/config/config.toml
```


set `seeds` property according ot latest [Testnet Get Started Status List](https://github.com/cosmos/testnets#testnet-status) for example


seeds = "c24f496b951148697f8a24fd749786075c128f00@35.203.176.214:26656"

To save changes: **Ctrl+O, [Enter], Ctrl+X**

Start a Full Node

```
mkdir -p $HOME/logs
nohup gaiad start &> $HOME/logs/gaiad.log &

#to preview loggs
tail -n 100 $HOME/logs/gaiad.log
```

To generate a bip32 seed you can use [Mnemonic Code Converter](https://iancoleman.io/bip39/) in order to persist a single key between different testnets. After clicking "GENERATE" button you will be presented with random 12 words you can use for the gaiacli keys add command, for example.

`bright flee spell nature unfold anchor govern envelope solve exercise flower fine`

Additionally you will have to set a minimum of 8 character password, for example: `12345678`

```
gaiacli keys add ValidatorKey --recover
```

You should expect output to resemble following

```
NAME:   TYPE:   ADDRESS:                                        PUBKEY:
ValidatorKey    local   cosmos1zmw9kwmldgxt8czg0csuqnr4j8syls5jn0njqm   cosmospub1addwnpepqg6l93rcut0j9fjjd93lr6u3rkppkwc6vtpd6mljxtshxnus8jwhg9uv30z
```

Use [Public Faucet](https://hubble.figment.network/chains/gaia-13002/faucet), use it to redeem testnet tokens to your address, in our case: 

`cosmos1zmw9kwmldgxt8czg0csuqnr4j8syls5jn0njqm`

As testnet explorer [Hubble](https://hubble.figment.network/chains/gaia-13002) can be used, a single atom is generally enough to join network as validator.

Configure gaiacli


```
gaiacli config trust-node true

gaiacli config chain-id $(cat $HOME/.gaiad/config/genesis.json | jq -r '.chain_id')

gaiacli config node tcp://localhost:26657

```

Query balance and block height

```
gaiacli status | jq -r '.sync_info.latest_block_height'

gaiacli query account cosmos1zmw9kwmldgxt8czg0csuqnr4j8syls5jn0njqm

```

If you see message similar to 
```
ERROR: {"codespace":"sdk","code":9,"message":"account cosmos1zmw9kwmldgxt8czg0csuqnr4j8syls5jn0njqm does not exist"}
```

It means you might have not synced to the latest block yet and do not have any ATOMS as per visible blockchain state.


Find out validator public key

cat $HOME/.gaiad/config/priv_validator_key.json | jq -r '.pub_key.value'

In our case output resulted in following response: `2fB28TlrPvwoddrlan7xUwp1635XSSmm/+RzVLLtsTA=`






























