# Getting Started - PayPal JS SDK

Welcome to PayPal's JS SDK getting started guide. Learn how to accept payments on your website using card, PayPal, Venmo, and alternative payment methods.

## Browser Support

See [Support](./standards/support.md')

## UI Frameworks
 - React
 - Angular
 - Vue

## UI Modularity
- [CardFields](./components/card-fields/index.md)
- [Buttons](./components/buttons/index.md)
- [Marks (Radio Buttons)](./components/marks/index.md)
- [Messaging](./components/messages/index.md)

## Loading the Client SDK

There are two ways you can load the client side SDK:

1. You can add it in a script tag on the page.

Sample Code:
```html
<script src="https://www.paypal.com/sdk/js?client-id=<YOUR_CLIENT_ID>" />
```

```js
window.paypal.Buttons().render('#paypal-buttons-container');
```

2. You can install as a module from npm.

Sample Code:
```sh
npm install @paypal/paypal-js
```

```js
import { loadScript } from "paypal";

const configuration = {
  clientID: '<YOUR_CLIENT_ID>',
};

try {
  const paypal = await loadScript(configuration)
} catch(error) {
  console.error(error.code);
}

paypal.Buttons().render('#paypal-buttons-container');
```

