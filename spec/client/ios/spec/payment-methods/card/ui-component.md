#### CardClient

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
    var submitButton: UIButton

    var type: Type = .single
}
```
