## Core spec

#### CoreConfig

```swift
// Contains shared data that applies to every payment method
public struct CoreConfig {
    let clientID: String
    let environment: Environment
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
