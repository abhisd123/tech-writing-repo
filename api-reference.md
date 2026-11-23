# Create a Payment Intent

The `POST /v1/payment_intents` endpoint creates a new Payment Intent object to track the lifecycle of a customer checkout session.

## Authentication
This endpoint requires a Bearer token in the authorization header.
`Authorization: Bearer <sk_live_token>`

## Request

**Endpoint:** `POST https://api.example-pay.com/v1/payment_intents`  
**Content-Type:** `application/json`

### Body Parameters

| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `amount` | integer | Yes | The amount to charge, represented in the smallest currency unit (e.g., cents). |
| `currency` | string | Yes | Three-letter ISO currency code, in lowercase. |
| `payment_method` | string | No | The ID of the payment method to attach to this Payment Intent. |
| `receipt_email` | string | No | Email address where the receipt should be sent upon successful payment. |

### Request Example

```json
{
  "amount": 2500,
  "currency": "usd",
  "payment_method": "pm_card_visa",
  "receipt_email": "customer@example.com"
}

## Response

```json
{
  "id": "pi_1Hh1XYZ",
  "object": "payment_intent",
  "amount": 2500,
  "currency": "usd",
  "status": "requires_confirmation",
  "client_secret": "pi_1Hh1XYZ_secret_abc123"
}

## Error Codes

- 400 Bad Request: Missing required parameters.<br>
- 401 Unauthorized: Invalid or missing API key.<br>
