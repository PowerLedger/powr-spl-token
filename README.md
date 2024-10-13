<p align="center">
  <a href="https://powerledger.io">
    <img alt="powr" src="https://raw.githubusercontent.com/PowerLedger/powr-spl-token/19ca2175db07ab9df9b5477eb28d369300ca6025/powr-logo.png" width="250" />
  </a>
</p>

# POWR spl-token

POWR tokens on Solana

## POWR token address on Solana mainnet-beta: POWR...

[solanafm:PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w](https://solana.fm/address/PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w/transactions?cluster=mainnet-alpha)

[solscan:PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w](https://solscan.io/token/PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w)

[explorer:PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w](https://explorer.solana.com/address/PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w)

## spl-token commands for deployment of POWR on Solana

``` bash
# Set default keypair and mainnet-beta env
solana config set -k <PATH TO DEFAULT AUTH KEYPAIR>

# mainnet-beta
solana config set -um

# Create Mint (transfer-hook is using a random wallet that later is disabled)
spl-token create-token \
--program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb \
--enable-metadata \
--decimals 6 \
--enable-confidential-transfers manual \
--transfer-hook <RANDOM_ADDRESS> \
<TOKEN_MINT_ADDRESS>.json

# Display Mint properties
spl-token display <TOKEN_MINT_ADDRESS>

# Disable transfer hook
spl-token set-transfer-hook --disable <TOKEN_MINT_ADDRESS>

# Initialize metadata (Check where to store the metadata json file, IPFS?)
spl-token initialize-metadata <TOKEN_MINT_ADDRESS> 'Powerledger' 'POWR' 'https://raw.githubusercontent.com/PowerLedger/powr-spl-token/refs/heads/main/powr_metadata.json'

# Update metadata IF NEEDED
# spl-token update-metadata <TOKEN_MINT_ADDRESS> niceness 100%

# Generate keypairs for the first mint recipient
solana-keygen grind --starts-with init:1

# Create an ATA for the mint of the initial supply
spl-token create-account <TOKEN_MINT_ADDRESS> init... .json 
# OR. --owner <OWNER_ADDRESS> Address of the primary authority controlling a mint or account. Defaults to the client keypair address.
spl-token create-account <TOKEN_MINT_ADDRESS> init... .json --owner <PATH TO AUTH KEYPAIR>

# Check balance
spl-token balance --address init... .json

# Mint some tokens (how many?)
spl-token mint <TOKEN_MINT_ADDRESS> <AMOUNT> <RECIPIENT_TOKEN_ACCOUNT_ADDRESS (init... .json)>

# Send some tokens as test
spl-token transfer <TOKEN_MINT_ADDRESS> <AMOUNT> <RECIPIENT_TOKEN_ACCOUNT_ADDRESS (???... .json)>  --owner <init... .json>

# Update Token Mint authority addresses
spl-token authorize <TOKEN_MINT_ADDRESS> mint <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> confidential-transfer-mint <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> confidential-transfer-fee <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> transfer-hook-program-id <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> metadata-pointer <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> metadata <auth... .json>_ADDRESS

spl-token authorize <TOKEN_MINT_ADDRESS> freeze <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> owner <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> close <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> close-mint <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> transfer-fee-config <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> withheld-withdraw <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> interest-rate <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> permanent-delegate <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> group-pointer <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> group-member-pointer <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> group <auth... .json>_ADDRESS
```

## deployment logs

``` bash
# Create mint
user@hostname ~ % spl-token create-token \
--program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb \
--enable-metadata \
--decimals 6 \
--enable-confidential-transfers manual \
--transfer-hook randh9AtTKEKB6nMXjH7874Fp5o2pzbQhRGHmei4rBM \
./keypairs/PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w.json
Creating token PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w under program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
To initialize metadata inside the mint, please run `spl-token initialize-metadata PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w <YOUR_TOKEN_NAME> <YOUR_TOKEN_SYMBOL> <YOUR_TOKEN_URI>`, and sign with the mint authority.

Address:  PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w
Decimals:  6

Signature: 3ZVBcKd5jeJReUCKMbRcEVaDz2kX43yNeeGRwm9jKVArPJy6rfhRFpTEETNMMt2K1C8fj3PUkRCe3PfVgPueWxTF

# Display mint extensions
user@hostname ~ % spl-token display PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w

SPL Token Mint
  Address: PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w
  Program: TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
  Supply: 0
  Decimals: 6
  Mint authority: initJDrFFiBjjrEmUvAN5oSQF9YT2os3tGvbfZbGWHV
  Freeze authority: (not set)
Extensions
  Confidential transfer:
    Authority: initJDrFFiBjjrEmUvAN5oSQF9YT2os3tGvbfZbGWHV
    Account approve policy: manual
    Audit key: audits are disabled
  Transfer Hook:
    Authority: initJDrFFiBjjrEmUvAN5oSQF9YT2os3tGvbfZbGWHV
    Program Id: randh9AtTKEKB6nMXjH7874Fp5o2pzbQhRGHmei4rBM
  Metadata Pointer:
    Authority: initJDrFFiBjjrEmUvAN5oSQF9YT2os3tGvbfZbGWHV
    Metadata address: PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w

# Disable transfer hook
user@hostname ~ % spl-token set-transfer-hook --disable PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w
Setting Transfer Hook Program id for PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w to disabled

Signature: 3FFbwNzBx62N1CUnebx4EEGrvND4b8NmZmf4p2G3ZCHoQ5bsGL5eFobnYqDvDnGRfPQWtudWrDWgu5NAdf52UU9c

# Initialize metadata
user@hostname ~ % spl-token initialize-metadata PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w 'Powerledger' 'POWR' 'https://raw.githubusercontent.com/PowerLedger/powr-spl-token/refs/heads/main/powr_metadata.json'

Signature: 4eg9oQPVqfWqrPP3nwewW5kNA57AjxQU3pZ3btBDJxCNMNZhZxpfbwfu8TNpQ6bvndxLAVju4thzwwzAosEKtbCE

# Display mint
user@hostname ~ % spl-token display PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w

SPL Token Mint
  Address: PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w
  Program: TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
  Supply: 0
  Decimals: 6
  Mint authority: initJDrFFiBjjrEmUvAN5oSQF9YT2os3tGvbfZbGWHV
  Freeze authority: (not set)
Extensions
  Confidential transfer:
    Authority: initJDrFFiBjjrEmUvAN5oSQF9YT2os3tGvbfZbGWHV
    Account approve policy: manual
    Audit key: audits are disabled
  Transfer Hook:
    Authority: initJDrFFiBjjrEmUvAN5oSQF9YT2os3tGvbfZbGWHV
    Program Id: Disabled
  Metadata Pointer:
    Authority: initJDrFFiBjjrEmUvAN5oSQF9YT2os3tGvbfZbGWHV
    Metadata address: PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w
  Metadata:
    Update Authority: initJDrFFiBjjrEmUvAN5oSQF9YT2os3tGvbfZbGWHV
    Mint: PowerQT5bz29ch1ABYDeBhmp9CJM63kAmqgVP41ko4w
    Name: Powerledger
    Symbol: POWR
    URI: https://raw.githubusercontent.com/PowerLedger/powr-spl-token/refs/heads/main/powr_metadata.json
```
