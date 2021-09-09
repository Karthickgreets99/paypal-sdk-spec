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

    // <Not implemented>
    public func createOrder(_ order: Order, completion: (Result<OrderData, ErrorData>) -> Void)
}
```

#### Callbacks

```swift
// createOrder/onApprove/onError callbacks for our UI components
public protocol PaymentDelegate {
    func createOrder(_ sender: PaymentUIComponent, action: CreateOrderAction)
    func onApprove(_ sender: PaymentUIComponent, data: OrderData, action: ApprovalAction)
    func onError(_ sender: PaymentUIComponent, data: ErrorData)
}
```

#### Order actions

```swift
// The action vended to merchant when the SDK creates an order
// This allows merchants to pass in an Order (request the SDK to create order) or an orderID (if the order was created from merchants' server)
public class CreateOrderAction {
    // <Not implemented> Client-side
    public func create(order: Order, completion: (String?) -> Void)

    // Server-side
    public func completion(orderID: String?)
}

// The action vended to merchant after buyer approval
// This allows merchants to capture/authorize orders client-side
public class ApprovalAction {
    // <Not implemented> Client-side authorize
    public func authorize(orderId: String, completion: (Result<OrderData, ErrorData>) -> Void) {}

    // <Not implemented> Client-side capture
    public func capture(orderId: String, completion: (Result<OrderData, ErrorData>) -> Void) {}
}
```

#### Models

```swift
public class Order {
    var intent: Intent
    var purchaseUnits: [PurchaseUnit]
}

public class OrderData {
    var orderID: String
    var status: OrderStatus
    var paymentSource: PaymentSource?
}

public class ErrorData {
    var error: SDKError
    var orderID: String?
    var sdkVersion: String
}

public enum SDKError: Error {
    case networkError(metaData: [String: Any], correlationID: String)
    case decodingError
    ...

    var errorCode: Int
    var errorUserInfo: [String: Any]
}
```
