# Scopes

The `scope` prop is used to request specific information about a user.

```javascript
paypal.AuthButton({
    scopes: ['openid', 'profile', 'email', 'address', 'phone']
    // add rest of your props here
});
```

## Common Scopes

The following table shows how user attributes map to scopes.

| User Attribute | Category             | Scope Value |
| -------------- | -------------------- | ----------- |
| None           | Basic Authentication | `openid`    |
| Full Name      | Personal Information | `profile`   |
| Email address  | Address Information  | `email`     | 
| Street address | Address Information  | `address`   |
| City           | Address Information  | `address`   |
| State          | Address Information  | `address`   |
| Country        | Address Information  | `address`   |
| Zip code       | Address Information  | `address`   |
