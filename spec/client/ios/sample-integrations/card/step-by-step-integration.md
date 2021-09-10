## Step-by-step integration

### Basic server-side integration

#### 1. Import card module

**Client**

```swift
import CardPayment
```

#### 2. Initialize CoreConfig and CardClient

**Client**

```swift
let config = CoreConfig(clientID: <your_clientID>, environment: .sandbox)
let cardClient = CardClient(config: config)
```

#### 3. Create an order in your server

**Server**

```
curl --location --request POST 'https://api.sandbox.paypal.com/v2/checkout/orders/' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <access_token>' \
--data-raw '{
    "intent": "CAPTURE",
    "purchase_units": [
        {
            "amount": {
                "currency_code": "USD",
                "value": "5.00"
            }
        }
    ]
}'
```

#### 4. Approve order with buyer's card info and authorize/capture the order

**Client**

```swift
// Create a Card object from buyer's inputs
let card = Card(
    number: <card_number>
    cvv: <card_cvv>
    expiry: <card_expiry>
)

// Approve the order with the orderID of the order you created in your server in step 3
cardClient.approveOrder(orderID: <orderID>, card: card) { result in
    switch result {
    case let .success(data):
        // Authorize/capture the order
        switch data.intent {
        case .authorize:
            // Authorize the order in your server with order ID `data.orderID`
        case .capture:
            // Capture the order in your server with order ID `data.orderID`
        }
    case let .failure(data):
        // Handle error
        print(data.error)
    }
}
```

**Server**

Authorize an order:
```
curl --location --request POST 'https://api.sandbox.paypal.com/v2/checkout/orders/<orderID>/authorize' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <access_token>' \
--data-raw ''
```

Capture an order:
```
curl --location --request POST 'https://api.sandbox.paypal.com/v2/checkout/orders/<orderID>/capture' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <access_token>' \
--data-raw ''
```
