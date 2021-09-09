#### CardClient

```swift
// API client that handles card network requests
public class CardClient: Client {

    // To be used when buyer submits their card info
    // This function will validate buyer's card, and if valid, the order will be paid with this card
    // Merchant will need to handle capturing/authorizing the order in completion, either client-side with ApprovalAction or server-side using their own server.
    public func approveOrder(orderID: String, card: Card, completion: (Result<(OrderData, ApprovalAction), ErrorData>) -> Void)
}
```

#### Models

```swift
public struct Card: PaymentSource {
    var cardNumber: String
    var cvv: String
    var expiry: String
}
```
