## Payment Links

### Create payment link

Request #1
Standard Payment Link

```java
String json = "{\n" +
              "  \"amount\": 500,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": true,\n" +
              "  \"first_min_partial_amount\": 100,\n" +
              "  \"description\": \"For XYZ purpose\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\",\n" +
              "    \"contact\": \"+919999999999\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": true,\n" +
              "  \"notes\": {\n" +
              "    \"policy_name\": \"Jeevan Bima\"\n" +
              "  },\n" +
              "  \"callback_url\": \"https://example-callback-url.com/\",\n" +
              "  \"callback_method\": \"get\"\n" +
              "}";

JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);
```

Request #2
UPI Payment Link

```java
String json = "{\n" +
              "  \"upi_link\": true,\n" +
              "  \"amount\": 500,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": true,\n" +
              "  \"first_min_partial_amount\": 100,\n" +
              "  \"description\": \"For XYZ purpose\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\",\n" +
              "    \"contact\": \"+919999999999\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": true,\n" +
              "  \"notes\": {\n" +
              "    \"policy_name\": \"Jeevan Bima\"\n" +
              "  }\n" +
              "}";

JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);

```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|upi_link*          | boolean | boolean Must be set to true   //   to creating UPI Payment Link only                                     |
|amount*        | integer  | Amount to be paid using the Payment Link.                     |
|currency           | string  |  A three-letter ISO code for the currency in which you want to accept the payment. For example, INR.                     |
|description           | string  | A brief description of the Payment Link                     |
|reference_id           | string  | AReference number tagged to a Payment Link.                      |
|customer           | object  | name, email, contact                 |
|expire_by           | integer  | Timestamp, in Unix, at which the Payment Link will expire. By default, a Payment Link will be valid for six months from the date of creation.                     |
|notify           | object  | sms or email (boolean)                     |
|notes           | json object  | Key-value pair that can be used to store additional information about the entity. Maximum 15 key-value pairs, 256 characters (maximum) each. For example, "note_key": "Beam me up Scotty”                     |

