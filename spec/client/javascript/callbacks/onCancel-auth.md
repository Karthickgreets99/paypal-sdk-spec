# onCancel Auth

Callback used to signal user consent cancelled due to an incomplete auth button flow.

## Examples


### Capture cancel consent code

```javascript
const onCancel = (data) => {
    // data will contain information about the canceled consent request
    // sample data object {"errorCode":"Consent denied"}
};
```

## Types

```typescript
type OnCancel = (
    data : OnCancelData,
    actions : OnCancelActions
) => void | Promise<void>

// __TODO__
// Cancel Data will have consent denied object and based on that partner can show appropriate screen for user.
type OnCancelData = {
    // consent denied object  {"error_code" : consent_denied}
};
// __TODO__
// Based on cancel data partner can  guide the next action for the user.
type OnCancelActions = {
    // appropriate action for cancel.
};
```
