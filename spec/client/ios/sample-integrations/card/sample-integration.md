## Sample card integration

### 1. Using your UI components

```swift
import CardPayment

class MerchantViewController: UIViewController {

    // Initialize CoreConfig and CardClient
    let config = CoreConfig(clientID: "ABCD1234", environment: .sandbox)
    lazy var cardClient: CardClient = { CardClient(config: config) }()

    // Your UI components
    let cardNumberField = UITextField() 
    let cvvField = UITextField()
    let expiryField = UITextField() 
    lazy var submitButton: UIButton = {
        let button = UIButton()
        button.addTarget(self, action: #selector(submit), for: .touchUpInside)
    }()

    override func viewDidLoad() {
        super.viewDidLoad()
        
        // <Not implemented> Client-side create order.
        // Not necessary if the order is created from server-side
        let order = Order(
            intent: .authorize
            purchaseUnits: [PurchaseUnit(amount: Amount(currencyCode: .usd, value: 5))]
        )
        cardClient.createOrder(order) { result in
            switch result {
            case .success(let data):
                // Save orderID here
                print(data.orderID)
            case .failure(let data):
                // Handle error here
                print(data.error)
            }
        }
    }

    @objc
    func submit(_ sender: UIButton) {
        // Create Card from buyer's inputs and approve the order

        let card = Card(
            number: cardNumberField.text
            cvv: cvvField.text
            expiry: expiryField.text
        )
        cardClient.approveOrder(orderID: <orderID>, card: card) {
            switch result {
            case let .success(data, action):
                // Authorize/capture the order

                switch data.intent {
                case .authorize:
                    // <Not implemented> Client-side
                    action.authorize() { result in }

                    // OR Server-side
                    Network.post("merchant/api/to/authorize/order", data.orderID) { _ in }
                case .capture:
                    // <Not implemented> Client-side
                    action.capture() { result in }

                    // OR Server-side
                    Network.post("merchant/api/to/capture/order", data.orderID) { _ in }
                }
            case let .failure(data):
                // Handle error here
                print(data.error)
            }
        }
    }
}
```

### 2. Using the SDK's card field UI component

```swift
import CardPayment

class MerchantViewController: UIViewController {

    // Initialize CoreConfig and CardFields UI component
    let config = CoreConfig(clientID: "ABCD1234", environment: .sandbox)
    lazy var cardFields: CardFields = { 
        // CardFields with built-in submit button
        CardFields(config: config, type: .multi) 

        // OR CardFields with your submit button
        CardFields(config: config, type: .multi, submitButton: <yourUIButton>)
    }()

    override func viewDidLoad() {
        super.viewDidLoad()

        // Set PaymentDelegate to respond to createOrder/onApprove/onError.
        config.delegate = self
    }
}

extension MerchantViewController: PaymentDelegate {

    func createOrder(_ sender: PaymentUIComponent, action: CreateOrderAction) {
        // The SDK is requesting an Order or orderID to create the order

        // <Not implemented> Client-side
        let order = Order(
            intent: .authorize
            purchaseUnits: [PurchaseUnit(amount: Amount(currencyCode: .usd, value: 5))]
        )
        action.create(order: order)

        // OR Server-side
        Network.post("merchant/api/to/create/order") { result in
            switch result {
            case .success(let orderID):
                action.completion(orderID)
            case .failure:
                action.completion(nil)
            }
        }
    }

    func onApprove(_ sender: PaymentUIComponent, data: OrderData, action: ApprovalAction) {
        // Buyer has finished approving the order and the SDK is requesting you to handle authorizing/capturing the order

        switch data.intent {
        case .authorize:
            // <Not implemented> Client-side
            action.authorize() { result in }

            // OR Server-side
            Network.post("merchant/api/to/authorize/order", data.orderID) { _ in }
        case .capture:
            // <Not implemented> Client-side
            action.capture() { result in }

            // OR Server-side
            Network.post("merchant/api/to/capture/order", data.orderID) { _ in }
        }
    }

    func onError(_ sender: PaymentUIComponent, data: ErrorData) {
        // The SDK encountered an error. You can handle the error here.
        print(data.error)
    }
}
```
