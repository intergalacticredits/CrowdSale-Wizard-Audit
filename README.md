[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

# Token Crowdsale Wizard Audit (ICO)

[![Join the Gitchat at https://gitter.im/TokenIndustrialAverage/Lobby](https://badges.gitter.im/TokenIndustrialAverage/Lobby.svg)](https://gitter.im/TokenIndustrialAverage/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## Overview

Contracts for this repo are created for the [InterGalactic Credits](http://igcredits.com) crowdsale .

Contracts are generated by [ICO Wizard](https://github.com/poanetwork/ico-wizard).

## Parameters

### Token

Parameters of ICO Wizard used to generate the instance of token contract for the audit.

| Field           | Value                    |
|-----------------|--------------------------|
| Token name      | InterGalactic Credits    |
| Token Ticker    | CREE                     |
| Decimals        | 18                       |
| Reserved tokens | Yes*                     |

*10,000 tokens to [0xd]

Remarks:
- "Reserved tokens - None" no % or fixed tokens 

### Crowdsale

Parameters of ICO Wizard used to generate the instance of crowdsale for the audit.

| Field              	| Value                      	|
|--------------------	|---------------------------	|
| Tiers              	| 1                         	|
| Supply             	| 7,000,000,000,000      	    |
| Rate               	| 100000                   	  |
| Allow modifying    	| Yes                        	|
| Disable whitelist  	| Yes                        	|
| Start date         	| 2017-12-23T17:55 (GMT - 5)  |
| End date           	| 2018-01-14T18:00 (GMT - 5)	|

Remarks:

- Rate - how many tokens for 1 ETH
- Supply - max cap of tokens. Token is mintable. Unsold tokens will not be produced.
- "Allow modifying - No" means that rate, supply, start date, end date are not modifiable.
- "Disable whitelist - No" means that whitelist is enable and only whitelisted accounts could participate in the crowdsale.

## Source code and deployed contracts

Source code for code audit is located in [/icowizard_Mainnet_0xa5F8fC0921880Cb7342368BD128eb8050442B1a1/](/icowizard_Mainnet_0xa5F8fC0921880Cb7342368BD128eb8050442B1a1) folder of the repository

###  Files structure

Files have prefixes corresponding to order of execution, e.g. a file with prefix `001_` will be deployed before a file with prefix `002_`.

A `.sol` file contain contract code.
A `.txt` file contain metadata

### Deployed contracts
Contracts are deployed on Mainnet and verified 
- `SafeMathLibExt`. The code of verified [SafeMathLibExt is here](https://etherscan.io/address/0xcdcd0638664657Ed3B031A75e00E02e47057e226#code).
- `CrowdsaleTokenExt`. The token contract. The code of verified [CrowdsaleTokenExt is here](https://etherscan.io/address/0xa5F8fC0921880Cb7342368BD128eb8050442B1a1#code).
- `FlatPricingExt`. The pricing strategy contract. The code of verified [FlatPricingExt is here](https://etherscan.io/address/0x6692D5dD701b9373933730d4e4f3b498DB7F7C32#code).
- `MintedTokenCappedCrowdsaleExt`. The crowdsale contract for a tier. The code of verified [MintedTokenCappedCrowdsaleExt is here](https://etherscan.io/address/0x3D5fb1E9d2F15D9ae5d7f4af4825FDEf03dE9685#code).
- `NullFinalizeAgentExt`. The finalize agent contract. The example of verified [NullFinalizeAgentExt is here](https://etherscan.io/address/0x766e51c940B9656E34b91041ca8aFa00B7E9ED71#code).

## Deployment stage

After all of the contracts are deployed next methods are executed at deployment stage:
- `setMintAgent` - sets `finalizeAgent` contract and crowdsale contract addresses as mint agents of token contract.
- `setFinalizeAgent` - sets `finalizeAgent` contract address as a finalize agent of the crowdsale contract.
- `setReleaseAgent` - sets `finalizeAgent` contract address as a release agent of token contract.
- `transferOwnership` - transfers ownership of token contract to the address that holds collected ether, which filled at step 2 of ICO Wizard.
