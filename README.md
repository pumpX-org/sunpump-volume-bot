# Sunpump Launch + Sniper + Volume Bot.

## Getting Started
- Join our [Discord]((https://discord.gg/aTXpGfzVxt)) for more Info.

### Prerequisites

- Node.js and npm installed on your machine (latest versions).
- Tron wallet(s)/Base58 private key.
- TronGrid api key (free or paid plan)

### Installation

1. Download or clone the repository to your local machine.
2. Navigate to the project directory.
3. Install dependencies:
```npm install```

### Usage

1. Run the script:
```npm run start```

### Configuration and Setup


1. Rename `.env.example` to `.env` in the root directory.
- Populate it with the required fields.
- Do not change, add or remove fields but only change their values.


2. Rename `volume-wallets.example.json` to `volume-wallets.json` in the root directory and `sniper-wallets.example.json` to `sniper-wallets.json`.
- Populate the `volume-wallets.json` and `sniper-wallets.json` file with wallet entries.
- Wallet entry:
```json
        {
            "privateKey": "ENTER WALLET BASE58 PRIVATE KEY HERE",
            "trx": 1000,
        },
```
- Do not add a trailing comma at the last entry.


3. Config variables breakdown:
- `TRON_FUNDER_PRIVATE_KEY`: Wallet used for funding wallets to perform cetain operations.
- `TRON_GRID_API_KEY`: Tron grid api key used to authenticate blockchain interactions.
- `CAPSOLVER_API_KEY`: capsolver api key used to solve certain needed recaptcha tasks.
- `ENABLE_LAUNCH_MASS_SNIPER`: option to enable launch mode. These additions apply:
  - `sniper-wallets.json` will be used as the launch sniper wallets
  - metadata will be validated in `assets` folder
  - your Capsolver account will be used to solve captchas (needs minor funding)
  - the first entry in `sniper-wallets.json` will be the dev wallet 
- `BUY_SLIPPAGE`: sets the buy slippage.


4. If `ENABLE_LAUNCH_MASS_SNIPER` is set to `true`: 
- Rename `metadata.example.json` to `metadata.json` in the `assets` directory.
- Populate the `metadata.json` file with the required and optional values.
- Do not change, add or remove fields but only change their values.
- Add an image file in the `assets` directory and name it `image.png|jpeg|jpg|gif (choose only one of the supported extension).`
- Now you can choose the `launch + mass sniper` option in main menu + use `sniper-wallets.json` for all operations aswell (funding/redeeming/selling).



## BreakDown

### General WorkFlow of Volume Task
General workflow of the tool would be:
1. fill in config variables in `.env` file.
2. input initial wallets in `volume-wallets.json` or `sniper-wallets.json` (you can also generate wallets later in-tool).
3. Fund Wallets with configured amount using the fund option (you can overfund them for approvals later).
4. check their balances in-tool to make sure they are funded correctly.
5. choose the prepare/start volume (with standard mode for now) or launch + sniper task option.
6. launch the task, and watch your wallets by up the token.
7. after all buy orders or snipes are done, or before so, you can approve and sell your currently held tokens.
8. rerun the approve or sell option just to make sure.
9. check wallets trx and token balances to confirm that all wallets have sold.
10. use the redeem option to get back all TRX to the original funding wallet.
11. Voila.


### Pointers
- All the transaction in the bot require fees as all transactions in TRON.
- There are some safeguard put in place like leaving behind TRX for buys, approvals and sells.
- due to the nature of the chain, the fees are dynamic and can lead to failures in transactions if they spike.
- there is an emergency fund option to fund all wallets instantly with a spcific amount if thats the case.
- if you using alot of wallets close to the max (30) sometimes but rarely you might encounter rate limits.
- its recommended to get a custom TronGrid plan with a higher rps than the standard 15.



