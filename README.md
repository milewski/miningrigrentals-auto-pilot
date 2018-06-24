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

in order for this software to work you must generate an `api key` and `secret`, this can be generated here: `https://www.miningrigrentals.com/account/apikey`, ONLY SELECT `Manage Rigs` permission.

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
./mmr-pilot.exe --config config.json --fee 10
```

# Miner config

You will need to use your own miner in order to use this software, all you need to do is create a new folder inside the `miners` and setup a `config.json` inside, this is a sample of a config:

```json
{
  "binaryPath": "./bin/ccminer.exe",
  "algorithms": [
    "xevan",
    "lyra2rev2",
    "c11",
    "blake2s"
  ],
  "configFile": {
    "algo": "{algorithm}",
    "intensity": 20,
    "url": "stratum+tcp://{url}:{port}",
    "user": "{worker}",
    "pass": "{password}"
  },
  "params": [
    "-c",
    "{configPath}"
  ]
}
```

here is a list of all the placeholders you can use to setup the miner config:

`algorithm`, `url`, `port`, `worker`, `password`, `configPath`

the params property will be given directly to your miner binary so the above configuration will output:

```bash
./bin/ccminer.exe -c ./temp/lyra2rev2.json
```

#### Note

The current version has a small dev fee of 3% that will only ever run when your rig is not rented.

### Donation address

BTC `3QJTxhufh7j5TnZ2fQJbQiX9VNuPuG5oS6`
LTC `LhfsbV5iXnBzJYvRJXSDhE2fKtQCUMimAY`
