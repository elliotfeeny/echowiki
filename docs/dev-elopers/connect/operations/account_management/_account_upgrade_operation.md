# account_upgrade_operation

Manage an account's membership status

This operation is used to upgrade an account to a member, or renew its subscription. If an account which is an unexpired annual subscription member publishes this operation with upgrade_to_lifetime_member set to false, the account's membership expiration date will be pushed backward one year. If a basic account publishes it with upgrade_to_lifetime_member set to false, the account will be upgraded to a subscription member with an expiration date one year after the processing time of this operation.

Any account may use this operation to become a lifetime member by setting upgrade_to_lifetime_member to true. Once an account has become a lifetime member, it may not use this operation anymore.

### JSON Example 

```json
[
  8,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "account_to_upgrade": "1.2.0",
    "upgrade_to_lifetime_member": false,
    "extensions": []
  }
]
```