**Response:**
For create payment link response please click [here](https://razorpay.com/docs/api/payment-links/#create-payment-link)

-------------------------------------------------------------------------------------------------------

### Fetch all payment link

```java
List<PaymentLink> paymentlink = instance.PaymentLink.fetchAll();
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|payment_id          | string | Unique identifier of the payment associated with the Payment Link.                                               |
|reference_id        | string  | The unique reference number entered by you while creating the Payment Link.                     |

**Response:**
For fetch all payment link response please click [here](https://razorpay.com/docs/api/payment-links/#all-payment-links)

-------------------------------------------------------------------------------------------------------

### Fetch specific payment link

```java
String PaymentLinkId = "plink_FMbhpT6nqDjDei";
 
instance.PaymentLink.fetch(PaymentLinkId);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| paymentLinkId*          | string |  Unique identifier of the Payment Link.                         |

**Response:**
For fetch specific payment link response please click [here](https://razorpay.com/docs/api/payment-links/#specific-payment-links-by-id)

-------------------------------------------------------------------------------------------------------

### Update payment link

```java
String PaymentLinkId = "plink_FMbhpT6nqDjDei";

String json = "{\n" +
              "    \"reference_id\": \"TS35\",\n" +
              "    \"expire_by\": 1653347540,\n" +
              "    \"reminder_enable\":false,\n" +
              "    \"notes\":{\n" +
              "      \"policy_name\": \"Jeevan Saral\"\n" +
              "    }\n" +
              "}";
              
JSONObject request = new JSONObject(json);
              
PaymentLink paymentlink = instance.PaymentLink.edit(PaymentId,request);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| paymentLinkId*          | string | The unique identifier of the Payment Link that needs to be updated.                         |
| accept_partial         | boolean | Indicates whether customers can make partial payments using the Payment Link. Possible values: true - Customer can make partial payments. false (default) - Customer cannot make partial payments.                         |
| reference_id          | string | Adds a unique reference number to an existing link.                         |
| expire_by         | integer | Timestamp, in Unix format, when the payment links should expire.                         |
| notes          | string | object Key-value pair that can be used to store additional information about the entity. Maximum 15 key-value pairs, 256 characters (maximum) each. For example, "note_key": "Beam me up Scotty”.                         |

**Response:**
For updating payment link response please click [here](https://razorpay.com/docs/api/payment-links/#update-payment-link)

-------------------------------------------------------------------------------------------------------

### Cancel a payment link

```java
String PaymentLinkId = "plink_FMbhpT6nqDjDei";

PaymentLink paymentlink = instance.PaymentLink.cancel(PaymentLinkId,medium);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| paymentLinkId*          | string | Unique identifier of the Payment Link.                         |

**Response:**
For canceling payment link response please click [here](https://razorpay.com/docs/api/payment-links/#cancel-payment-link)
-------------------------------------------------------------------------------------------------------

### Send notification

```java
String PaymentLinkId = "plink_FMbhpT6nqDjDei";

String medium = "email";

PaymentLink paymentlink = instance.PaymentLink.notifyBy(PaymentLinkId,medium);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| paymentLinkId*          | string | Unique identifier of the Payment Link that should be resent.                         |
| medium*          | string | `sms`/`email`,Medium through which the Payment Link must be resent. Allowed values are:           |

**Response:**
```json
{
    "success": true
}
```
-------------------------------------------------------------------------------------------------------

### Transfer payments received using payment links

```java
String json = "{\n" +
              "  \"amount\": 20000,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": false,\n" +
              "  \"description\": \"For XYZ purpose\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\",\n" +
              "    \"contact\": \"+919999999999\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": true,\n" +
              "  \"options\": {\n" +
              "    \"order\": [\n" +
              "      {\n" +
              "        \"account\": \"acc_CNo3jSI8OkFJJJ\",\n" +
              "        \"amount\": 500,\n" +
              "        \"currency\": \"INR\",\n" +
              "        \"notes\": {\n" +
              "          \"branch\": \"Acme Corp Bangalore North\",\n" +
              "          \"name\": \"Saurav Kumar\",\n" +
              "          \"linked_account_notes\": [\n" +
              "            \"branch\"\n" +
              "          ]\n" +
              "        }\n" +
              "      }\n" +
              "    ]\n" +
              "  }\n" +
              "}";

JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);

```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|amount*        | integer  | Amount to be paid using the Payment Link.                     |
|options*           | array  |  Options to configure the transfer in the Payment Link. Parent parameter under which the order child parameter must be passed.                     |

**Response:**
```json
{
  "accept_partial": false,
  "amount": 1500,
  "amount_paid": 0,
  "callback_method": "",
  "callback_url": "",
  "cancelled_at": 0,
  "created_at": 1596526969,
  "currency": "INR",
  "customer": {
    "contact": "+919999999999",
    "email": "gaurav.kumar@example.com",
    "name": "Gaurav Kumar"
  },
  "deleted_at": 0,
  "description": "Payment for policy no #23456",
  "expire_by": 0,
  "expired_at": 0,
  "first_min_partial_amount": 0,
  "id": "plink_FMbhpT6nqDjDei",
  "notes": null,
  "notify": {
    "email": true,
    "sms": true
  },
  "payments": null,
  "reference_id": "#aasasw8",
  "reminder_enable": true,
  "reminders": [],
  "short_url": "https://rzp.io/i/ORor1MT",
  "source": "",
  "source_id": "",
  "status": "created",
  "updated_at": 1596526969,
  "user_id": ""
}
```
-------------------------------------------------------------------------------------------------------

### Offers on payment links

```java
String json = "{\n" +
              "  \"amount\": 3400,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": false,\n" +
              "  \"reference_id\": \"#425\",\n" +
              "  \"description\": \"Payment for policy no #23456\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"contact\": \"+919999999999\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": false,\n" +
              "  \"options\": {\n" +
              "    \"order\": {\n" +
              "      \"offers\": [\n" +
              "        \"offer_F4WMTC3pwFKnzq\",\n" +
              "        \"offer_F4WJHqvGzw8dWF\"\n" +
              "      ]\n" +
              "    }\n" +
              "  }\n" +
              "}";
              
JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);

```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|amount*        | integer  | Amount to be paid using the Payment Link.                     |
|currency           | string  |  A three-letter ISO code for the currency in which you want to accept the payment. For example, INR.                     |
|description           | string  | A brief description of the Payment Link                     |
|reference_id           | string  | AReference number tagged to a Payment Link.                      |
|customer           | array  | name, email, contact                 |
|expire_by           | integer  | Timestamp, in Unix, at which the Payment Link will expire. By default, a Payment Link will be valid for six months from the date of creation.                     |
|notify           | object  | sms or email (boolean)                     |
|options*        | array  | Options to associate the offer_id with the Payment Link. Parent parameter under which the order child parameter must be passed.                     |

**Response:**
```json
{
  "accept_partial": false,
  "amount": 3400,
  "amount_paid": 0,
  "cancelled_at": 0,
  "created_at": 1600183040,
  "currency": "INR",
  "customer": {
    "contact": "+919999999999",
    "email": "gaurav.kumar@example.com",
    "name": "Gaurav Kumar"
  },
  "description": "Payment for policy no #23456",
  "expire_by": 0,
  "expired_at": 0,
  "first_min_partial_amount": 0,
  "id": "plink_FdLt0WBldRyE5t",
  "notes": null,
  "notify": {
    "email": true,
    "sms": true
  },
  "payments": null,
  "reference_id": "#425",
  "reminder_enable": false,
  "reminders": [],
  "short_url": "https://rzp.io/i/CM5ohDC",
  "status": "created",
  "user_id": ""
}
```
-------------------------------------------------------------------------------------------------------

### Managing reminders for payment links

```java
String json = "{\n" +
              "  \"amount\": 1000,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": true,\n" +
              "  \"first_min_partial_amount\": 100,\n" +
              "  \"reference_id\": \"#425\",\n" +
              "  \"description\": \"Payment for policy no #23456\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"contact\": \"+919999999999\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": false\n" +
              "}";
              
JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);

