## Payments

### Capture payment

```java
String paymentId = "pay_G8VQzjPLoAvm6D";
String jsonRequest = "{\n" +
              "  \"amount\": 1000,\n" +
              "  \"currency\": \"INR\"\n" +
              "}";

JSONObject requestRequest = new JSONObject(jsonRequest);

Payment payment = instance.payments.capture(paymentId, requestRequest);
```

**Parameters:**

| Name       | Type    | Description                                                                    |
|------------|---------|--------------------------------------------------------------------------------|
| paymentId* | string  | Id of the payment to capture                                                   |
| amount*    | integer | The amount to be captured (should be equal to the authorized amount, in paise) |
| currency   | string  | The currency of the payment (defaults to INR)                                  |

**Response:**
```json
{
  "id": "pay_G8VQzjPLoAvm6D",
  "entity": "payment",
  "amount": 1000,
  "currency": "INR",
  "status": "captured",
  "order_id": "order_G8VPOayFxWEU28",
  "invoice_id": null,
  "international": false,
  "method": "upi",
  "amount_refunded": 0,
  "refund_status": null,
  "captured": true,
  "description": "Purchase Shoes",
  "card_id": null,
  "bank": null,
  "wallet": null,
  "vpa": "gaurav.kumar@exampleupi",
  "email": "gaurav.kumar@example.com",
  "contact": "+919999999999",
  "customer_id": "cust_DitrYCFtCIokBO",
  "notes": [],
  "fee": 24,
  "tax": 4,
  "error_code": null,
  "error_description": null,
  "error_source": null,
  "error_step": null,
  "error_reason": null,
  "acquirer_data": {
    "rrn": "033814379298"
  },
  "created_at": 1606985209
}
```
-------------------------------------------------------------------------------------------------------

### Fetch all payments

```java
String jsonRequest = "{\n" +
                 "\"count\" : 1\n" +
               "}";

JSONObject requestJson = new JSONObject(jsonRequest);

List<Payment> payment = instance.payments.fetchAll(requestJson);
```

**Parameters:**

| Name  | Type      | Description                                      |
|-------|-----------|--------------------------------------------------|
| from  | timestamp | timestamp after which the payments were created  |
| to    | timestamp | timestamp before which the payments were created |
| count | integer   | number of payments to fetch (default: 10)        |
| skip  | integer   | number of payments to be skipped (default: 0)    |

**Response:**
```json
{
  "entity": "collection",
  "count": 2,
  "items": [
    {
      "id": "pay_G8VaL2Z68LRtDs",
      "entity": "payment",
      "amount": 900,
      "currency": "INR",
      "status": "captured",
      "order_id": "order_G8VXfKDWDEOHHd",
      "invoice_id": null,
      "international": false,
      "method": "netbanking",
      "amount_refunded": 0,
      "refund_status": null,
      "captured": true,
      "description": "Purchase Shoes",
      "card_id": null,
      "bank": "KKBK",
      "wallet": null,
      "vpa": null,
      "email": "gaurav.kumar@example.com",
      "contact": "+919999999999",
      "customer_id": "cust_DitrYCFtCIokBO",
      "notes": [],
      "fee": 22,
      "tax": 4,
      "error_code": null,
      "error_description": null,
      "error_source": null,
      "error_step": null,
      "error_reason": null,
      "acquirer_data": {
        "bank_transaction_id": "0125836177"
      },
      "created_at": 1606985740
    }
  ]
}
```
-------------------------------------------------------------------------------------------------------

### Fetch a payment

```java
String paymentId = "pay_G8VQzjPLoAvm6D";

Payment payment = instance.payments.fetch(paymentId);
```

**Parameters:**

| Name       | Type   | Description                       |
|------------|--------|-----------------------------------|
| PaymentId* | string | Id of the payment to be retrieved |

**Response:**
```json
{
  "id": "pay_G8VQzjPLoAvm6D",
  "entity": "payment",
  "amount": 1000,
  "currency": "INR",
  "status": "captured",
  "order_id": "order_G8VPOayFxWEU28",
  "invoice_id": null,
  "international": false,
  "method": "upi",
  "amount_refunded": 0,
  "refund_status": null,
  "captured": true,
  "description": "Purchase Shoes",
  "card_id": null,
  "bank": null,
  "wallet": null,
  "vpa": "gaurav.kumar@exampleupi",
  "email": "gaurav.kumar@example.com",
  "contact": "+919999999999",
  "customer_id": "cust_DitrYCFtCIokBO",
  "notes": [],
  "fee": 24,
  "tax": 4,
  "error_code": null,
  "error_description": null,
  "error_source": null,
  "error_step": null,
  "error_reason": null,
  "acquirer_data": {
    "rrn": "033814379298"
  },
  "created_at": 1606985209
}
```
-------------------------------------------------------------------------------------------------------

