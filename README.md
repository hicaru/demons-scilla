# Demons contracts.

Contracts:
  * [Main ZRC1](https://github.com/hicaru/demons-scilla/blob/master/ZRC1/nft-demons.scilla)
  * [Main DMZ ZRC2](https://github.com/hicaru/demons-scilla/blob/master/ZRC2/dmz.scilla)
  * [Auction](https://github.com/hicaru/demons-scilla/tree/master/auction)
  * [claim DMZ](https://github.com/hicaru/demons-scilla/tree/master/claim)
  * [crowd-sale](https://github.com/hicaru/demons-scilla/tree/master/crowd-sale)
  * [lvl-up](https://github.com/hicaru/demons-scilla/tree/master/lvl)
  * [name-change](https://github.com/hicaru/demons-scilla/tree/master/name-change)
  * [market-place](https://github.com/hicaru/demons-scilla/tree/master/market-place)

# Deploy

### 1: [Deploy Main ZRC1 contract:](https://github.com/hicaru/demons-scilla/blob/master/ZRC1/nft-demons.scilla)

Init:
```json
[
    {
        "type": "ByStr20",
        "value": "0x119929d8c388DE3650Ea1B3DC7b9Fe0ceEFE862F",
        "vname": "contract_owner"
    },
    {
        "type": "String",
        "value": "Demons",
        "vname": "name"
    },
    {
        "type": "String",
        "value": "DEM",
        "vname": "symbol"
    }
]
```
=> "0xeb9b2acf86d52c900fc01852bb351ebc91c96f38"

### 2: [Deploy Main ZRC2 (DMZ) contract:]((https://github.com/hicaru/demons-scilla/blob/master/ZRC2/dmz.scilla))

Init:
```json
[
    {
        "type": "ByStr20",
        "value": "0x119929d8c388DE3650Ea1B3DC7b9Fe0ceEFE862F",
        "vname": "contract_owner"
    },
    {
        "type": "String",
        "value": "Demon",
        "vname": "name"
    },
    {
        "type": "String",
        "value": "DMZ",
        "vname": "symbol"
    },
    {
        "type": "Uint32",
        "value": "18",
        "vname": "decimals"
    },
    {
        "type": "Uint128",
        "value": "1000000000000000000000000",
        "vname": "init_supply"
    }
]
```
=> "0xda914bcb7ad629b0ba3f84b33ab668faa4519ca0"

### 3: [Deploy Claim DMZ rewards contract:](https://github.com/hicaru/demons-scilla/tree/master/claim)

Init:
```json
[
    {
        "type": "ByStr20",
        "value": "0x119929d8c388DE3650Ea1B3DC7b9Fe0ceEFE862F",
        "vname": "contract_owner"
    },
    {
        "type": "ByStr20",
        "value": "0xda914bcb7ad629b0ba3f84b33ab668faa4519ca0",
        "vname": "dmz"
    },
    {
        "type": "ByStr20",
        "value": "0xeb9b2acf86d52c900fc01852bb351ebc91c96f38",
        "vname": "main"
    }
]
```
=> "0x1a490d1a57caacc6d231051a396215b4e433f949"

After deploy you need send some `DMZ` tokens to this contract, this tokens will be useing as rewards.
example: [viewblock](https://viewblock.io/zilliqa/tx/0x9e32146bdf76326977afbd79de2160017eb20f9ee668e52745eaa989fdd5b229?network=testnet)

### 4: [Deploy CrowdSale contract:](https://github.com/hicaru/demons-scilla/tree/master/crowd-sale)

Init:
```json
[
    {
        "type": "ByStr20",
        "value": "0x119929d8c388DE3650Ea1B3DC7b9Fe0ceEFE862F",
        "vname": "contract_owner"
    },
    {
        "type": "ByStr20",
        "value": "0x4ef291cEbD95ab4231eB52b02Cdf0E231Eab565a",
        "vname": "wallet"
    },
    {
        "type": "ByStr20",
        "value": "0x1a490d1a57caacc6d231051a396215b4e433f949",
        "vname": "distributor"
    },
    {
        "type": "ByStr20",
        "value": "0xeb9b2acf86d52c900fc01852bb351ebc91c96f38",
        "vname": "main"
    }
]
```
=> "0xa8c7405241ade8cb289e540568648acd1c014c24"

On the contract `Claim DMZ rewards` need call method `SetCrowdSale` with `address` = "0xa8c7405241ade8cb289e540568648acd1c014c24".
example: [viewblock](https://viewblock.io/zilliqa/tx/0xb442e9058531c95f8f7f7f0a3a137da1eb5cdaab9def6da8cb6b1def3a833024?network=testnet)


Also this CrowdSale contract should be minter, you need call on `Main` contract need call `ConfigureMinter` with `minter` = "0xa8c7405241ade8cb289e540568648acd1c014c24"
example: [viewblock](https://viewblock.io/zilliqa/tx/0x9b92b7e58d8a75d736f03d9358f68478ddeca9167545cb053ccb2b781f03eb8b?network=testnet)

### 5: [Deploy NameChange contract:](https://github.com/hicaru/demons-scilla/tree/master/name-change)

Init:
```json
[
    {
        "type": "ByStr20",
        "value": "0x119929d8c388DE3650Ea1B3DC7b9Fe0ceEFE862F",
        "vname": "contract_owner"
    },
    {
        "type": "ByStr20",
        "value": "0x4ef291cEbD95ab4231eB52b02Cdf0E231Eab565a",
        "vname": "wallet"
    },
    {
        "type": "ByStr20",
        "value": "0xda914bcb7ad629b0ba3f84b33ab668faa4519ca0",
        "vname": "dmz"
    },
    {
        "type": "ByStr20",
        "value": "0xeb9b2acf86d52c900fc01852bb351ebc91c96f38",
        "vname": "main"
    }
]
```
=> "0x1091f96a72677c8bea1cae379eeac8713a6e6ea6"

Also this NameChange contract should be minter, you need call on `Main` contract need call `ConfigureMinter` with `minter` = "0x1091f96a72677c8bea1cae379eeac8713a6e6ea6"
example: [viewblock](https://viewblock.io/zilliqa/tx/a3ffafabe603b299b92a43137f49acdadca5da58e40c214a222885004dd89888?network=testnet)

### 6: [Deploy level-up contract:](https://github.com/hicaru/demons-scilla/tree/master/lvl)

Init:
```json
[
    {
        "type": "ByStr20",
        "value": "0x119929d8c388DE3650Ea1B3DC7b9Fe0ceEFE862F",
        "vname": "contract_owner"
    },
    {
        "type": "ByStr20",
        "value": "0x4ef291cEbD95ab4231eB52b02Cdf0E231Eab565a",
        "vname": "wallet"
    },
    {
        "type": "ByStr20",
        "value": "0xda914bcb7ad629b0ba3f84b33ab668faa4519ca0",
        "vname": "dmz"
    },
    {
        "type": "ByStr20",
        "value": "0xeb9b2acf86d52c900fc01852bb351ebc91c96f38",
        "vname": "main"
    }
]
```
=> "0xa58bbeb4207205339dd24e2a430841b4bcc3b5a7"

Also this level-up contract should be minter, you need call on `Main` contract need call `ConfigureMinter` with `minter` = "0x1091f96a72677c8bea1cae379eeac8713a6e6ea6"
example: [viewblock](https://viewblock.io/zilliqa/tx/4665571b18bdb0acad2f105212aea77217b35add8ef064db15c6a0efa810fbf8?network=testnet)

### 7: [Deploy Auctino contract:](https://github.com/hicaru/demons-scilla/tree/master/auction)

Init:
```json
[
    {
        "type": "ByStr20",
        "value": "0x119929d8c388DE3650Ea1B3DC7b9Fe0ceEFE862F",
        "vname": "contract_owner"
    },
    {
        "type": "ByStr20",
        "value": "0x4ef291cEbD95ab4231eB52b02Cdf0E231Eab565a",
        "vname": "wallet"
    },
    {
        "type": "ByStr20",
        "value": "0xeb9b2acf86d52c900fc01852bb351ebc91c96f38",
        "vname": "main"
    }
]
```
=> "0x8550c1f62f4a40081600a6986c6e420a75ebdece"

### 7: [Deploy MarketPlace contract:](https://github.com/hicaru/demons-scilla/tree/master/market-place)

Init:
```json
[
    {
        "type": "ByStr20",
        "value": "0x119929d8c388DE3650Ea1B3DC7b9Fe0ceEFE862F",
        "vname": "contract_owner"
    },
    {
        "type": "ByStr20",
        "value": "0x4ef291cEbD95ab4231eB52b02Cdf0E231Eab565a",
        "vname": "wallet"
    },
    {
        "type": "ByStr20",
        "value": "0xeb9b2acf86d52c900fc01852bb351ebc91c96f38",
        "vname": "main"
    }
]
```
=> "0x728f6affcdcf5fb8d9b13879c90ce9a4491a7e81"
