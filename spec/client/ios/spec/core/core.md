## Core module

#### CoreConfig

```swift
// Contains shared data that applies to every payment method
public struct CoreConfig {
    let clientID: String
    let environment: Environment

    weak var delegate: PaymentDelegate?
}
```

#### Client

```swift
// API client that handles network requests
public class Client {
    // Parent class containing shared properties/functions for all payment method clients (CardClient, PayPalClient, etc.)
    // In the future if we support things like createOrder client-side (which applies for every payment method), they can be in here.

    // public func createOrder(_ order: Order, completion: (Result<OrderData, ErrorData>) -> Void)
}
```

#### Callbacks

```swift
// createOrder/onApprove/onError callbacks for our UI components
public protocol PaymentDelegate {
    func createOrder(_ sender: PaymentUIComponent, completion: (CreateOrderInput) -> Void)
    func onApprove(_ sender: PaymentUIComponent, data: OrderData, action: ApprovalAction)
    func onError(_ sender: PaymentUIComponent, data: ErrorData)
}
```

#### Order actions

```swift
// The action vended to merchant when the SDK creates an order
// This allows merchants to pass in either an Order object (for client-side create order) or orderID (for server-side create order)
public class CreateOrderAction {
    // Client-side
    public func create(order: Order, completion: (String) -> Void)

    // Server-side
    public func set(orderID: String)
}

// The action vended to merchant after buyer approval
// This allows merchants to capture/authorize orders client-side
public class ApprovalAction {
    // Client-side authorize
    public func authorize(orderId: String, completion: (Result<OrderData, ErrorData>) -> Void) {}

    // Client-side capture
    public func capture(orderId: String, completion: (Result<OrderData, ErrorData>) -> Void) {}
}
```

#### Models

```swift
public class Order {
    var intent: Intent
    var purchaseUnits: [PurchaseUnit]
}

public struct Card: PaymentSource {
    var cardNumber: String
    var cvv: String
    var expiry: String
}

public class OrderData {
    var orderID: String
    var status: OrderStatus
    var paymentSource: PaymentSource?
}

public class ErrorData {
    var error: Error
    var description: String
    var correlationID: String
    var orderID: String
    var sdkVersion: String
}
```
