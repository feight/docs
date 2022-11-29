# Subscribe user to a package

Purchasing a subscription happens in stages:

-   Initializing a subscription for the user.
-   Accepting payment, which will activate the subscription.

## These APIs need to be run sequentially:

---

## /apiv1/user/update-address

    This API will update the physical address of the user.

    NOTE: This is only required if the package that you are subscribing to requires a physical address.

### Params

-   #### **street: string**
-   #### **house_no: string**
-   #### **building: string** (optional)
-   #### **zip_code: string**
-   #### **suburb: string**
-   #### **district: string**
-   #### **city: string**
-   #### **country: string**
-   #### **latitude: float**
-   #### **longitude: float**

<br>

---

## /apiv1/user/subscribe

    This API will subscribe to a package in an "initialized" state.
    An initialized subscription will remain inactive until a payment is finalized.

### Params

-   #### **product_id: string**

    The product ID for which to subscribe.

    -   Example: 73f39c33-c0e5-4690-9b57-d8a1ad75019f

-   #### **gift: boolean** (optional)

    Indicates that this purchase is a gift. The result of the purchase will include a voucher.

<br>

---

## /apiv1/subscriptions/create-transaction

    Creates a transaction for the subscription
    > Returns the subscription

### Params

-   #### **subscription_key: string**

    The subscription key that was returned from '/apiv1/user/subscribe'.

-   #### **amount: int32**

    The amount in ZAR for which the product was purchased.

-   #### **status_id: int32**

    Status of the transaction.

    Only a 'SUCCESS' status will activate the subscription.

    Possible values:

    -   FAILED = 300
    -   AUTHORIZED = 401
    -   SUCCESS = 400
    -   VOID = 500
    -   REFUNDED = 600

-   #### **created: int64**

    The date on which the transacton was created as unix timestamp in milliseconds.

-   #### **processed: int64**

    The date on which the transacton was processed as unix timestamp in milliseconds.

-   #### **payment_method: object**

    The payment method details (any)

-   #### **rebill_attempt: int32** (optional)

    The rebill attempt of this transaction. i.e '1' would be the first attempt.
    If the attempt failed, '2' would be the second attempt.

    Maximum of 3 attempts.

-   #### **error: string** (optional)

    If an error occured during payment, you can supply it here.

-   #### **attachment: object** (optional)

    Any useful data for support/debugging.
