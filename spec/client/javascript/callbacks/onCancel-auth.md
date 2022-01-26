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

```javascript
type OnCancel = (
    data : OnCancelData,
    actions : OnCancelActions
) => undefined | Promise<undefined>
// Cancel Data will have consent denied and based on that partner can show appropriate screen
type OnCancelData = {
    // Example of the consent denied  {"error_code" : consent_denied}
};
// Based on cancel data partner can  guide the next action for the user.
type OnCancelActions = {
    // appropriate action for cancel.
};
```