```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|amount*        | integer  | Amount to be paid using the Payment Link.                     |
|accept_partial        | boolean  |  Indicates whether customers can make partial payments using the Payment Link. Possible values:true - Customer can make partial payments.false (default) - Customer cannot make partial payments.                     |
|currency           | string  |  A three-letter ISO code for the currency in which you want to accept the payment. For example, INR.                     |
|description           | string  | A brief description of the Payment Link                     |
|customer           | object  | name, email, contact                 |
|expire_by           | integer  | Timestamp, in Unix, at which the Payment Link will expire. By default, a Payment Link will be valid for six months from the date of creation.                     |
|notify           | object  | sms or email (boolean)                     |
|reminder_enable       | boolean  | To disable reminders for a Payment Link, pass reminder_enable as false                     |

**Response:**
```json
{
  "amount": 340000,
  "amount_due": 340000,
  "amount_paid": 0,
  "billing_end": null,
  "billing_start": null,
  "cancelled_at": null,
  "comment": null,
  "created_at": 1592579126,
  "currency": "INR",
  "currency_symbol": "₹",
  "customer_details": {
    "billing_address": null,
    "contact": "9900990099",
    "customer_contact": "9900990099",
    "customer_email": "gaurav.kumar@example.com",
    "customer_name": "Gaurav Kumar",
    "email": "gaurav.kumar@example.com",
    "gstin": null,
    "id": "cust_F4WNtqj1xb0Duv",
    "name": "Gaurav Kumar",
    "shipping_address": null
  },
  "customer_id": "cust_F4WNtqj1xb0Duv",
  "date": 1592579126,
  "description": "Salon at Home Service",
  "email_status": null,
  "entity": "invoice",
  "expire_by": 1608390326,
  "expired_at": null,
  "first_payment_min_amount": 0,
  "gross_amount": 340000,
  "group_taxes_discounts": false,
  "id": "inv_F4WfpZLk1ct35b",
  "invoice_number": null,
  "issued_at": 1592579126,
  "line_items": [],
  "notes": [],
  "order_id": "order_F4WfpxUzWmYOTl",
  "paid_at": null,
  "partial_payment": false,
  "payment_id": null,
  "receipt": "5757",
  "reminder_enable": false,
  "short_url": "https://rzp.io/i/vitLptM",
  "sms_status": null,
  "status": "issued",
  "tax_amount": 0,
  "taxable_amount": 0,
  "terms": null,
  "type": "link",
  "user_id": "",
  "view_less": true
}
```
-------------------------------------------------------------------------------------------------------

### Rename labels in checkout section

```java
String json = "{\n" +
              "  \"amount\": 500,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": true,\n" +
              "  \"first_min_partial_amount\": 100,\n" +
              "  \"description\": \"For XYZ purpose\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\",\n" +
              "    \"contact\": \"+919999999999\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": true,\n" +
              "  \"options\": {\n" +
              "    \"checkout\": {\n" +
              "      \"partial_payment\": {\n" +
              "        \"min_amount_label\": \"Minimum Money to be paid\",\n" +
              "        \"partial_amount_label\": \"Pay in parts\",\n" +
              "        \"partial_amount_description\": \"Pay at least ₹100\",\n" +
              "        \"full_amount_label\": \"Pay the entire amount\"\n" +
              "      }\n" +
              "    }\n" +
              "  }\n" +
              "}";
              
JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|amount*        | integer  | Amount to be paid using the Payment Link.                     |
|accept_partial        | boolean  |  Indicates whether customers can make partial payments using the Payment Link. Possible values:true - Customer can make partial payments.false (default) - Customer cannot make partial payments.                     |
|currency           | string  |  A three-letter ISO code for the currency in which you want to accept the payment. For example, INR.                     |
|description           | string  | A brief description of the Payment Link                     |
|customer           | object  | name, email, contact                 |
|expire_by           | integer  | Timestamp, in Unix, at which the Payment Link will expire. By default, a Payment Link will be valid for six months from the date of creation.                     |
|notify           | object  | sms or email (boolean)                     |
|reminder_enable       | boolean  | To disable reminders for a Payment Link, pass reminder_enable as false                     |
|options*       | object  | Options to rename the labels for partial payment fields in the checkout form. Parent parameter under which the checkout and partial_payment child parameters must be passed. |

**Response:**
```json
{
  "accept_partial": true,
  "amount": 1000,
  "amount_paid": 0,
  "callback_method": "",
  "callback_url": "",
  "cancelled_at": 0,
  "created_at": 1596193199,
  "currency": "INR",
  "customer": {
    "contact": "+919999999999",
    "email": "gaurav.kumar@example.com",
    "name": "Gaurav Kumar"
  },
  "deleted_at": 0,
  "description": "Payment for policy no #23456",
  "expire_by": 0,
  "expired_at": 0,
  "first_min_partial_amount": 100,
  "id": "plink_FL4vbXVKfW7PAz",
  "notes": null,
  "notify": {
    "email": true,
    "sms": true
  },
  "payments": null,
  "reference_id": "#42321",
  "reminder_enable": true,
  "reminders": [],
  "short_url": "https://rzp.io/i/F4GC9z1",
  "source": "",
  "source_id": "",
  "status": "created",
  "updated_at": 1596193199,
  "user_id": ""
}
```
-------------------------------------------------------------------------------------------------------

### Change Business name