### Fetch payments for an order

```java
String orderId = "order_DovFx48wjYEr2I";

Order order = instance.orders.fetchPayments(orderId)
```
**Parameters**

| Name     | Type   | Description                         |
|----------|--------|-------------------------------------|
| orderId* | string | The id of the order to be retrieve payment info |

**Response:**
```json
{
  "count": 1,
  "entity": "collection",
  "items": [
    {
      "id": "pay_DovGQXOkPBJjjU",
      "entity": "payment",
      "amount": 600,
      "currency": "INR",
      "status": "captured",
      "order_id": "order_DovFx48wjYEr2I",
      "method": "netbanking",
      "amount_refunded": 0,
      "refund_status": null,
      "captured": true,
      "description": "A Wild Sheep Chase is a novel by Japanese author Haruki Murakami",
      "card_id": null,
      "bank": "SBIN",
      "wallet": null,
      "vpa": null,
      "email": "gaurav.kumar@example.com",
      "contact": "9364591752",
      "fee": 70,
      "tax": 10,
      "error_code": null,
      "error_description": null,
      "error_source": null,
      "error_step": null,
      "error_reason": null,
      "notes": [],
      "acquirer_data": {
        "bank_transaction_id": "0125836177"
      },
      "created_at": 1400826750
    }
  ]
}
```
-------------------------------------------------------------------------------------------------------

### Update a payment

```java
String paymentId = "pay_CBYy6tLmJTzn3Q";

String jsonRequest = "{\n" +
              "  \"notes\": {\n" +
              "       \"key1\": \"value1\",\n" +
              "       \"key2\": \"value2\"\n" +
              "  }\n" +
              "}";
              
JSONObject requestRequest = new JSONObject(jsonRequest);
              
Payment payment = instance.payments.edit(PaymentId,requestRequest);
```

**Parameters:**

| Name       | Type    | Description                          |
|------------|---------|--------------------------------------|
| PaymentId* | string  | Id of the payment to update          |
| notes*     | object  | A key-value pair                   |

**Response:**
```json
{
  "id": "pay_CBYy6tLmJTzn3Q",
  "entity": "payment",
  "amount": 1000,
  "currency": "INR",
  "status": "authorized",
  "order_id": null,
  "invoice_id": null,
  "international": false,
  "method": "netbanking",
  "amount_refunded": 0,
  "refund_status": null,
  "captured": false,
  "description": null,
  "card_id": null,
  "bank": "UTIB",
  "wallet": null,
  "vpa": null,
  "email": "testme@acme.com",
  "notes": {
    "key1": "value1",
    "key2": "value2"
  },
  "fee": null,
  "tax": null,
  "error_code": null,
  "error_description": null,
  "error_source": null,
  "error_step": null,
  "error_reason": null,
  "acquirer_data": {
    "bank_transaction_id": "0125836177"
  },
  "created_at": 1553504328
}
```
-------------------------------------------------------------------------------------------------------

### Fetch expanded card or emi details for payments

Request #1: Card

```java
String jsonRequest = "{\"expand[]\":\"card\"}";

JSONObject requestRequest = new JSONObject(jsonRequest);

List<Payment> payment = instance.payments.fetchAll(requestRequest);
```

Request #2: EMI

```java
String jsonRequest = "{\"expand[]\":\"emi\"}";

JSONObject requestRequest = new JSONObject(jsonRequest);

List<Payment> payment = instance.Payments.fetchAll(requestRequest);
```

**Response:**

