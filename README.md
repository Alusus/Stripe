# Stripe
library to work with Stripe API.

## Adding to the Project

We can install this library using the following statements:
```
import "Srl/Console";
import "Apm";
Apm.importFile("Alusus/Stripe");
```
## Example

```
import "Apm";
Apm.importFile("Alusus/Stripe");
use Stripe;
// to store all the balance of stripe account 
def balanceArray : Array[SrdRef[Balance]];
// the key from stripe website
def key : String="my_test_key"
// to get all the balance 
balanceArray = getBalance(key);

def i : int =0;
for i=0 , i<balanceArray.getLength(),i++{
    // to print the balance array
    balanceArray(i).print();

}
```
## Classes

### Customer class 

This class hold the json object of customer object from Stripe Api.

```
some of this class properties
```

`id` the id of the customer object from stripe.

`name` the name of the customer object from stripe.

`balance` the balance of the customer object from stripe.

`email` the email of the customer object from stripe.

`phone` the phone of the customer object from stripe.

```
func getCustomers(key: String): Array[SrdRef[Customer]]
```

This function get customers array from Stripe Api.

`key` the secret key from stripe website.

Returns customers Array.

```
func getCustomer(key: String, id: String): SrdRef[Customer]
```

This function does the same work as the previous function but it get one customer.

`key` the secret key from stripe website.

`id` the customer id.

Returns customer object.

```
func getCustomers(key: String): Array[SrdRef[Customer]]
```

This function get customers array from Stripe Api.

`key` the secret key from stripe website.

Returns customers Array.

```
func postCustomer(key: String, parameters: String): String
```

This function post a customer object to Stripe.

`key` the secret key from stripe website.

`parameters` the parametes of customer object in the form "email=super211@gmail.com&name=sonicmrah".

Returns customer id.



### Balance class

This class hold the json object of balance object from Stripe Api.

```
some of this class properties
```

`amount` the amount of the balance object from stripe.

`currency` the currency of the amount from stripe.

`sourceType` the source of the amount  from stripe (bank_account , card).

`balanceType` the type of the balance object from stripe (available , pending ).


```
func getBalance(key: String): Array[SrdRef[Balance]]
```

This function get Balances array from Stripe Api.

`key` the secret key from stripe website.

Returns Balances Array.



### BalanceTransaction class

This class hold the json object of BalanceTransaction object from Stripe Api.

```
some of this class properties
```

`id` the id of the BalanceTransaction object from stripe.

`amount` the amount of the transaction.

`availableOn` the time this amount will be available.

`fee` the fee on this transaction .

`exchangeRate` the exchangeRate of the transaction.

```
func getBalanceTranasaction(key: String): Array[SrdRef[BalanceTranasaction]]
```

This function get BalanceTranasactions array from Stripe Api.

`key` the secret key from stripe website.

Returns BalanceTranasactions Array.

```
func getBalanceTranasaction(key: String, id: String): SrdRef[BalanceTranasaction]
```

This function does the same work as the previous function but it get one BalanceTranasaction.

`key` the secret key from stripe website.

`id` the BalanceTranasaction id.

Returns BalanceTranasaction object.



### checkOut class

This class hold the json object of checkOut object from Stripe Api.

```
some of this class properties
```

`id` the id of the checkOut object from stripe.

`amountTotal` the amount of the transaction.

`url` the checkOut url.

`successUrl` the url if the checkOut success .

`cancelUrl` the url if the checkOut cancel.

```
func getCheckOuts(key: String): Array[SrdRef[CheckOut]] 
```

This function get CheckOuts array from Stripe Api.

`key` the secret key from stripe website.

Returns CheckOuts Array.

```
func getCheckOut(key: String, checkOutId: String): Array[SrdRef[CheckOut]]
```

This function does the same work as the previous function but it get one CheckOut.

`key` the secret key from stripe website.

`id` the CheckOut id.

Returns CheckOut object.

```
func postCheckOutSession(key: String, parameters: String): String
```

This function post a CheckOutSession object to Stripe.

`key` the secret key from stripe website.

`parameters` the parametes of CheckOutSession object in the form "customer=customerID&line_items=planID".

Returns CheckOutSession id.