```java
String json = "{\n" +
              "  \"amount\": 1000,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": true,\n" +
              "  \"first_min_partial_amount\": 100,\n" +
              "  \"reference_id\": \"#2234542\",\n" +
              "  \"description\": \"Payment for policy no #23456\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"contact\": \"+919999999999\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": true,\n" +
              "  \"options\": {\n" +
              "    \"checkout\": {\n" +
              "      \"name\": \"Lacme Corp\"\n" +
              "    }\n" +
              "  }\n" +
              "}";
              
JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|amount*        | integer  | Amount to be paid using the Payment Link.                     |
|currency           | string  |  A three-letter ISO code for the currency in which you want to accept the payment. For example, INR.                     |
|accept_partial        | boolean  |  Indicates whether customers can make partial payments using the Payment Link. Possible values:true - Customer can make partial payments.false (default) - Customer cannot make partial payments.                     |
|first_min_partial_amount        | integer  |                      |
|description           | string  | A brief description of the Payment Link                     |
|customer           | object  | name, email, contact                 |
|notify           | object  | sms or email (boolean)                     |
|reminder_enable       | boolean  | To disable reminders for a Payment Link, pass reminder_enable as false                     |
|options*       | object  | Option to customize the business name. Parent parameter under which the checkout child parameter must be passed.|

**Response:**
```json
{
  "accept_partial": true,
  "amount": 1000,
  "amount_paid": 0,
  "callback_method": "",
  "callback_url": "",
  "cancelled_at": 0,
  "created_at": 1596187657,
  "currency": "INR",
  "customer": {
    "contact": "+919999999999",
    "email": "gaurav.kumar@example.com",
    "name": "Gaurav Kumar"
  },
  "description": "Payment for policy no #23456",
  "expire_by": 0,
  "expired_at": 0,
  "first_min_partial_amount": 100,
  "id": "plink_FL3M2gJFs1Jkma",
  "notes": null,
  "notify": {
    "email": true,
    "sms": true
  },
  "payments": null,
  "reference_id": "#2234542",
  "reminder_enable": true,
  "reminders": [],
  "short_url": "https://rzp.io/i/at2OOsR",
  "source": "",
  "source_id": "",
  "status": "created",
  "updated_at": 1596187657,
  "user_id": ""
}
```
-------------------------------------------------------------------------------------------------------

### Prefill checkout fields

```java
String json = "{\n" +
              "  \"amount\": 1000,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": true,\n" +
              "  \"first_min_partial_amount\": 100,\n" +
              "  \"reference_id\": \"#417\",\n" +
              "  \"description\": \"Payment for policy no #23456\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"contact\": \"+919999999999\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": true,\n" +
              "  \"options\": {\n" +
              "    \"checkout\": {\n" +
              "      \"prefill\": {\n" +
              "        \"method\": \"card\",\n" +
              "        \"card[name]\": \"Gaurav Kumar\",\n" +
              "        \"card[number]\": \"4111111111111111\",\n" +
              "        \"card[expiry]\": \"12/21\",\n" +
              "        \"card[cvv]\": \"123\"\n" +
              "      }\n" +
              "    }\n" +
              "  }\n" +
              "}";
              
JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);

```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|amount*        | integer  | Amount to be paid using the Payment Link.                     |
|currency           | string  |  A three-letter ISO code for the currency in which you want to accept the payment. For example, INR.                     |
|accept_partial        | boolean  |  Indicates whether customers can make partial payments using the Payment Link. Possible values:true - Customer can make partial payments.false (default) - Customer cannot make partial payments.                     |
|first_min_partial_amount        | integer  |                      |
|description           | string  | A brief description of the Payment Link                     |
|customer           | object  | name, email, contact                 |
|notify           | object  | sms or email (boolean)                     |
|reminder_enable       | boolean  | To disable reminders for a Payment Link, pass reminder_enable as false                     |
|options*       | array  | Options to customize Checkout. Parent parameter under which the checkout and prefill child parameters must be passed.|

**Response:**
For prefill checkout fields response please click [here](https://razorpay.com/docs/payment-links/api/new/advanced-options/customize/prefill/)

-------------------------------------------------------------------------------------------------------

### Customize payment methods

```java 
String json = "{\n" +
              "  \"amount\": 500,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": true,\n" +
              "  \"first_min_partial_amount\": 100,\n" +
              "  \"description\": \"For XYZ purpose\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\",\n" +
              "    \"contact\": \"+919999999999\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": true,\n" +
              "  \"options\": {\n" +
              "    \"checkout\": {\n" +
              "      \"method\": {\n" +
              "        \"netbanking\": \"1\",\n" +
              "        \"card\": \"1\",\n" +
              "        \"upi\": \"0\",\n" +
              "        \"wallet\": \"0\"\n" +
              "      }\n" +
              "    }\n" +
              "  }\n" +
              "}";
              
JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|amount*        | integer  | Amount to be paid using the Payment Link.                     |
|currency           | string  |  A three-letter ISO code for the currency in which you want to accept the payment. For example, INR.                     |
|accept_partial        | boolean  |  Indicates whether customers can make partial payments using the Payment Link. Possible values:true - Customer can make partial payments.false (default) - Customer cannot make partial payments.                     |
|first_min_partial_amount        | integer  |                      |
|description           | string  | A brief description of the Payment Link                     |
|customer           | object  | name, email, contact                 |
|notify           | object  | sms or email (boolean)                     |
|reminder_enable       | boolean  | To disable reminders for a Payment Link, pass reminder_enable as false                     |
|options*       | object  | Options to display or hide payment methods on the Checkout section. Parent parameter under which the checkout and method child parameters must be passed.|

