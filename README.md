# powr-spl-token
POWR tokens on Solana

## taking PLBS snapshot

```
~/bin/cluster-monitoring/get-powr-deposits-and-withdrawals.js

```

## spl-token commands for deployment of POWR on Solana

``` bash
# Set default keypair and mainnet-beta env
solana config set -k <PATH TO DEFAULT AUTH KEYPAIR>

# devnet
solana config set -ud
# testnet
solana config set -ut
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
spl-token initialize-metadata <TOKEN_MINT_ADDRESS> 'Powerledger' 'POWR' 'https://<GCP BUCKET? IPFS? web3.storage Github??>/metadata.json'

# Update metadata IF NEEDED
# spl-token update-metadata <TOKEN_MINT_ADDRESS> niceness 100%

# Generate keypairs for the first mint recipient
solana-keygen grind --starts-with 1st:1
solana-keygen grind --starts-with 2nd:1
solana-keygen grind --starts-with auth:1

# Create an ATA for the mint of the initial supply
spl-token create-account <TOKEN_MINT_ADDRESS> 1st... .json 
# OR. --owner <OWNER_ADDRESS> Address of the primary authority controlling a mint or account. Defaults to the client keypair address.
spl-token create-account <TOKEN_MINT_ADDRESS> 1st... .json --owner <PATH TO AUTH KEYPAIR>

# Check balance
spl-token balance --address 1st... .json

spl-token create-account <TOKEN_MINT_ADDRESS> 2nd... .json
# OR.
spl-token create-account <TOKEN_MINT_ADDRESS> 2nd... .json --owner <PATH TO AUTH KEYPAIR>

# Check balance
spl-token balance --address 2nd... .json

# Mint some tokens (how many?)
spl-token mint <TOKEN_MINT_ADDRESS> <AMOUNT> <RECIPIENT_TOKEN_ACCOUNT_ADDRESS (1st... .json)>

# Send some tokens as test
spl-token transfer <TOKEN_MINT_ADDRESS> <AMOUNT> <RECIPIENT_TOKEN_ACCOUNT_ADDRESS (2nd... .json)>  --owner <1st... .json>

# Update Token Mint authority address
spl-token authorize <TOKEN_MINT_ADDRESS> mint <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> confidential-transfer-mint <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> confidential-transfer-fee <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> transfer-hook-program-id <auth... .json>_ADDRESS
spl-token authorize <TOKEN_MINT_ADDRESS> metadata-pointer <auth... .json>_ADDRESS
# SPL-TOKEN-DEPLOYMENT ENDS❗️

# MISC
# Note: Token-2022 ATAs are always immutable, ignoring --immutable parameter
# Tokens sent to keywKyugZ26CfuHAPG5HwoFY7oUae5dpBekbMGwk8L5 -> pda (nic9cZWo9pY36sW8MR69zfe5x1AoKxrKFDKZjcF8g8T) -> CR5oLD96JRSfEnAVFoVqjrMYCS8XGjoREersqfWr8DnF
spl-token mint nic9cZWo9pY36sW8MR69zfe5x1AoKxrKFDKZjcF8g8T 100
spl-token create-account nic9cZWo9pY36sW8MR69zfe5x1AoKxrKFDKZjcF8g8T othTVn66nv5SkA37Ww2CDaDDHwQpq26tVsn5U1BSk8K.json --owner owng6D2q582U5uL29hv92nptncCXD65rHsi3BJL5kDJ --fee-payer keywKyugZ26CfuHAPG5HwoFY7oUae5dpBekbMGwk8L5.json
spl-token transfer nic9cZWo9pY36sW8MR69zfe5x1AoKxrKFDKZjcF8g8T 10 othTVn66nv5SkA37Ww2CDaDDHwQpq26tVsn5U1BSk8K --fund-recipient
spl-token create-account nic9cZWo9pY36sW8MR69zfe5x1AoKxrKFDKZjcF8g8T othGqcrHdaRQ5swkS9fVM4GQXubEF4btpXDkW3zx3A1.json --immutable --owner owng6D2q582U5uL29hv92nptncCXD65rHsi3BJL5kDJ --fee-payer keywKyugZ26CfuHAPG5HwoFY7oUae5dpBekbMGwk8L5.json 
spl-token transfer nic9cZWo9pY36sW8MR69zfe5x1AoKxrKFDKZjcF8g8T 15 othGqcrHdaRQ5swkS9fVM4GQXubEF4btpXDkW3zx3A1 --fund-recipient
spl-token transfer nic9cZWo9pY36sW8MR69zfe5x1AoKxrKFDKZjcF8g8T 13 PeoExexcsE4srQCkhhbrHcnA15TaQc994SCGWPnM5uG --fund-recipient

# Proposed JSON metadata for POWR

{
  "name": "Powerledger",
  "symbol": "POWR",
  "description": "Powerledger POWR token expanded on Solana mainnet-beta",
  "image": "https://bafybeieyr6pyt5fqhuzl4cohvcduubssrfszbmw6dve5pbslnb3oopzx2u.ipfs.w3s.link/powr-logo.png"
}

{
  "name": "Powerledger",
  "symbol": "POWR",
  "description": "Powerledger POWR token expanded on Solana mainnet-beta",
  "website": "https://powerledger.io",
  "image": "https://bafybeieyr6pyt5fqhuzl4cohvcduubssrfszbmw6dve5pbslnb3oopzx2u.ipfs.w3s.link/powr-logo.png"
}
```

