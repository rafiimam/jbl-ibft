# IBFT

Interbank fund-transfer path for Jamuna Bank PLC, built against the ITCL-style switch. The channel submits a transfer intent. This service validates it, attaches an idempotency key, and hands the request to payment middleware. It does not store a beneficiary account in the public sample.

This repository is a sanitized public sample.

## What I owned

I built the Node API in front of the switch: routes, controllers, middleware, and services. The channel never sees the switch host. Validation happens here, before any outbound call.

## Technologies

- Node.js and Express
- Controllers, services, middleware, and utils split so validation is not inside the route
- Shared idempotency rules with payment middleware
- Environment-only switch URL and credentials

## Features

- Positive amount check
- Request shape validated before the switch is called
- Masked references only in any response this sample would return
- Middleware for the auth header the channel must present
- No beneficiary account numbers and no switch credentials in this repository

## Design choice

IBFT is a special case of a payment, not a reason to skip the payment router. This service owns the switch-specific fields. Payment middleware owns accept, retry, and fail.

Related: [Payment Middleware](https://github.com/rafiimam/jbl-payment-middleware)

Portfolio: https://rafiimam.github.io/rafi_portfolio/
