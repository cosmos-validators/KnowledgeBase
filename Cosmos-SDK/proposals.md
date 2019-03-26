



#### Voting on proposals

Argument: `<vote>`
* `yes`
* `no`
* `no_with_veto`
* `abstain`

Argument: `<proposal_id>`
* `ID` can be discovered with `gaiacli query gov proposals` command

Argument: `<account_name>`
* `NAME` can be discovered with `gaiacli keys list` command

```
gaiacli tx gov vote <proposal_id> <vote> --from=<account_name> --chain-id=cosmoshub-1 --fees=50000uatom
```






