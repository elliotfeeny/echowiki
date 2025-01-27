# Echo Wallet API

## Contents
* Info and help
    * [info](#info)
    * [about](#about)
    * [help](#help)
    * [help_method](#help_method-method)
    * [get_prototype_operation](#get_prototype_operation-operation_type)
    * [get_object](#get_object-object_id)
* Blocks and transactions
    * [get_block](#get_block-block_num)
    * [get_block_virtual_ops](#get_block_virtual_ops-block_num)
    * [get_transaction_id](#get_transaction_id-tx)
    * [serialize_transaction](#serialize_transaction-tx)
    * [sign_transaction](#sign_transaction-tx-broadcast)
* Accounts
    * [get_account_count](#get_account_count)
    * [list_my_accounts](#list_my_accounts)
    * [list_accounts](#list_accounts-lowerbound-limit)
    * [get_account_history](#get_account_history-name-limit)
    * [get_relative_account_history](#get_relative_account_history-name-stop-limit-start)
    * [get_account](#get_account-account_name_or_id)
    * [get_account_id](#account_name_or_id-account_name_or_id)
    * [get_account_addresses](#get_account_addresses-account_id-from-limit)
    * [get_account_by_address](#get_account_by_address-address)
    * [import_accounts](#import_accounts-filename-password)
    * [register_account_with_api](#register_account_with_api-name-active_key-echorand_key)
    * [create_account_with_brain_key](#create_account_with_brain_key-brain_key-account_name-registrar_account-broadcast)
    * [generate_account_address](#generate_account_address-owner_account-label-broadcast)
    * [whitelist_account](#whitelist_account-authorizing_account-account_to_list-new_listing_status-broadcast)
* Keys
    * [import_key](#import_key-account_name_or_id-priv_key)
    * [import_account_keys](#import_account_keys-filename-password-src_account_name-dest_account_name)
    * [create_eddsa_keypair](#create_eddsa_keypair)
    * [get_private_key](#get_private_key-pubkey)
    * [is_public_key_registered](#is_public_key_registered-public_key)
    * [suggest_brain_key](#suggest_brain_key)
    * [normalize_brain_key](#normalize_brain_key-brain_key)
    * [derive_keys_from_brain_key](#derive_keys_from_brain_key-brain_key-number_of_desired_keys)
    * [dump_private_keys](#dump_private_keys)
    * [old_key_to_wif](#old_key_to_wif-b58)
* Password & lock
    * [is_new](#is_new)
    * [is_locked](#is_locked)
    * [lock](#lock)
    * [unlock](#unlock-password)
    * [set_password](#set_password-password)
    * [exit](#exit)
* Wallet file
    * [load_wallet_file](#load_wallet_file-wallet_filename)
    * [save_wallet_file](#save_wallet_file-wallet_filename)
* Balances
    * [import_balance](#import_balance-account_name_or_id-broadcast-private_keys)
    * [list_account_balances](#list_account_balances-id)
    * [list_id_balances](#list_id_balances-id)
    * [get_vesting_balances](#get_vesting_balances-account)
    * [withdraw_vesting](#withdraw_vesting-account-amount-asset_symbol-broadcast)
    * [transfer](#transfer-from-to-amount-asset_symbol-broadcast)
    * [list_frozen_balances](#list_frozen_balances-account)
    * [get_committee_frozen_balance](#get_committee_frozen_balance-owner_account)
    * [freeze_balance](#freeze_balance-account-amount-asset-duration-broadcast)
    * [committee_freeze_balance](#committee_freeze_balance-owner_account-amount-broadcast)
    * [committee_withdraw_balance](#committee_withdraw_balance-owner_account-amount-broadcast)
* Assets
    * [list_assets](#list_assets-lowerbound-limit)
    * [create_asset](#create_asset-issuer-symbol-precision-asset_opts-bitasset_opts-broadcast)
    * [update_asset](#update_asset-symbol-new_issuer-new_options-broadcast)
    * [update_bitasset](#update_bitasset-symbol-new_options-broadcast)
    * [update_asset_feed_producers](#update_asset_feed_producers-symbol-new_feed_producers-broadcast)
    * [publish_asset_feed](#publish_asset_feed-publishing_account-symbol-feed-broadcast)
    * [issue_asset](#issue_asset-to_account-amount-symbol-broadcast)
    * [get_asset](#get_asset-asset_name_or_id)
    * [get_asset_id](#get_asset_id-asset_name)
    * [get_bitasset_data](#get_bitasset_data-asset_name_or_id)
    * [fund_asset_fee_pool](#fund_asset_fee_pool-from-symbol-amount-broadcast)
    * [reserve_asset](#reserve_asset-from-amount-symbol-broadcast)
* Committee members
    * [create_committee_member](#create_committee_member-owner_account-url-amount-eth_address-btc_public_key-broadcast)
    * [update_committee_member](#update_committee_member-owner_account-committee_member-new_url-new_eth_address-new_btc_public_key-broadcast)
    * [create_activate_committee_member_proposal](#create_activate_committee_member_proposal-sender-committee_to_activate-expiration_time-broadcast)
    * [create_deactivate_committee_member_proposal](#create_deactivate_committee_member_proposal-sender-committee_to_activate-expiration_time-broadcast))
    * [list_committee_members](#list_committee_members-lowerbound-limit)
    * [get_committee_member](#get_committee_member-owner_account)
* Globals
    * [get_chain_properties](#get_chain_properties)
    * [get_global_properties](#get_global_properties)
    * [get_dynamic_global_properties](#get_dynamic_global_properties)
    * [propose_parameter_change](#propose_parameter_change-proposing_account-expiration_time-changed_values-broadcast)
    * [propose_fee_change](#propose_fee_change-proposing_account-expiration_time-changed_values-broadcast)
    * [approve_proposal](#approve_proposal-fee_paying_account-proposal_id-delta-broadcast)
* Contracts
    * [get_contract_object](#get_contract_object-id)
    * [get_contract](#get_contract-id)
    * [get_contract_result](#get_contract_result-id)
    * [create_contract](#create_contract-registrar_account-code-value-asset_type-supported_asset_id-eth_accuracy-save_wallet)
    * [call_contract](#call_contract-registrar_account-receiver-code-value-asset_type-save_wallet)
    * [call_contract_no_changing_state](#call_contract_no_changing_state-contract_id-registrar_account-asset_type-code)
    * [get_contract_pool_balance](#get_contract_pool_balance-id)
    * [get_contract_pool_whitelist](#get_contract_pool_whitelist-id)
    * [contract_fund_fee_pool](#contract_fund_fee_pool-registrar_account-receiver-value-broadcast)
    * [whitelist_contract_pool](#whitelist_contract_pool-registrar_account-contract_id-add_to_whitelist-add_to_blacklist-rm_whitelist-rm_blacklist-broadcast)
* Network
    * [network_add_nodes](#network_add_nodes-nodes)
    * [network_get_connected_peers](#network_get_connected_peers)
* Sidechain
    * [get_account_deposits](#get_account_deposits-account-type)
    * [get_account_withdrawals](#get_account_withdrawals-account-type)
* Sidechain-Ethereum
    * [get_eth_address](#get_eth_address-account)
    * [generate_eth_address](#generate_eth_address-account-broadcast)
    * [withdraw_eth](#withdraw_eth-account-eth_addr-value-broadcast)
* Sidechain-ERC20
    * [get_erc20_token](#get_erc20_token-eth_addr)
    * [check_erc20_token](#check_erc20_token-id)
    * [get_erc20_account_deposits](#get_erc20_account_deposits-account)
    * [get_erc20_account_withdrawals](#get_erc20_account_withdrawals-account)
    * [register_erc20_token](#register_erc20_token-account-eth_addr-name-symbol-decimals-broadcast)
    * [withdraw_erc20_token](#withdraw_erc20_token-account-to-erc20_token-value-broadcast)
* Sidechain-Bitcoin
    * [generate_btc_deposit_address](#generate_btc_deposit_address-account-backup_address-broadcast)
    * [get_btc_addresses](#get_btc_addresses-account)
    * [get_btc_deposit_script](#get_btc_deposit_script-address)
    * [withdraw_btc](#withdraw_btc-account-btc_addr-value-broadcast)

## Info and help

### `info`
Returns info about current chain and active committee members.

### `about`
Returns info such as client version, git version of graphene/fc, version of boost, openssl.

### `help`
Returns a list of all commands supported by the wallet API. This lists each command, along with its arguments and return types. For more detailed help on a single command, use help_method

### `help_method method`
Returns a list of all commands supported by the wallet API or detailed help on a single command.

| Option | Description |
| :--- | :--- |
| `string method` | (Optional) for more detailed help on a single command |

### `get_prototype_operation operation_type` 
Returns an uninitialized object representing a given blockchain operation.  
This returns a default-initialized object of the given type; it can be used during early development of the wallet when we don't yet have custom commands for creating all of the operations the blockchain supports.

* `operation_type` the type of operation to return, must be one of the operations described in [Operation section](/api-reference/echo-operations/README.md#Echo-Operations) 

### `get_object object_id`
Returns the blockchain object corresponding to the given id.

| Option | Description |
| :--- | :--- |
| `triplet object_id` | the id of the object to return |

## Blocks and transactions

### `get_block block_num`
Retrieve a full, signed block.

| Option | Description |
| :--- | :--- |
| `number block_num` | Height of the block to be returned |

### `get_block_virtual_ops block_num`
Get virtual ops from the block.

| Option | Description |
| :--- | :--- |
| `number block_num` | Height of the block to be returned |

### `get_transaction_id tx`
This method is used to convert a JSON transaction to its transactin ID.

| Option | Description |
| :--- | :--- |
| `string tx` | signed transaction |

### `serialize_transaction tx`
Converts a signed_transaction in JSON form to its binary representation.

| Option | Description |
| :--- | :--- |
| `string tx` | the transaction to serialize |

### `sign_transaction tx broadcast`
Signs a transaction.

| Option | Description |
| :--- | :--- |
| `string tx` | the unsigned transaction |
| `bool broadcast` | true if you wish to broadcast the transaction |

## Accounts

### `get_account_count`
Returns the number of accounts registered on the blockchain.

### `list_my_accounts`
Lists all accounts controlled by this wallet. This returns a list of the full account objects for all accounts whose private keys we possess.

### `list_accounts lowerbound limit`
Lists all accounts registered in the blockchain. This returns a list of all account names and their account ids, sorted by account name.

Use the `lowerbound` and limit parameters to page through the list. To retrieve all accounts, start by setting `lowerbound` to the empty string `""`, and then each iteration, pass the last account name returned as the `lowerbound` for the next `list_accounts` call.

| Option | Description |
| :--- | :--- |
| `string lowerbound` | the name of the first account to return. If the named account does not exist, the list will start at the account that comes after `lowerbound` |
| `number limit` | the maximum number of accounts to return (max: 1000) |

```
list_accounts nathan 10
```

### `get_account_history name limit`
Returns the most recent operations on the named account. This returns a list of operation history objects, which describe activity on the account.

| Option | Description |
| :--- | :--- |
| `string name` | the name or id of the account |
| `number limit` | the number of entries to return (starting from the most recent) |
```
get_account_history nathan 10
```

### `get_relative_account_history name stop limit start`
Returns the relative operations on the named account from start number.

| Option | Description |
| :--- | :--- |
| `string name` | the name or id of the account |
| `number stop` | Sequence number of earliest operation |
| `number limit` | the number of entries to return |
| `number start` | the sequence number where to start looping back throw the history |
```
get_relative_account_history nathan 0 10 20
```

### `get_account account_name_or_id`
Returns information about the given account.

| Option | Description |
| :--- | :--- |
| `string account_name_or_id` | the name or id of the account to provide information about |
```
get_account nathan or 1.2.0
```

### `get_account_id account_name_or_id`
Lookup the id of a named account.

| Option | Description |
| :--- | :--- |
| `string account_name_or_id` | the name of the account to look up |
```
get_account_id 1.2.0
```

### `get_account_addresses account_id from limit`
Get addresses owned by account in specified ids interval

| Option | Description |
| :--- | :--- |
| `triplet account_id`|  ID of the account |
| `number from` | Number of block to start retrieve from |
| `number limit` | Maximum number of addresses to return |
```
get_account_addresses 1.2.0 0 10
```

### `get_account_by_address address`
Get owner of specified address.

| Option | Description |
| :--- | :--- |
| `ripemd160 address` | address in form of ripemd160 hash |
```
get_account_by_address 8815c69de5d32d3061e52ca9386446332225b43d
```

### `import_accounts filename password`
Imports accounts from a Echo wallet file. Current wallet file must be unlocked to perform the import.  
Returns a map containing the accounts found and whether imported.

| Option | Description |
| :--- | :--- |
| `string filename` | the Echo wallet file to import |
| `string password` | the password to encrypt the Echo wallet file |

### `register_account name active registrar-account broadcast`
Registers a third party's account on the blockckain.  
This function is used to register an account for which you do not own the private keys. When acting as a registrar, an end user will generate their own private keys and send you the public keys. The registrar will use this function to register the account on behalf of the end user.

| Option | Description |
| :--- | :--- |
| `string name` | the name of the account, must be unique on the blockchain. Shorter names are more expensive to register; the rules are still in flux, but in general names of more than 8 characters with at least one digit will be cheap. |
| `public_key active` | the active key for a new account |
| `string registrar-account`|  the account which will pay the fee to register the user |
| `bool broadcast` | true to broadcast the transaction on the network |
```
register_account nathan ECHO6XS3BMVnEHAzo1PhHWt9vndrZn2P27tCbU9WdqCM8sJu new_acc true
```

### `register_account_with_api name active-key echorand-key`
Request connected node to register account with provided name and keys.

| Option | Description |
| :--- | :--- |
| `string name` | the name of the account, must be unique on the blockchain. Shorter names are more expensive to register; the rules are still in flux, but in general names of more than 8 characters with at least one digit will be cheap.
| `public_key active-key` | the active key for a new account
| `public_key echorand-key` | the echorand key for a new account


### `create_account_with_brain_key brain_key account_name registrar_account broadcast` 
Creates a new account and registers it on the blockchain.

| Option | Description |
| :--- | :--- |
| `string brain_key` | the brain key used for generating the account's private keys |
| `string account_name` | the name of the account, must be unique on the blockchain. Shorter names are more expensive to register; the rules are still in flux, but in general names of more than 8 characters with at least one digit will be cheap. |
| `string registrar_account` | the account which will pay the fee to register the user |
| `bool broadcast` | true to broadcast the transaction on the network |
```
create_account_with_brain_key "brain_key" new_acc nathan true
```

### `generate_account_address owner_account label broadcast` 
Creates a transaction to generate account address.

| Option | Description |
| :--- | :--- |
| `string owner_account` | The account for which the address is generated. |
| `string label` | The label for address |
| `bool broadcast` | true if you wish to broadcast the transaction |
```
generate_account_address nathan label true
```

### `whitelist_account authorizing_account account_to_list new_listing_status broadcast` 
Whitelist and blacklist accounts, primarily for transacting in whitelisted assets.

Accounts can freely specify opinions about other accounts, in the form of either whitelisting or blacklisting them. This information is used in chain validation only to determine whether an account is authorized to transact in an asset type which enforces a whitelist, but third parties can use this information for other uses as well, as long as it does not conflict with the use of whitelisted assets.

An asset which enforces a whitelist specifies a list of accounts to maintain its whitelist, and a list of accounts to maintain its blacklist. In order for a given account A to hold and transact in a whitelisted asset S, A must be whitelisted by at least one of S's whitelist_authorities and blacklisted by none of S's blacklist_authorities. If A receives a balance of S, and is later removed from the whitelist(s) which allowed it to hold S, or added to any blacklist S specifies as authoritative, A's balance of S will be frozen until A's authorization is reinstated.

| Option | Description |
| :--- | :--- |
| `string authorizing_account` | the account who is doing the whitelisting |
| `string account_to_list` | the account being whitelisted |
| `account_listing new_listing_status` | the new whitelisting status |
| `bool broadcast` | true to broadcast the transaction on the network |

## Keys

### `import_key account_name_or_id priv_key`
Imports the private key for an existing account.  
The private key must match either an owner key or an active key for the named account.

Returns true if the key was imported.

| Option | Description |
| :--- | :--- |
| `string account_name_or_id` | the account owning the key |
| `private_key priv_key` | the private key, should be input interactively |
```
import_key nathan private_key
```

### `import_account_keys filename password src_account_name dest_account_name` 
Imports from a Echo wallet file, find keys that were bound to a given account name on the Echo chain, rebind them to an account name on the Echo chain. Current wallet file must be unlocked to perform the import.

| Option | Description |
| :--- | :--- |
| `string filename` | the wallet file to import |
| `string password` | the password to encrypt the wallet file |
| `string src_account_name` | name of the account on chain |
| `string dest_account_name` | name of the account on chain, can be same or different to `src_account_name`|

### `create_eddsa_keypair` 
Create new EdDSA keypair encoded in base58 for public key and WIF for private key.

### `get_private_key pubkey` 
Get the WIF private key corresponding to a public key. The private key must already be in the wallet.

| Option | Description |
| :--- | :--- |
| `public_key pubkey` | eddsa public key |
```
get_private_key ECHO6XS3BMVnEHAzo1PhHWt9vndrZn2P27tCbU9WdqCM8sJu
```

### `is_public_key_registered public_key` 
Determine whether a textual representation of a public key (in Base-58 format) is *currently* linked to any account on the blockchain 

Returns true whether a public key is known.

| Option | Description |
| :--- | :--- |
| `public_key public_key` | Public key |
```
is_public_key_registered ECHO6XS3BMVnEHAzo1PhHWt9vndrZn2P27tCbU9WdqCM8sJu
```

### `suggest_brain_key`
Suggests a safe brain key to use for creating your account. [create_account_with_brain_key](#create_account_with_brain_key-brain_key-account_name-registrar_account-broadcast) requires you to specify a 'brain key', a long passphrase that provides enough entropy to generate cyrptographic keys. This function will suggest a suitably random string that should be easy to write down (and, with effort, memorize). 

### `normalize_brain_key brain-key`
Transforms a brain key to reduce the chance of errors when re-entering the key from memory.

This takes a user-supplied brain key and normalizes it into the form used for generating private keys. In particular, this upper-cases all ASCII characters and collapses multiple spaces into one.

Returns the brain key in its normalized form

| Option | Description |
| :--- | :--- |
| `string brain-key` | the brain key as supplied by the user |
```
Example normalize_brain_key brain_key
```

### `derive_keys_from_brain_key brain_key number_of_desired_keys`
Derive any number of *possible* owner keys from a given brain key.

Returns a list of keys that are deterministically derived from the brainkey

NOTE: These keys may or may not match with the owner keys of any account. This function is merely intended to assist with account or key recovery.

| Option | Description |
| :--- | :--- |
| `string brain_key` | Brain key |
| `number number_of_desired_keys` | Number of desired keys |
```
derive_keys_from_brain_key brain_key 1
```

### `dump_private_keys`
Dumps all private keys owned by the wallet.  
The keys are printed in WIF format. You can import these keys into another wallet using `import_key`.  
Returns a map containing the private keys, indexed by their public key

### `old_key_to_wif b58` 
Dumps private key from old b58 format to new WIF.  
The keys are printed in WIF format. You can import these key into another wallet using `import_key`.  
Returns string new in WIF eddsa private key

| Option | Description |
| :--- | :--- |
| `string b58` | old b58 format eddsa private_key |

## Password & lock

### `is_new`
Checks whether the wallet has just been created and has not yet had a password set.
Calling `set_password` will transition the wallet to the locked state. 

### `is_locked` 
Checks whether the wallet is locked (is unable to use its private keys).
This state can be changed by calling `lock` or `unlock`.

### `lock` 
Locks the wallet immediately.

### `unlock password` 
Unlocks the wallet.
The wallet remain unlocked until the `lock` is called or the program exits. 

| Option | Description |
| :--- | :--- |
| `string password` | the password previously set with `set_password`, in the wallet it should be input interactively |
```
unlock some_password
```

### `set_password password`
Sets a new password on the wallet.
The wallet must be either 'new' or 'unlocked' to execute this command. 

| Option | Description |
| :--- | :--- |
| `string password` | the password, should be input automatically in the wallet |
```
set_password your_password
```

### `exit` 
Exit from wallet

### `cancel_all_subscriptions`

## Wallet file

### `load_wallet_file wallet_filename` 
Loads a specified Graphene wallet.  
The current wallet is closed before the new wallet is loaded.
This does not change the filename that will be used for future wallet writes, so this may cause you to overwrite your original wallet unless you also call `set_wallet_filename`
Returns true if the specified wallet is loaded

| Option | Description |
| :--- | :--- |
| `string wallet_filename` | the filename of the wallet JSON file to load. If `wallet_filename` is empty, it reloads the existing wallet file |

### `save_wallet_file wallet_filename` 
Saves the current wallet to the given filename.  
This does not change the wallet filename that will be used for future writes, so think of this function as 'Save a Copy As...' instead of 'Save As...'. Use `set_wallet_filename` to make the filename persist. 

| Option | Description |
| :--- | :--- |
| `string wallet_filename` | the filename of the new wallet JSON file to create or overwrite. If `wallet_filename` is empty, save to the current filename. |

## Balances

### `import_balance account_name_or_id broadcast private_keys` 

This call will construct transaction(s) that will claim all balances controled by wif_keys and deposit them into the given account. wif_key should be input interactively

| Option | Description |
| :--- | :--- |
| `string account_name_or_id` | the account owning the key |
| `bool broadcast` | true to broadcast the transaction on the network |
| `listprivate_key private_keys` | array of eddsa private keys |
```
import_balance nathan true [ private_keys ]
```

### `list_account_balances id` 
List the balances of an account. Each account can have multiple balances, one for each type of asset owned by that account. The returned list will only contain assets for which the account has a nonzero balance.  
Returns a list of the given account's balances

| Option | Description |
| :--- | :--- |
| `string id` | the name or id of the account whose balances you want |
```
list_account_balances nathan or 1.2.0
```

### `list_id_balances id` 
List the balances of an account or a contract.

| Option | Description |
| :--- | :--- |
| `string id` | the id of either an account or a contract |
```
list_id_balances 1.11.0
```

### `list_frozen_balances account` 
List frozen balances of an account.

| Option | Description |
| :--- | :--- |
| `string account` | the name or id of the account whose balances you want |
```
list_frozen_balances nathan
```

### `get_committee_frozen_balance owner_account` 
List frozen balances of an committee member account.

| Option | Description |
| :--- | :--- |
| `string owner_account` | the name or id of the committee members account whose balances you want |
```
get_committee_frozen_balance nathan
```

### `freeze_balance account amount asset duration broadcast` 
Freezes part of your balance for the specified amount of time.

| Option | Description |
| :--- | :--- |
| `string account` | the name or id of the balance holder |
| `string amount` | the amount of asset to freeze |
| `string asset` | the name of asset you want to freeze |
| `number duration` | duration of freeze in days |
| `bool broadcast` | true to broadcast the transaction on the network |
```
freeze_balance nathan 1 ECHO 90 true
```

### `committee_freeze_balance owner_account amount broadcast` 
Freezes balance required for committee members to operate.

| Option | Description |
| :--- | :--- |
| `string owner_account` | the name or id of the committee member account |
| `number amount` | the amount of asset to freeze |
| `bool broadcast` | true to broadcast the transaction on the network |
```
committee_freeze_balance nathan 10 true
```

### `committee_withdraw_balance owner_account amount broadcast` 
Withdraws part of frozen committee members balance.

| Option | Description |
| :--- | :--- |
| `string owner_account` | the name or id of the committee member account |
| `number amount` | the amount of frozen committee balance to withdraw |
| `bool broadcast` | true to broadcast the transaction on the network |
```
committee_withdraw_balance nathan 1 true
```

### `get_vesting_balances account` 
Get information about a vesting balance object.

| Option | Description |
| :--- | :--- |
| `string account` | An account name or account ID or vesting balance object ID. |
```
get_vesting_balances nathan
```

### `withdraw_vesting account amount asset_symbol broadcast` 
Withdraw a vesting balance.

| Option | Description |
| :--- | :--- |
| `string account` | The account ID or vesting balance ID type. |
| `string amount` | The amount to withdraw. |
| `string asset_symbol` | The symbol of the asset to withdraw. |
| `bool broadcast` | true if you wish to broadcast the transaction |
```
withdraw_vesting nathan 10 ECHO true
```

### `transfer from to amount asset_symbol broadcast` 
Transfer an amount from one account to another.  
Returns the signed transaction transferring funds

| Option | Description |
| :--- | :--- |
| `string from` | the name or id of the account sending the funds |
| `string to` | the name or id of the account receiving the funds |
| `string amount` | the amount to send (in nominal units  to send half of a BTS, specify 0.5) |
| `string asset_symbol` | the symbol or id of the asset to send |
| `bool broadcast` | true to broadcast the transaction on the network |
```
transfer 1.2.0 1.2.1 10 ECHO true
```

## Assets

### `list_assets lowerbound limit` 
Lists all assets registered on the blockchain.  
To list all assets, pass the empty string `""` for the lowerbound to start at the beginning of the list, and iterate as necessary.  
Returns the list of asset objects, ordered by symbol

| Option | Description |
| :--- | :--- |
| `string lowerbound` | the symbol of the first asset to include in the list. |
| `number limit` | the maximum number of assets to return (max: 100) |
```
list_assets ECHO 10
list_assets "" 10
```

### `create_asset issuer symbol precision asset_opts bitasset_opts broadcast` 
Creates a new user-issued or market-issued asset.  
Many options can be changed later using `update_asset`.  
Right now this function is difficult to use because you must provide raw JSON data structures for the options objects, and those include prices and asset ids.

Returns the signed transaction creating a new asset

| Option | Description |
| :--- | :--- |
| `string issuer` | the name or id of the account who will pay the fee and become the issuer of the new asset. This can be updated later |
| `string symbol` | the ticker symbol of the new asset |
| `number precision` | the number of digits of precision to the right of the decimal point, must be less than or equal to 12 |
| `asset_options asset_opts` | asset options required for all new assets. Note that core_exchange_rate technically needs to store the asset ID of this new asset. Since this ID is not known at the time this operation is created, create this price as though the new asset has instance ID 1, and the chain will overwrite it with the new asset's ID. |
| `bitasset_options bitasset_opts` | (Optional) options specific to BitAssets. This may be null unless the `market_issued` flag is set in common.flags |
| `bool broadcast` | true to broadcast the transaction on the network |

### `update_asset symbol[new_issuer new_options broadcast` 
Update the core options on an asset. There are a number of options which all assets in the network use. These options are enumerated in the asset_object::asset_options struct. This command is used to update these options for an existing asset.  
This operation cannot be used to update BitAsset-specific options. For these options, `update_bitasset` instead.

Returns the signed transaction updating the asset

| Option | Description |
| :--- | :--- |
| `string symbol` | the name or id of the asset to update |
| `string new_issuer` | (Optional) if changing the asset's issuer, the name or id of the new issuer. null if you wish to remain the issuer of the asset |
| `asset_options new_options` | the new asset_options object, which will entirely replace the existing options. |
| `bool broadcast` | true to broadcast the transaction on the network |

### `update_bitasset symbol new_options broadcast` 
Update the options specific to a BitAsset.  
BitAssets have some options which are not relevant to other asset types. This operation is used to update those options an an existing BitAsset.

Returns the signed transaction updating the bitasset

| Option | Description |
| :--- | :--- |
| `string symbol` | the name or id of the asset to update, which must be a market-issued asset |
| `bitasset_options new_options` | the new bitasset_options object, which will entirely replace the existing options. |
| `bool broadcast` | true to broadcast the transaction on the network |

### `update_asset_feed_producers symbol new_feed_producers broadcast` 
Update the set of feed-producing accounts for a BitAsset.  
BitAssets have price feeds selected by taking the median values of recommendations from a set of feed producers. This command is used to specify which accounts may produce feeds for a given BitAsset. 

Returns the signed transaction updating the bitasset's feed producers

| Option | Description |
| :--- | :--- |
| `string symbol` | the name or id of the asset to update |
| `liststring new_feed_producers` | a list of account names or ids which are authorized to produce feeds for the asset. this list will completely replace the existing list |
| `bool broadcast` | true to broadcast the transaction on the network |
```
update_asset_feed_producers UIA [nathan, foobar] true
```

### `publish_asset_feed publishing_account symbol feed broadcast` 
Publishes a price feed for the named asset.  
Price feed providers use this command to publish their price feeds for market-issued assets. A price feed is used to tune the market for a particular market-issued asset. For each value in the feed, the median across all committee_member feeds for that asset is calculated and the market for the asset is configured with the median of that value.  
The feed object in this command contains three prices: a call price limit, a short price limit, and a settlement price. The call limit price is structured as (collateral asset) / (debt asset) and the short limit price is structured as (asset for sale) / (collateral asset). Note that the asset IDs are opposite to eachother, so if we're publishing a feed for USD, the call limit price will be ECHO/USD and the short limit price will be USD/ECHO. The settlement price may be flipped either direction, as long as it is a ratio between the market-issued asset and its collateral.

Returns the signed transaction updating the price feed for the given asset

| Option | Description |
| :--- | :--- |
| `string publishing_account` | the account publishing the price feed |
| `string symbol` | the name or id of the asset whose feed we're publishing |
| `price_feed feed` | the price_feed object containing the three prices making up the feed |
| `bool broadcast` | true to broadcast the transaction on the network |

### `issue_asset to_account amount symbol broadcast` 
Issue new shares of an asset.

Returns the signed transaction issuing the new shares

| Option | Description |
| :--- | :--- |
| `string to_account` | the name or id of the account to receive the new shares |
| `string amount` | the amount to issue, in nominal units |
| `string symbol` | the ticker symbol of the asset to issue |
| `bool broadcast` | true to broadcast the transaction on the network |

### `get_asset asset_name_or_id` 
Returns information about the given asset.

| Option | Description |
| :--- | :--- |
| `string asset_name_or_id` | the symbol or id of the asset in question |
```
get_asset ECHO
```

### `get_asset_id asset_name` 
Lookup the id of a named asset.

| Option | Description |
| :--- | :--- |
| `string asset_name` | the symbol of an asset to look up |
```
get_asset_id ECHO
```

### `get_bitasset_data asset_name_or_id` 
Returns the BitAsset-specific data for a given asset. Market-issued assets's behavior are determined both by their "BitAsset Data" and their basic asset data, as returned by `get_asset`.

| Option | Description |
| :--- | :--- |
| `string asset_name_or_id` | the symbol or id of the BitAsset in question |
```
get_bitasset_data ECHO
```

### `fund_asset_fee_pool from symbol amount broadcast` 
Pay into the fee pool for the given asset.  
User-issued assets can fc::optionally have a pool of the core asset which is automatically used to pay transaction fees for any transaction using that asset (using the asset's core exchange rate).  
This command allows anyone to deposit the core asset into this fee pool.

Returns the signed transaction funding the fee pool

| Option | Description |
| :--- | :--- |
| `string from` | the name or id of the account sending the core asset |
| `string symbol` | the name or id of the asset whose fee pool you wish to fund |
| `string amount` | the amount of the core asset to deposit |
| `bool broadcast` | true to broadcast the transaction on the network |

### `reserve_asset from amount symbol broadcast` 
Burns the given user-issued asset.  
This command burns the user-issued asset to reduce the amount in circulation. you cannot burn market-issued assets. 

Returns the signed transaction burning the asset

| Option | Description |
| :--- | :--- |
| `string from` | the account containing the asset you wish to burn |
| `string amount` | the amount to burn, in nominal units |
| `string symbol` | the name or id of the asset to burn |
| `bool broadcast` | true to broadcast the transaction on the network |
```
reserve_asset nathan 10 ECHO true
```

## Committee members

### `create_committee_member owner_account url amount eth_address btc_public_key broadcast` 
Creates a committee_member object owned by the given account.  
An account can have at most one committee_member object.

Returns the signed transaction registering a committee_member

| Option | Description |
| :--- | :--- |
| `string owner_account` | the name or id of the account which is creating the committee_member |
| `string url` | a URL to include in the committee_member record in the blockchain. Clients may display this when showing a list of committee_members. May be blank. |
| `string amount` | amount of ECHO asset to freeze |
| `string eth_address` | address of the account in the ethereum network |
| `string btc_public_key` | public key of the account in the bitcoin network |
| `bool broadcast` | true to broadcast the transaction on the network |
```
create_committee_member nathan example.com 1000 E8fd4Db0C38d48493AD167A268683fAb7230a88A 02c16e97132e72738c9c0163656348cd1be03521de17efeb07e496e742ac84512e true
```

### `update_committee_member owner_account committee_member new_url new_eth_address new_btc_public_key broadcast` 
Updates a committee_member object owned by the given account.

Returns the signed transaction updating a committee_member.

| Option | Description |
| :--- | :--- |
| `string owner_account` | the name or id of the account which is updating the committee_member |
| `triplet committee_member` | a committee_member owned by the owner_account |
| `string new_url` | a new URL of the committee_member_object, enter empty string if you don't want to change it |
| `string new_eth_address` | a new ethereum address of the committee_member object, enter empty string if you don't want to change it |
| `string new_btc_public_key` | a new bitcoin public key of the committee_member object, enter empty string if you don't want to change it |
| `bool broadcast` | true to broadcast the transaction on the network |
```
update_committee_member nathan 1.4.0 new_url E8fd4Db0C38d48493AD167A268683fAb7230a88A 02c16e97132e72738c9c0163656348cd1be03521de17efeb07e496e742ac84512e true
```

### `create_activate_committee_member_proposal sender committee_to_activate expiration_time broadcast` 
Creates a proposal to activate given commitee.  
An account can have at most one committee_member object.

Returns the signed transaction registering a committee_member

| Option | Description |
| :--- | :--- |
| `string sender` | the name or id of the account which is creating proposal |
| `triplet committee_to_activate` | a committee member |
| `time_point expiration_time` | expiration time of created proposal |
| `bool broadcast` | true to broadcast the transaction on the network |
```
create_activate_committee_member_proposal nathan 1.4.0 1970-01-01T00:00:00 true
```

### `create_deactivate_committee_member_proposal sender committee_to_activate expiration_time broadcast)` 
Creates a proposal to deactivate given commitee.  
An account can have at most one committee_member object.

Returns the signed transaction registering a committee_member

| Option | Description |
| :--- | :--- |
| `string sender` | the name or id of the account which is creating proposal |
| `triplet committee_to_activate` | a committee member |
| `time_point expiration_time` | expiration time of created proposal |
| `bool broadcast` | true to broadcast the transaction on the network |
```
create_deactivate_committee_member_proposal nathan 1.4.0 1970-01-01T00:00:00 true
```

### `list_committee_members lowerbound limit` 
Lists all committee_members registered in the blockchain. This returns a list of all account names that own committee_members, and the associated committee_member id, sorted by name. This lists committee_members whether they are currently voted in or not.

Use the `lowerbound` and limit parameters to page through the list. To retrieve all committee_members, start by setting `lowerbound` to the empty string `""`, and then each iteration, pass the last committee_member name returned as the `lowerbound` for the next `[list_committee_members()](#classgraphene_1_1wallet_1_1wallet__api_1aec9eca62eb2c6748d463604632ba6508)` call.

| Option | Description |
| :--- | :--- |
| `string lowerbound` | the name of the first committee_member to return. If the named committee_member does not exist, the list will start at the committee_member that comes after `lowerbound`|
| `number limit` | the maximum number of committee_members to return (max: 1000) |
```
list_committee_members
```

### `get_committee_member owner_account` 
Returns information about the given committee_member. 

| Option | Description |
| :--- | :--- |
| `string owner_account` | the name or id of the committee_member account owner, or the id of the committee_member |
```
get_committee_member nathan
```

## Globals

### `get_chain_properties` 
Retrieve the chain_property_object associated with the chain

### `get_global_properties` 
Returns the block chain's slowly-changing settings. This object contains all of the properties of the blockchain that are fixed or that change only once per maintenance interval (daily) such as the current list of committee_members, block interval, etc.  
**See also**: `get_dynamic_global_properties` for frequently changing properties.

### `get_dynamic_global_properties` 
Returns the block chain's rapidly-changing properties. The returned object contains information that changes every block interval such as the head block number, etc.  
**See also**: `get_global_properties` for less-frequently changing properties 

### `propose_parameter_change proposing_account expiration_time changed_values broadcast` 
Creates a transaction to propose a parameter change.  
Multiple parameters can be specified if an atomic change is desired.

| Option | Description |
| :--- | :--- |
| `string proposing_account` | The account paying the fee to propose the tx |
| `time_point expiration_time` | Timestamp specifying when the proposal will either take effect or expire. |
| `string changed_values` | The values to change; all other chain parameters are filled in with default values |
| `bool broadcast` | true if you wish to broadcast the transaction |

### `propose_fee_change proposing_account expiration_time changed_values broadcast` 
Propose a fee change.

| Option | Description |
| :--- | :--- |
| `string proposing_account` | The account paying the fee to propose the tx |
| `time_point expiration_time` | Timestamp specifying when the proposal will either take effect or expire. |
| `string changed_values` | Map of operation type to new fee. Operations may be specified by name or ID. The "scale" key changes the scale. All other operations will maintain current values. |
| `bool broadcast` | true if you wish to broadcast the transaction |

### `approve_proposal fee_paying_account proposal_id delta broadcast` 
Approve or disapprove a proposal.

| Option | Description |
| :--- | :--- |
| `string fee_paying_account` | The account paying the fee for the op. |
| `string proposal_id` | The proposal to modify. |
| `approval_delta delta` | Members contain approvals to create or remove. In JSON you can leave empty members undefined. |
| `bool broadcast` | true if you wish to broadcast the transaction |


## Contracts

### `get_contract_object id` 
Get the contract object from the database by it's id.

| Option | Description |
| :--- | :--- |
| `triplet id` | the id of the contract |
```
get_contract_object 1.11.0
```

### `get_contract id` 
Get the contract information by the contract's id

| Option | Description |
| :--- | :--- |
| `triplet id` | id of the contract |
```
get_contract 1.11.0
```

### `get_contract_result id` 
Get the result of contract execution.

| Option | Description |
| :--- | :--- |
| `triplet id` | the id of the conract result |
```
get_contract_result 1.10.0
```

### `create_contract registrar_account code value asset_type supported_asset_id eth_accuracy save_wallet` 
Upload/Create a contract.

Returns the signed transaction creating the contract

| Option | Description |
| :--- | :--- |
| `string registrar_account` | name of the account creating the contract |
| `string code` | code of the contract in hex format |
| `number value` | the amount of asset transfered to the contract |
| `string asset_type` | the type of the asset transfered to the contract |
| `string supported_asset_id` | the asset that can be used to create/call the contract (see [https://echo-dev.io/developers/smart-contracts/solidity/introduction/#flag-of-supported-asset](https://echo-dev.io/developers/smart-contracts/solidity/introduction/#flag-of-supported-asset)) |
| `bool eth_accuracy` | whether to use the ethereum asset accuracy (see [https://echo-dev.io/developers/smart-contracts/solidity/introduction/#flag-of-using-ethereum-accuracy](https://echo-dev.io/developers/smart-contracts/solidity/introduction/#flag-of-using-ethereum-accuracy)) |
| `bool save_wallet` | whether to save the contract to the wallet |
```
create_contract nathan code_contract 0 ECHO "" false true
```

### `call_contract registrar_account receiver code value asset_type save_wallet` 
Call a contract.

Returns the signed transaction calling the contract

| Option | Description |
| :--- | :--- |
| `string registrar_account` | name of the account calling the contract |
| `triplet receiver` | the id of the contract to call |
| `string code` | the hash of the method to call |
| `number value` | the amount of asset transfered to the contract |
| `string asset_type` | the type of the asset transfered to the contract |
| `bool save_wallet` | whether to save the contract call to the wallet |
```
call_contract nathan 1.11.0 code_contract 0 ECHO false
```

### `call_contract_no_changing_state contract_id registrar_account asset_type code` 
Call the provided contract, but don't change the state.

Returns result of execution

| Option | Description |
| :--- | :--- |
| `triplet contract_id` | ID of the contract |
| `string caller` | ID of the account or contract that calls contract |
| `string amount` | amount in ECHO. 1 ECHO is 100000000 |
| `string asset_type` | the type of the asset transfered to the contract |
| `string code` | the hash of the method to call |
```
call_contract_no_changing_state 1.11.0 1.2.0 0 ECHO "6d4ce63c"
```

### `get_contract_pool_balance id` 
Get contract's feepool balance.

| Option | Description |
| :--- | :--- |
| `triplet id` | for getting feepool balance. |
```
get_contract_pool_balance 1.11.0
```

### `get_contract_pool_whitelist id` 
Get contract's whitelist and blacklist.

| Option | Description |
| :--- | :--- |
| `triplet id` | for getting whitelist and blacklist of feepool object. |
```
get_contract_pool_whitelist 1.11.0
```

### `contract_fund_fee_pool registrar_account receiver value broadcast` 
Fund feepool of contract.

| Option | Description |
| :--- | :--- |
| `string registrar_account` | name of the account which fund contract's feepool |
| `triplet receiver` | the id of the contract's feepool |
| `number value` | the amount of asset transfered to the contract in default asset_id_type() |
| `bool broadcast` | whether to broadcast the fund contract operation to the network |
```
contract_fund_fee_pool nathan 1.11.0 0 true
```

### `whitelist_contract_pool registrar_account contract_id add_to_whitelist add_to_blacklist rm_whitelist rm_blacklist broadcast` 
Whitelist or blacklist contract pool.

Returns the signed version of the transaction.

| Option | Description |
| :--- | :--- |
| `string registrar_account` | is an owner of contract which perform whitelistining or blacklistining. |
| `triplet contract_id` | Whitelistining or blacklistining applying for this contract. |
| `listtriplet add_to_whitelist` | Leave it empty if you don't want to add some account to whitelist. |
| `listtriplet add_to_blacklist` | Leave it empty if you don't want to add some account to blacklist. |
| `listtriplet rm_whitelist` | Leave it empty if you don't want to remove some account from whitelist. |
| `listtriplet rm_blacklist` | Leave it empty if you don't want to remove some account from blacklist. |
| `bool broadcast` | true if you wish to broadcast the contract whitelist operation |
```
whitelist_contract_pool nathan 1.11.0 [] [] [] [] true
```

## Network

### `network_add_nodes nodes` 
Adding nodes to network.

| Option | Description |
| :--- | :--- |
| `liststring nodes` | endpoints your nodes |
```
network_add_nodes 127.0.0.1:8090
```

### `network_get_connected_peers` 
Get connected peers.

## Sidechain

### `get_account_deposits account type` 
Returns all deposits, for the given account id.

| Option | Description |
| :--- | :--- |
| `triplet account` | the id of the account to provide information about |
| `string type` | the type of the deposits may be "", "eth" or "btc". By default "" = all deposits |
```
get_account_deposits 1.2.0 ""
```

### `get_account_withdrawals account type` 
Returns all withdrawals, for the given account id.

| Option | Description |
| :--- | :--- |
| `triplet account` | the id of the account to provide information about |
| `string type` | the type of the deposits may be "", "eth" or "btc". By default "" = all deposits |
```
get_account_withdrawals 1.2.0 ""
```

## Sidechain Ethereum

### `get_eth_address account` 
Returns information about generated eth address, if exist and approved, for the given account id.

| Option | Description |
| :--- | :--- |
| `triplet account` | the id of the account to provide information about |
```
get_eth_address 1.2.0
```

### `generate_eth_address account broadcast` 
Creates a transaction to generate ethereum address.

| Option | Description |
| :--- | :--- |
| `triplet account` | The account for which the ethereum address is generated. |
| `bool broadcast` | true if you wish to broadcast the transaction |
```
generate_eth_address nathan true
```

### `withdraw_eth account eth_addr value broadcast` 
Creates a transaction to withdraw ethereum.

| Option | Description |
| :--- | :--- |
| `string account` | The account who withdraw ethereum. |
| `string eth_addr` | The Ethereum address where withdraw. |
| `number value` | Withdraw amount. |
| `bool broadcast` | true if you wish to broadcast the transaction. |
```
withdraw_eth nathan 0102fe7702b96808f7bbc0d4a888ed1468216cfd 10 true
```

## Sidechain ERC20

### `get_erc20_token eth_addr` 
Get erc20 token information.

| Option | Description |
| :--- | :--- |
| `eth_address eth_addr` | the ethereum address of token in Ethereum network |
```
get_erc20_token 0102fe7702b96808f7bbc0d4a888ed1468216cfd
```

### `check_erc20_token id` 
Checks the contract exists and is ERC20 token contract registered by register_erc20_contract operation

| Option | Description |
| :--- | :--- |
| `triplet id` | ID of the contract |
```
check_erc20_token 1.11.0
```

### `get_erc20_account_deposits account` 
Returns all deposits, for the given account id.

| Option | Description |
| :--- | :--- |
| `triplet account` | the id of the account to provide information about |
```
get_erc20_account_deposits 1.2.0
```

### `get_erc20_account_withdrawals account` 
Returns all withdrawals for the given account id.

| Option | Description |
| :--- | :--- |
| `triplet account` | the id of the account to provide information about |
```
get_erc20_account_withdrawals 1.2.0
```

### `register_erc20_token account eth_addr name symbol decimals broadcast` 
Creates a transaction to register erc20_token for sidechain.

Returns the signed version of the transaction.

| Option | Description |
| :--- | :--- |
| `string account` | The account who create erc20 token and become his owner. |
| `string eth_addr` | The address of token erc20 token in ethereum network. |
| `string name` | Name of the token in echo network. |
| `string symbol` | Symbol of the token in echo network. |
| `number decimals` | Number of the digist after the comma of the token in echo network. |
| `bool broadcast` | true if you wish to broadcast the transaction. |
```
register_erc20_token nathan E62627255a4BC0c92E190E01c515Ba28233c9207 erc20DbeVxoV QIGMPUZ 8 true
```

### `withdraw_erc20_token account to erc20_token value broadcast` 
Creates a transaction to withdraw erc20_token.

Returns the signed version of the transaction.

| Option | Description |
| :--- | :--- |
| `string account` | The account who withdraw erc20 token. |
| `string to` | The Ethereum address where withdraw erc20 token. |
| `string erc20_token` | The erc20 token id in ECHO. |
| `string value` | The amount withdraw. |
| `bool broadcast` | true if you wish to broadcast the transaction. |


## Sidechain Bitcoin

### `generate_btc_deposit_address account backup_address broadcast` 
Creates a transaction to generate bitcoin deposit address.

| Option | Description |
| :--- | :--- |
| `string account` | The account for which the bitcoin address is generated. |
| `string backup_address` | The P2PK address to transfer satoshis back. |
| `bool broadcast` | true if you wish to broadcast the transaction |
```
generate_btc_deposit_address nathan n4cLNDfyVPGoNFUpUEyBP8TzDPRNaVBm6E true
```

### `get_btc_address account` 
Returns information about generated btc address, if exist and approved, for the given account id.

| Option | Description |
| :--- | :--- |
| `triplet account` | the id of the account to provide information about |
```
get_btc_address 1.2.0
```

### `get_btc_deposit_script address` 
Returns bitcoin script for generated bitcoin deposit address, if exist, for the given address id.

| Option | Description |
| :--- | :--- |
| `triplet address` | the id of the bitcoin address to provide script |
```
get_btc_deposit_script 1.22.0
```

### `withdraw_btc account btc_addr value broadcast` 
Creates a transaction to withdraw btc.

| Option | Description |
| :--- | :--- |
| `string account` | The account who withdraw btc. |
| `string btc_addr` | The Bitcoin address where withdraw. |
| `number value` | The amount withdraw in satoshis. |
| `bool broadcast` | true if you wish to broadcast the transaction. |
```
withdraw_btc nathan 0102fe7702b96808f7bbc0d4a888ed1468216cfd 10000000 true
```