For expanded card or emi details for payments response please click [here](https://razorpay.com/docs/api/payments/#fetch-expanded-card-or-emi-details-for-payments)

-------------------------------------------------------------------------------------------------------

### Fetch card details with paymentId

```java
String paymentId = "pay_CBYy6tLmJTzn3Q";

Card card = instance.cards.fetchCardDetails(paymentId);
```

**Parameters:**

| Name       | Type    | Description                          |
|------------|---------|--------------------------------------|
| paymentId* | string  | Id of the payment to update          |

**Response:**
```json
{
  "id": "card_6krZ6bcjoeqyV9",
  "entity": "card",
  "name": "Gaurav",
  "last4": "3335",
  "network": "Visa",
  "type": "debit",
  "issuer": "SBIN",
  "international": false,
  "emi": null,
  "sub_type": "business"
}
```
-------------------------------------------------------------------------------------------------------

### Fetch Payment Downtime Details

```java
List<Payment> payment = instance.Payments.fetchPaymentDowntime();
```
**Response:**

For payment downtime response please click [here](https://razorpay.com/docs/api/payments/downtime/#fetch-payment-downtime-details)

-------------------------------------------------------------------------------------------------------

### Fetch Payment Downtime Details By Downtime Id

```java
String DowntimeId = "down_F7LroRQAAFuswd";

instance.payments.fetchPaymentDowntimeById(DowntimeId);
```

**Parameters:**

| Name        | Type    | Description                          |
|-------------|---------|--------------------------------------|
| DowntimeId* | string  | Id to fetch payment downtime         |

**Response:**
For payment downtime by id response please click [here](https://razorpay.com/docs/api/payments/downtime/#fetch-payment-downtime-details-by-id)
-------------------------------------------------------------------------------------------------------

### Payment capture settings API

```java
String jsonRequest = "{\n" +
                   "  \"amount\":50000,\n" +
                   "  \"currency\": \"INR\",\n" +
                   "  \"receipt\": \"rcptid_11\",\n" +
                   "  \"payment\": {\n" +
                   "    \"capture\": \"automatic\",\n" +
                   "    \"capture_options\": {\n" +
                   "      \"automatic_expiry_period\": 12,\n" +
                   "      \"manual_expiry_period\": 7200,\n" +
                   "      \"refund_speed\": \"optimum\"\n" +
                   "    }  \n" +
                   "  }\n" +
                   "}";

JSONObject requestRequest = new JSONObject(jsonRequest);
              
instance.orders.create(requestRequest);
```

**Parameters:**

| Name        | Type    | Description                          |
|-------------|---------|--------------------------------------|
| amount*          | integer | Amount of the order to be paid                                               |
| currency*        | string  | Currency of the order. Currently only `INR` is supported.       |
| receipt         | string  | Your system order reference id.                                              |
| payment         | object  | please refer this [doc](https://razorpay.com/docs/payments/payments/capture-settings/api/) for params                       |

**Response:**
```json
{
  "id": "order_DBJOWzybf0sJbb",
  "entity": "order",
  "amount": 50000,
  "amount_paid": 0,
  "amount_due": 50000,
  "currency": "INR",
  "receipt": "rcptid_11",
  "status": "created",
  "attempts": 0,
  "notes": [],
  "created_at": 1566986570
}
```
-------------------------------------------------------------------------------------------------------

### Create Payment Json

```java
String jsonRequest = "{\n" +
            "  \"amount\": 100,\n" +
            "  \"currency\": \"INR\",\n" +
            "  \"order_id\": \"order_EAkbvXiCJlwhHR\",\n" +
            "  \"email\": \"gaurav.kumar@example.com\",\n" +
            "  \"contact\": 9090909090,\n" +
            "  \"method\": \"card\",\n" +
            "  \"card\":{\n" +
            "    \"number\": 4111111111111111,\n" +
            "    \"name\": \"Gaurav\",\n" +
            "    \"expiry_month\": 11,\n" +
            "    \"expiry_year\": 23,\n" +
            "    \"cvv\": 100\n" +
            "  }\n" +
            "}";
              
JSONObject requestRequest = new JSONObject(jsonRequest);
              
instance.payments.createJsonPayment(requestRequest);
```

**Parameters:**

 please refer this [doc](https://razorpay.com/docs/payment-gateway/s2s-integration/payment-methods/) for params

**Response:** <br>
```json
{
  "razorpay_payment_id": "pay_FVmAstJWfsD3SO",
  "next": [
    {
      "action": "redirect",
      "url": "https://api.razorpay.com/v1/payments/FVmAtLUe9XZSGM/authorize"
    },
    {
      "action": "otp_generate",
      "url": "https://api.razorpay.com/v1/payments/pay_FVmAstJWfsD3SO/otp_generate?track_id=FVmAtLUe9XZSGM&key_id=<YOUR_KEY_ID>"
    }
  ]
}
```

**PN: * indicates mandatory fields**
<br>
<br>
**For reference click [here](https://razorpay.com/docs/api/payments/)**