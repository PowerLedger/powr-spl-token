<p align="center">
  <a href="https://powerledger.io">
    <img alt="powr" src="https://raw.githubusercontent.com/PowerLedger/powr-spl-token/19ca2175db07ab9df9b5477eb28d369300ca6025/powr-logo.png" width="250" />
  </a>
</p>

# POWR spl-token

POWR tokens on Solana

## POWR token address on Solana mainnet-beta: PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR

[solanafm:PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR](https://solana.fm/address/PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR/transactions?cluster=mainnet-alpha)

[solscan:PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR](https://solscan.io/token/PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR)

[explorer:PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR](https://explorer.solana.com/address/PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR)

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

# Update Token Mint authority address
spl-token authorize <TOKEN_MINT_ADDRESS> mint <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> confidential-transfer-mint <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> confidential-transfer-fee <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> transfer-hook-program-id <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> metadata-pointer <auth... .json>_ADDRESS
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
./keypairs/PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR.json
Creating token PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR under program TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb

To initialize metadata inside the mint, please run `spl-token initialize-metadata PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR <YOUR_TOKEN_NAME> <YOUR_TOKEN_SYMBOL> <YOUR_TOKEN_URI>`, and sign with the mint authority.

Address:  PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR
Decimals:  6

Signature: g42Tf7BcbQmvn2ntNADXTByLCMA2jRM7Jd3nDEX9Wv7iFtzT8LTThgAfu6Y1Y2XYGQSU145kpfJjZ9pHZFyYX46

# -------------------------------------------------------
% spl-token display PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR

SPL Token Mint
  Address: PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR
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
    Metadata address: PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR

# -------------------------------------------------------
% spl-token set-transfer-hook --disable PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR
Setting Transfer Hook Program id for PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR to disabled

Signature: 5aQEgSTMuWTsggiYFU4aoasYMwpjDxJhYPox6SFRkhMf5uNYSAjBemkJAZfdTGAzqjemds9o9d1MTwyqrHtrgGBd

# -------------------------------------------------------
% spl-token initialize-metadata PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR 'Powerledger' 'POWR' 'https://raw.githubusercontent.com/PowerLedger/powr-spl-token/refs/heads/main/powr_metadata.json'

Signature: 4XgxaTG6mig7jpUq7VjwQ29BXMzNLhSCuyGTWeVBKhWqh5iuj4xX2VWgya87BmP5XDjT56MZnYu9MZPXPG3L2wKB

# -------------------------------------------------------
% spl-token display PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR

SPL Token Mint
  Address: PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR
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
    Metadata address: PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR
  Metadata:
    Update Authority: initJDrFFiBjjrEmUvAN5oSQF9YT2os3tGvbfZbGWHV
    Mint: PWrRWNTMkccctdiJEs6kEFNDgTAV8rQzhT2afckW1gR
    Name: Powerledger
    Symbol: POWR
    URI: https://raw.githubusercontent.com/PowerLedger/powr-spl-token/refs/heads/main/powr_metadata.json
```
