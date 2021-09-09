## Not implemented

#### Create + approve + capture order in one step (data handler)

```swift
public class CardClient: Client {
    public func completeOrder(_ order: Order, card: Card, completion: (Result<OrderData, ErrorData>) -> Void)
}
```

#### Client-side create order (data handler)

```swift
public class Client {
    public func createOrder(_ order: Order, completion: (Result<OrderData, ErrorData>) -> Void)
}
```
#### Client-side create order (CreateOrderAction)

```swift
public class CreateOrderAction {
    public func create(order: Order, completion: (String?) -> Void)
}
```

#### Client-side capture/authorize order (ApprovalAction)

```swift
public class ApprovalAction {
    public func authorize(orderId: String, completion: (Result<OrderData, ErrorData>) -> Void) {}
    public func capture(orderId: String, completion: (Result<OrderData, ErrorData>) -> Void) {}
}
```

#### CardFields (UI component)

```swift
// Card fields UI component
public class CardFields: PaymentUIComponent {

    public enum Type {
        // single or multiple card fields
        case single
        case multi
    }

    var config: CoreConfig

    var cardNumberField: UITextField
    var cvvField: UITextField
    var expiryField: UITextField
    var submitButton: UIButton?

    var type: Type = .single

    public init(config: CoreConfig, type: Type = .single, submitButton: UIButton?)

    func submit(card: Card)
}
```
