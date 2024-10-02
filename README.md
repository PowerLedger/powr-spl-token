<p align="center">
  <a href="https://powerledger.io">
    <img alt="powr" src="https://raw.githubusercontent.com/PowerLedger/powr-spl-token/19ca2175db07ab9df9b5477eb28d369300ca6025/powr-logo.png" width="250" />
  </a>
</p>

# POWR spl-token

POWR tokens on Solana

## POWR token address on Solana mainnet-beta: POWR...

[solanafm:POWR...](https://solana.fm/address/POWR.../transactions?cluster=mainnet-alpha)

[solscan:POWR...](https://solscan.io/token/POWR...)

[explorer:POWR...](https://explorer.solana.com/address/POWR...)

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
# -------------------------------------------------------
% spl-token create-token \
--program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb \
--enable-metadata \
--decimals 6 \
--enable-confidential-transfers manual \
--transfer-hook randh9AtTKEKB6nMXjH7874Fp5o2pzbQhRGHmei4rBM \
./keypairs/POWR....json
Creating token POWR... under program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb

To initialize metadata inside the mint, please run `spl-token initialize-metadata POWR... <YOUR_TOKEN_NAME> <YOUR_TOKEN_SYMBOL> <YOUR_TOKEN_URI>`, and sign with the mint authority.

Address:  POWR...
Decimals:  6

Signature: ...

# -------------------------------------------------------
% spl-token display POWR...

SPL Token Mint
  Address: POWR...
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
    Metadata address: POWR...

# -------------------------------------------------------
% spl-token set-transfer-hook --disable POWR...
Setting Transfer Hook Program id for POWR... to disabled

Signature: ...

# -------------------------------------------------------
% spl-token initialize-metadata POWR... 'Powerledger' 'POWR' 'https://raw.githubusercontent.com/PowerLedger/powr-spl-token/refs/heads/main/powr_metadata.json'

Signature: ...

# -------------------------------------------------------
% spl-token display POWR...

SPL Token Mint
  Address: POWR...
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
    Metadata address: POWR...
  Metadata:
    Update Authority: initJDrFFiBjjrEmUvAN5oSQF9YT2os3tGvbfZbGWHV
    Mint: POWR...
    Name: Powerledger
    Symbol: POWR
    URI: https://raw.githubusercontent.com/PowerLedger/powr-spl-token/refs/heads/main/powr_metadata.json
```
