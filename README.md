# MiningRentalAutoPilot

# What is this?

This software will automatically advertise your rig in every supported algo available on [https://www.miningrigrentals.com/](https://www.miningrigrentals.com/)

Currently the supported algos are: `lyra2rev2`, `equihash`, `neoscrypt`, `blake2s`, `nist5`, `x16r`, `x16s`, `x17`, `c11`, `xevan`, `phi1612`, `phi2`, `allium`, `lyra2z`, `tribus`, `timetravel`, `hashimotos`, `zhash`

Once one of your rig is rented, it automatically un-list all your non-rented miners, and once the rental is done, put them all back in.

# Features

- Detect when someone rent and auto toggle off all the active miners but the rented one
- Auto adjust your miner price with given min/max auto calculated based on your advertised hashrate
- Auto restart miner if it hangs or crash

# Config

```json
{
  "api_key": "",
  "api_secret": "",
  "minBTCPrice": "0.0015000",
  "priceModifier": 5,
  "enableLTC": true,
  "fee": 2,
  "rigs": {
    "lyra2rev2": {
      "priceModifier": -10,
      "minBTCPrice": 0.00002500,
      "details": {
        "minhours": 24,
        "maxhours": 720,
        "name": "Monitored Lyra Rig - Best price on the market"
      },
      "pools": [
        {
          "host": "lyra2rev2.mine.zpool.ca",
          "port": 4533,
          "user": "YOUR_BTC_ADDRESS",
          "pass": "c=LTC,d=64"
        },
        {
          "host": "lyra2rev2.hk.nicehash.com",
          "port": 3347,
          "user": "USERNAME",
          "pass": "x"
        }
      ]
    },
    "neoscrypt": {
      "minRentalPrice": 0.00050000,
      "pools": [
        {
          "host": "neoscrypt.mine.zpool.ca",
          "port": 4233,
          "user": "BTC_ADDRESS",
          "pass": "c=BTC"
        }
      ]
    }
  },
  "rigDetails": {
    "minhours": 3,
    "maxhours": 720,
    "extensions:": true,
    "name": "Super Cool Rig / Monitored 24h"
  }
}

```

# Usage 

```bash
./mmr-pilot.exe --config config.json
```
