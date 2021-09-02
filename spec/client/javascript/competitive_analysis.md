# Stripe

## Browser Support
[Supported Browsers](https://stripe.com/docs/js/appendix/supported_browsers)

- Support IE11 and above + edge
- Major browsers latest version

## UI Frameworks

[Frameworks](https://stripe.com/docs/stripe-js)

- [Officially support react](https://stripe.com/docs/stripe-js/react)
- [Endorse third party support for angular](https://stripe.com/partners/ngx-stripe)
- [Endorse third party support for vue](https://stripe.com/partners/vue-stripe)

## UI Modularity
[Stripe elements](https://stripe.com/docs/stripe-js#elements)
- Card Elements
- Payment Request Elements (GooglePay, ApplePay, etc.)

## Loading the Client SDK
[Including Stripe](https://stripe.com/docs/js/including)
- Simple versioned script tag
```HTML
<script src="https://js.stripe.com/v3/"></script>
```
- [NPM package](https://github.com/stripe/stripe-js#installation)
```sh
npm install @stripe/stripe-js
```
## Sample Code
```js
import {loadStripe} from '@stripe/stripe-js';

const stripe = await loadStripe('pk_test_TYooMQauvdEDq54NiTphI7jx');

const elements = stripe.elements();
const card = elements.create('card');
card.mount('#card-element');

```

# Adyen

## Browser Support
- Not listed

## UI Frameworks
- Don't have any official packages
- [Include various notes about integrating with frameworks in their documentation](https://docs.adyen.com/online-payments/components-web#step-2-add-components)

## UI Modularity
- Drop-In
- Cards
- Bank Payment Methods
    - SEPA
    - QIWI
    - iDEA

## Loading the Client SDK
[Including Adyen](https://docs.adyen.com/online-payments/drop-in-web?tab=npm_recommended__1#step-2-add-drop-in)

- Simple versioned script tag and versioned css file if using UI library

```html
<script src="https://checkoutshopper-test.adyen.com/checkoutshopper/sdk/{VERSION}/adyen.js"
integrity="sha384-SGA+BK9i1sG5N4BTCgRH6EGbopUK8WG/azn/TeIHYeBEXmEaB+NT+410Z9b1ii7Z"
crossorigin="anonymous"></script>

<link rel="stylesheet" href="https://checkoutshopper-test.adyen.com/checkoutshopper/sdk/{VERSION}/adyen.css"
integrity="sha384-oT6lIQpTr+nOu+yFBPn8mSMkNQID9wuEoTw8lmg2bcrFoDu/Ae8DhJVj+T5cUmsM"
crossorigin="anonymous">
```

- [NPM Package](https://github.com/Adyen/adyen-web)
```sh
npm install @adyen/adyen-web --save
```

## Sample Code

```js
import AdyenCheckout from '@adyen/adyen-web';
import '@adyen/adyen-web/dist/adyen.css';

function handleOnChange(state, component) {}
function handleOnAdditionalDetails(state, component) {}

const checkout = new AdyenCheckout({
    locale: "en_US",
    environment: "test",  
    clientKey: "YOUR_CLIENT_KEY",
    paymentMethodsResponse: paymentMethodsResponse,
    onChange: handleOnChange,
    onAdditionalDetails: handleOnAdditionalDetails
});

const card = checkout.create('card').mount('#component-container');
```