**Response:**
```json
{
  "accept_partial": true,
  "amount": 1000,
  "amount_paid": 0,
  "callback_method": "",
  "callback_url": "",
  "cancelled_at": 0,
  "created_at": 1596188371,
  "currency": "INR",
  "customer": {
    "contact": "+919999999999",
    "email": "gaurav.kumar@example.com",
    "name": "Gaurav Kumar"
  },
  "deleted_at": 0,
  "description": "Payment for policy no #23456",
  "expire_by": 0,
  "expired_at": 0,
  "first_min_partial_amount": 100,
  "id": "plink_FL3YbdvN2Cj6gh",
  "notes": null,
  "notify": {
    "email": true,
    "sms": true
  },
  "payments": null,
  "reference_id": "#543422",
  "reminder_enable": true,
  "reminders": [],
  "short_url": "https://rzp.io/i/wKiXKud",
  "source": "",
  "source_id": "",
  "status": "created",
  "updated_at": 1596188371,
  "user_id": ""
}
```
-------------------------------------------------------------------------------------------------------

### Set checkout fields as read-only

```java
String json = "{\n" +
              "  \"amount\": 1000,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": true,\n" +
              "  \"first_min_partial_amount\": 100,\n" +
              "  \"reference_id\": \"#20\",\n" +
              "  \"description\": \"Payment for policy no #23456\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"contact\": \"+919999999999\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": true,\n" +
              "  \"options\": {\n" +
              "    \"checkout\": {\n" +
              "      \"readonly\": {\n" +
              "        \"email\": \"1\",\n" +
              "        \"contact\": \"1\"\n" +
              "      }\n" +
              "    }\n" +
              "  }\n" +
              "}";
              
JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|amount*        | integer  | Amount to be paid using the Payment Link.                     |
|currency           | string  |  A three-letter ISO code for the currency in which you want to accept the payment. For example, INR.                     |
|accept_partial        | boolean  |  Indicates whether customers can make partial payments using the Payment Link. Possible values:true - Customer can make partial payments.false (default) - Customer cannot make partial payments.                     |
|first_min_partial_amount        | integer  |                      |
|description           | string  | A brief description of the Payment Link                     |
|customer           | object  | name, email, contact                 |
|notify           | object  | sms or email (boolean)                     |
|reminder_enable       | boolean  | To disable reminders for a Payment Link, pass reminder_enable as false                     |
|options*       | object  | Options to set contact and email as read-only fields on Checkout. Parent parameter under which the checkout and readonly child parameters must be passed.|

**Response:**
```json
{
  "accept_partial": true,
  "amount": 1000,
  "amount_paid": 0,
  "callback_method": "",
  "callback_url": "",
  "cancelled_at": 0,
  "created_at": 1596190845,
  "currency": "INR",
  "customer": {
    "contact": "+919999999999",
    "email": "gaurav.kumar@example.com",
    "name": "Gaurav Kumar"
  },
  "deleted_at": 0,
  "description": "Payment for policy no #23456",
  "expire_by": 0,
  "expired_at": 0,
  "first_min_partial_amount": 100,
  "id": "plink_FL4GA1t6FBcaVR",
  "notes": null,
  "notify": {
    "email": true,
    "sms": true
  },
  "payments": null,
  "reference_id": "#19129",
  "reminder_enable": true,
  "reminders": [],
  "short_url": "https://rzp.io/i/QVwUglR",
  "source": "",
  "source_id": "",
  "status": "created",
  "updated_at": 1596190845,
  "user_id": ""
}
```
-------------------------------------------------------------------------------------------------------

### Implement thematic changes in payment links checkout section

```java
String json = "{\n" +
              "  \"amount\": 1000,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": true,\n" +
              "  \"first_min_partial_amount\": 100,\n" +
              "  \"reference_id\": \"#423212\",\n" +
              "  \"description\": \"Payment for policy no #23456\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"contact\": \"+919999999999\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": true,\n" +
              "  \"options\": {\n" +
              "    \"checkout\": {\n" +
              "      \"theme\": {\n" +
              "        \"hide_topbar\": true\n" +
              "      }\n" +
              "    }\n" +
              "  }\n" +
              "}";
              
JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|amount*        | integer  | Amount to be paid using the Payment Link.                     |
|currency           | string  |  A three-letter ISO code for the currency in which you want to accept the payment. For example, INR.                     |
|accept_partial        | boolean  |  Indicates whether customers can make partial payments using the Payment Link. Possible values:true - Customer can make partial payments.false (default) - Customer cannot make partial payments.                     |
|first_min_partial_amount        | integer  |                      |
|description           | string  | A brief description of the Payment Link                     |
|customer           | object  | name, email, contact                 |
|notify           | object  | sms or email (boolean)                     |
|reminder_enable       | boolean  | To disable reminders for a Payment Link, pass reminder_enable as false                     |
|options*       | object  | Options to show or hide the top bar. Parent parameter under which the checkout and theme child parameters must be passed.|

**Response:**
```json
{
  "accept_partial": true,
  "amount": 1000,
  "amount_paid": 0,
  "callback_method": "",
  "callback_url": "",
  "cancelled_at": 0,
  "created_at": 1596187814,
  "currency": "INR",
  "customer": {
    "contact": "+919999999999",
    "email": "gaurav.kumar@example.com",
    "name": "Gaurav Kumar"
  },
  "description": "Payment for policy no #23456",
  "expire_by": 0,
  "expired_at": 0,
  "first_min_partial_amount": 100,
  "id": "plink_FL3Oncr7XxXFf6",
  "notes": null,
  "notify": {
    "email": true,
    "sms": true
  },
  "payments": null,
  "reference_id": "#423212",
  "reminder_enable": true,
  "reminders": [],
  "short_url": "https://rzp.io/i/j45EmLE",
  "source": "",
  "source_id": "",
  "status": "created",
  "updated_at": 1596187814,
  "user_id": ""
}
```
-------------------------------------------------------------------------------------------------------

### Rename labels in payment details section

```java
String json = "{\n" +
              "  \"amount\": 1000,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"accept_partial\": true,\n" +
              "  \"first_min_partial_amount\": 100,\n" +
              "  \"reference_id\": \"#421\",\n" +
              "  \"description\": \"Payment for policy no #23456\",\n" +
              "  \"customer\": {\n" +
              "    \"name\": \"Gaurav Kumar\",\n" +
              "    \"contact\": \"+919999999999\",\n" +
              "    \"email\": \"gaurav.kumar@example.com\"\n" +
              "  },\n" +
              "  \"notify\": {\n" +
              "    \"sms\": true,\n" +
              "    \"email\": true\n" +
              "  },\n" +
              "  \"reminder_enable\": true,\n" +
              "  \"options\": {\n" +
              "    \"checkout\": {\n" +
              "      \"partial_payment\": {\n" +
              "        \"min_amount_label\": \"Minimum Money to be paid\",\n" +
              "        \"partial_amount_label\": \"Pay in parts\",\n" +
              "        \"partial_amount_description\": \"Pay at least ₹100\",\n" +
              "        \"full_amount_label\": \"Pay the entire amount\"\n" +
              "      }\n" +
              "    }\n" +
              "  }\n" +
              "}";
              
JSONObject request = new JSONObject(json);
              
PaymentLink payment = instance.PaymentLink.create(request);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
|amount*        | integer  | Amount to be paid using the Payment Link.                     |
|currency           | string  |  A three-letter ISO code for the currency in which you want to accept the payment. For example, INR.                     |
|accept_partial        | boolean  |  Indicates whether customers can make partial payments using the Payment Link. Possible values:true - Customer can make partial payments.false (default) - Customer cannot make partial payments.                     |
|first_min_partial_amount        | integer  |                      |
|description           | string  | A brief description of the Payment Link                     |
|customer           | object  | name, email, contact                 |
|notify           | object  | sms or email (boolean)                     |
|reminder_enable       | boolean  | To disable reminders for a Payment Link, pass reminder_enable as false                     |
|options*       | object  | Parent parameter under which the hosted_page and label child parameters must be passed.|

**Response:**
For rename labels in payment details section response please click [here](https://razorpay.com/docs/payment-links/api/new/advanced-options/customize/rename-payment-details-labels/)

-------------------------------------------------------------------------------------------------------

**PN: * indicates mandatory fields**
<br>
<br>
**For reference click [here](https://razorpay.com/docs/api/payment-links/)**