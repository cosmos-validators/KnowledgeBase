

#### Changing Validator Description

Argument: `<account_name>`
* `NAME` can be discovered with `gaiacli keys list` command

```

gaiacli tx staking edit-validator --moniker="Bity.com" \
  --website="https://cosmos.network" \
  --identity=6A013095E83CC0F4 \
  --details="We offer professional, secure, and reliable crypto staking services for investors looking to stake their coins with trusted third parties, such as the Cosmos Network." \
  --chain-id=cosmoshub-1 \
  --gas="auto" \
  --gas-prices="0.025uatom" \
  --from=<key_name> \
  --commission-rate="0.19"
  
  ```