``` bash
# utils
solana-keygen grind --starts-with tk9:1
solana-keygen new --no-outfile --no-bip39-passphrase
solana-keygen pubkey usb://ledger\?key=0
solana config set -k usb://ledger\?key=0
# Paypal USD (PYUSD)
spl-token display 2b1kV6DkPAnxd5ixfnxCpjxmKwqjjaYmCZfHsFu24GXo -um
```

``` json
{  "name":"PayPal USD",  "symbol":"PYUSD",  "description":"PayPal USD is designed to contribute to the opportunity stablecoins offer for payments and is 100% backed by U.S. dollar deposits, short-term U.S Treasuries and similar cash equivalents. PayPal USD is redeemable 1:1 for U.S. dollars and is issued by Paxos Trust Company.",  "image":"https://424565.fs1.hubspotusercontent-na1.net/hubfs/424565/PYUSDLOGO.png"}

{
  "name": "PayPal USD",
  "symbol": "PYUSD",
  "description": "PayPal USD is designed to contribute to the opportunity stablecoins offer for payments and is 100% backed by U.S. dollar deposits, short-term U.S Treasuries and similar cash equivalents. PayPal USD is redeemable 1:1 for U.S. dollars and is issued by Paxos Trust Company.",
  "image": "https://424565.fs1.hubspotusercontent-na1.net/hubfs/424565/PYUSDLOGO.png"
}
```

``` bash
# PAYPAL USD spl-token
% spl-token display 2b1kV6DkPAnxd5ixfnxCpjxmKwqjjaYmCZfHsFu24GXo -um
SPL Token Mint
  Address: 2b1kV6DkPAnxd5ixfnxCpjxmKwqjjaYmCZfHsFu24GXo
  Program: TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
  Supply: 364063131373881
  Decimals: 6
  Mint authority: 5gUuDFHswKi2QMA1qJHf6FEVhNCrHnyAdfWniMaUUPE4
  Freeze authority: 2apBGMsS6ti9RyF5TwQTDswXBWskiJP2LD4cUEDqYJjk
Extensions
  Close authority: 2apBGMsS6ti9RyF5TwQTDswXBWskiJP2LD4cUEDqYJjk
  Permanent delegate: 2apBGMsS6ti9RyF5TwQTDswXBWskiJP2LD4cUEDqYJjk
  Transfer fees:
    Current fee: 0bps
    Current maximum: 0
    Config authority: 2apBGMsS6ti9RyF5TwQTDswXBWskiJP2LD4cUEDqYJjk
    Withdrawal authority: 2apBGMsS6ti9RyF5TwQTDswXBWskiJP2LD4cUEDqYJjk
    Withheld fees: 0
  Confidential transfer:
    Authority: 2apBGMsS6ti9RyF5TwQTDswXBWskiJP2LD4cUEDqYJjk
    Account approve policy: manual
    Audit key: audits are disabled
  Confidential transfer fee:
    Authority: 2apBGMsS6ti9RyF5TwQTDswXBWskiJP2LD4cUEDqYJjk
    Withdraw Withheld Encryption key: HDfmQztzBN2Cc3rkDZuL88SfWw5sSajVMyiz5QaQHFc=
    Harvest to mint: Enabled
    Withheld Amount: AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA==
  Transfer Hook:
    Authority: 2apBGMsS6ti9RyF5TwQTDswXBWskiJP2LD4cUEDqYJjk
    Program Id: Disabled
  Metadata Pointer:
    Authority: 9nEfZqzTP3dfVWmzQy54TzsZqSQqDFVW4PhXdG9vYCVD
    Metadata address: 2b1kV6DkPAnxd5ixfnxCpjxmKwqjjaYmCZfHsFu24GXo
  Metadata:
    Update Authority: 9nEfZqzTP3dfVWmzQy54TzsZqSQqDFVW4PhXdG9vYCVD
    Mint: 2b1kV6DkPAnxd5ixfnxCpjxmKwqjjaYmCZfHsFu24GXo
    Name: PayPal USD
    Symbol: PYUSD
    URI: https://token-metadata.paxos.com/pyusd_metadata/prod/solana/pyusd_metadata.json
```
