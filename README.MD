# Fintech Project


##### Dependencies:
 - golang `https://golang.org/doc/install`
 - dep `https://github.com/golang/dep`
 
##### Build:
```
make build
```

### Problem Statement:

One day you think of building a fintech application that can make non-cash transactions, as a Minimum Viable Product you want this application to have the following features

Transaction :
- customers can register
- as an owner you can register new merchants who can make transactions
- customers can fill in the balance (Topup)
- Customers can make payments to merchants that have been registered

#### Meet the actor :
 - customer: 
 - merchant: 

 - transaction
    - Customers can topup
    - Customers can make transactions at registered merchants

Some Spec: 
```
GIVEN I am unregister person
WHEN i register as customer with (name, email, phone)
THEN e-wallet should record it as new customer and return my wallet-id

GIVEN I am owner of Ewallet
WHEN i register new merchant with (name, email)
THEN e-wallet should record it as new merchant and return merchant wallet-id

GIVEN I am customer of Ewallet
WHEN i topup some amount
THEN e-wallet my balance should increased

GIVEN I am customer of Ewallet
WHEN i pay merchant 
THEN my balance should decreased, and merchant balance should increased, and i get transactionsID
```

```
(entity) user_accounts
 - user_id
 - name
 - email
 - phonenumber
 - user_type (merchant | customer)

(entity) wallet
 - wallet_id
 - user_id
 - balance

(entity) transaksi
  - id
  - reference
  - date
  - description
  - type (topup | payment)
  
topup:
  - credit wallet

payment:
  - credited wallet (merchant walletid)
  - debited wallet (customer walletid)
```

```
service
  - register_customer | register_merchant =
    - add new user to user_accounts
    - add new wallet to wallet 

  - topup:
    - add new transaksi with type topup 
    - increase balance from wallet

  - payment:
    - add new transaksi with type payment 
    - decrease balance from debited wallet
    - incrase balance from credited wallet
```

```
API:
  -> :register_customer
    {
      "name": "",
      "email": "",
      "phonenumber": ""
    }
  -> :register_merchant
    {
      "name": "",
      "email": ""
    }
  -> :topup
    {
      "wallet_id": "",
      "amount": ""
    }
  -> :payment
    {
      "wallet_id": "",
      "amount": "",
      "merchant_id": ""
    }
 ```
 
 ### TODO:
 
 there are still many shortcomings in the implementation of this code, for example the implementation of a repository that doesn't exist yet (only a mock), the need to wrap logic into a database transaction (for consistency) and a non-happy path test
