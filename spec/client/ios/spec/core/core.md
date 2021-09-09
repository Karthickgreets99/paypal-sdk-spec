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
public class Client {}
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
// This allows merchants to pass in an orderID (created from merchants' server)
public class CreateOrderAction {
    // Server-side
    public func completion(orderID: String?)
}

// The action vended to merchant after buyer approval
// This allows merchants to capture/authorize orders client-side
public class ApprovalAction {}
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
