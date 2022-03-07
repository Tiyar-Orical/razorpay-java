## UPI

### Create customer
```java
String json = "{\n" +
              "  name: \"Gaurav Kumar\",\n" +
              "  contact: 9123456780,\n" +
              "  email: \"gaurav.kumar@example.com\",\n" +
              "  notes: {\n" +
              "    notes_key_1: \"Tea, Earl Grey, Hot\",\n" +
              "    notes_key_2: \"Tea, Earl Grey… decaf.\"\n" +
              "  }\n" +
              "}";
              
JSONObject request = new JSONObject(json);   
          
Customer customer = instance.Customers.create(request);
```

**Parameters:**

| Name          | Type        | Description                                 |
|---------------|-------------|---------------------------------------------|
| name*          | string      | Name of the customer                        |
| email        | string      | Email of the customer                       |
| contact      | string      | Contact number of the customer              |
| notes         | object      | A key-value pair                            |

**Response:**
```json
{
  "id": "cust_1Aa00000000003",
  "entity": "customer",
  "name": "Gaurav Kumar",
  "email": "Gaurav.Kumar@example.com",
  "contact": "9000000000",
  "gstin": null,
  "notes": {
    "notes_key_1": "Tea, Earl Grey, Hot",
    "notes_key_2": "Tea, Earl Grey… decaf."
  },
  "created_at": 1582033731
}
```

-------------------------------------------------------------------------------------------------------

### Create order

```java
String json = "{\n" +
              "  amount: 0,\n" +
              "  currency: \"INR\",\n" +
              "  method: \"upi\",\n" +
              "  customer_id: \"cust_1Aa00000000001\",\n" +
              "  receipt: \"Receipt No. 1\",\n" +
              "  notes: {\n" +
              "    notes_key_1: \"Beam me up Scotty\",\n" +
              "    notes_key_2: \"Engage\"\n" +
              "  },\n" +
              "  token: {\n" +
              "    auth_type: \"netbanking\",\n" +
              "    max_amount: 9999900,\n" +
              "    expire_at: 4102444799,\n" +
              "    notes: {\n" +
              "      notes_key_1: \"Tea, Earl Grey, Hot\",\n" +
              "      notes_key_2: \"Tea, Earl Grey… decaf.\"\n" +
              "    }\n" +
              "  }\n" +
              "}";
              
JSONObject request = new JSONObject(json);         
       
Order order = instance.Orders.create(request);

```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| amount*          | integer | Amount of the order to be paid                                               |
| currency*        | string  | Currency of the order. Currently only `INR` is supported.                      |
| method*        | string  | The authorization method. In this case the value will be `emandate`                      |
| receipt         | string  | Your system order reference id.                                              |
| notes           | object  | A key-value pair                                                             |
| token           | object  | A key-value pair                                                             |

**Response:**
```json
{
  "id": "order_1Aa00000000002",
  "entity": "order",
  "amount": 100,
  "amount_paid": 0,
  "amount_due": 100,
  "currency": "INR",
  "receipt": "Receipt No. 1",
  "offer_id": null,
  "status": "created",
  "attempts": 0,
  "notes": {
    "notes_key_1": "Tea, Earl Grey, Hot",
    "notes_key_2": "Tea, Earl Grey… decaf."
    },
  "created_at": 1565172642
}
```
-------------------------------------------------------------------------------------------------------

### Create an Authorization Payment

Please refer this [doc](https://razorpay.com/docs/api/recurring-payments/upi/authorization-transaction/#113-create-an-authorization-payment) for authorization payment

-------------------------------------------------------------------------------------------------------

### Create registration link

```java
String json = "{\n" +
              "  customer: {\n" +
              "    name: \"Gaurav Kumar\",\n" +
              "    email: \"gaurav.kumar@example.com\",\n" +
              "    contact: 9123456780\n" +
              "  },\n" +
              "  type: \"link\",\n" +
              "  amount: 100,\n" +
              "  currency: \"INR\",\n" +
              "  description: \"Registration Link for Gaurav Kumar\",\n" +
              "  subscription_registration: {\n" +
              "    method: \"upi\",\n" +
              "    max_amount: 500,\n" +
              "    expire_at: 1634215992\n" +
              "  },\n" +
              "  receipt: \"Receipt No. 5\",\n" +
              "  email_notify: 1,\n" +
              "  sms_notify: 1,\n" +
              "  expire_by: 1634215992,\n" +
              "  notes: {\n" +
              "    \"note_key 1\": \"Beam me up Scotty\",\n" +
              "    \"note_key 2\": \"Tea. Earl Gray. Hot.\"\n" +
              "  }\n" +
              "}";
JSONObject request = new JSONObject(json);       
        
Invoice invoice = instance.Invoices.createRegistrationLink(request);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| customer          | object | Details of the customer to whom the registration link will be sent.           |
| type*        | string  | In this case, the value is `link`.                      |
| currency*        | string  | The 3-letter ISO currency code for the payment. Currently, only `INR` is supported. |
| amount*         | integer  | The payment amount in the smallest currency sub-unit.                 |
| description*    | string  | A description that appears on the hosted page. For example, `12:30 p.m. Thali meals (Gaurav Kumar`).                                                             |
| subscription_registration           | object  | Details of the authorization payment.                      |
| notes           | object  | A key-value pair                                                             |

**Response:**
```json
{
  "id": "inv_FHr1ekX0r2VCVK",
  "entity": "invoice",
  "receipt": "Receipt No. 23",
  "invoice_number": "Receipt No. 23",
  "customer_id": "cust_BMB3EwbqnqZ2EI",
  "customer_details": {
    "id": "cust_BMB3EwbqnqZ2EI",
    "name": "Gaurav Kumar",
    "email": "gaurav.kumar@example.com",
    "contact": "9123456780",
    "gstin": null,
    "billing_address": null,
    "shipping_address": null,
    "customer_name": "Gaurav Kumar",
    "customer_email": "gaurav.kumar@example.com",
    "customer_contact": "9123456780"
  },
  "order_id": "order_FHr1ehR3nmNeXo",
  "line_items": [],
  "payment_id": null,
  "status": "issued",
  "expire_by": 4102444799,
  "issued_at": 1595489219,
  "paid_at": null,
  "cancelled_at": null,
  "expired_at": null,
  "sms_status": "pending",
  "email_status": "pending",
  "date": 1595489219,
  "terms": null,
  "partial_payment": false,
  "gross_amount": 100,
  "tax_amount": 0,
  "taxable_amount": 0,
  "amount": 100,
  "amount_paid": 0,
  "amount_due": 100,
  "currency": "INR",
  "currency_symbol": "₹",
  "description": "Registration Link for Gaurav Kumar",
  "notes": {
    "note_key 1": "Beam me up Scotty",
    "note_key 2": "Tea. Earl Gray. Hot."
  },
  "comment": null,
  "short_url": "https://rzp.io/i/ak1WxDB",
  "view_less": true,
  "billing_start": null,
  "billing_end": null,
  "type": "link",
  "group_taxes_discounts": false,
  "created_at": 1595489219,
  "idempotency_key": null
}
```
-------------------------------------------------------------------------------------------------------

### Send/Resend notifications

```java
String InvoiceId = "inv_DAweOiQ7amIUVd";

String medium = "sms";

Invoice invoice = instance.Invoices.notifyBy(InvoiceId,medium);
```

**Parameters:**

| Name       | Type    | Description                                                                  |
|------------|---------|------------------------------------------------------------------------------|
| InvoiceId* | string | The id of the invoice to be notified                         |
| medium*    | string | `sms`/`email`, Medium through which notification should be sent.                         |

**Response:**
```json
{
    "success": true
}
```
-------------------------------------------------------------------------------------------------------

### Cancel a registration link

```java
String InvoiceId = "inv_DAweOiQ7amIUVd";

Invoice invoice = instance.Invoices.cancel(InvoiceId);
```

**Parameters:**

| Name       | Type    | Description                                                                  |
|------------|---------|------------------------------------------------------------------------------|
| InvoiceId* | string | The id of the invoice to be cancelled                         |

**Response:**
```json
{
    "id": "inv_FHrfRupD2ouKIt",
    "entity": "invoice",
    "receipt": "Receipt No. 1",
    "invoice_number": "Receipt No. 1",
    "customer_id": "cust_BMB3EwbqnqZ2EI",
    "customer_details": {
        "id": "cust_BMB3EwbqnqZ2EI",
        "name": "Gaurav Kumar",
        "email": "gaurav.kumar@example.com",
        "contact": "9123456780",
        "gstin": null,
        "billing_address": null,
        "shipping_address": null,
        "customer_name": "Gaurav Kumar",
        "customer_email": "gaurav.kumar@example.com",
        "customer_contact": "9123456780"
    },
    "order_id": "order_FHrfRw4TZU5Q2L",
    "line_items": [],
    "payment_id": null,
    "status": "cancelled",
    "expire_by": 4102444799,
    "issued_at": 1595491479,
    "paid_at": null,
    "cancelled_at": 1595491488,
    "expired_at": null,
    "sms_status": "sent",
    "email_status": "sent",
    "date": 1595491479,
    "terms": null,
    "partial_payment": false,
    "gross_amount": 100,
    "tax_amount": 0,
    "taxable_amount": 0,
    "amount": 100,
    "amount_paid": 0,
    "amount_due": 100,
    "currency": "INR",
    "currency_symbol": "₹",
    "description": "Registration Link for Gaurav Kumar",
    "notes": {
        "note_key 1": "Beam me up Scotty",
        "note_key 2": "Tea. Earl Gray. Hot."
    },
    "comment": null,
    "short_url": "https://rzp.io/i/QlfexTj",
    "view_less": true,
    "billing_start": null,
    "billing_end": null,
    "type": "link",
    "group_taxes_discounts": false,
    "created_at": 1595491480,
    "idempotency_key": null
}
```
-------------------------------------------------------------------------------------------------------

### Fetch token by payment ID

```java
String PaymentId = "pay_1Aa00000000001";

Payment payment = instance.Payments.fetch(PaymentId)
```

**Parameters:**

| Name       | Type   | Description                       |
|------------|--------|-----------------------------------|
| PaymentId* | string | Id of the payment to be retrieved |

**Response:**
```json
{
  "id": "pay_FHfAzEJ51k8NLj",
  "entity": "payment",
  "amount": 100,
  "currency": "INR",
  "status": "captured",
  "order_id": "order_FHfANdTUYeP8lb",
  "invoice_id": null,
  "international": false,
  "method": "upi",
  "amount_refunded": 0,
  "refund_status": null,
  "captured": true,
  "description": null,
  "card_id": null,
  "bank": null,
  "wallet": null,
  "vpa": "gaurav.kumar@upi",
  "email": "gaurav.kumar@example.com",
  "contact": "+919876543210",
  "customer_id": "cust_DtHaBuooGHTuyZ",
  "token_id": "token_FHfAzGzREc1ug6",
  "notes": {
    "note_key 1": "Beam me up Scotty",
    "note_key 2": "Tea. Earl Gray. Hot."
  },
  "fee": 0,
  "tax": 0,
  "error_code": null,
  "error_description": null,
  "error_source": null,
  "error_step": null,
  "error_reason": null,
  "acquirer_data": {
    "rrn": "854977234911",
    "upi_transaction_id": "D0BED5A062ECDB3E9B3A1071C96BB273"
  },
  "created_at": 1595447490
}
```
-------------------------------------------------------------------------------------------------------

### Fetch tokens by customer ID

```java
String CustomerId = "cust_BMB3EwbqnqZ2EI";

List<Token> token = instance.Customers.fetchTokens(CustomerId);
```

**Parameters:**

| Name        | Type        | Description                                 |
|-------------|-------------|---------------------------------------------|
| CustomerId* | string      | The id of the customer to be fetched |

**Response:**
```json
{
  "entity": "collection",
  "count": 1,
  "items": [
    {
      "id": "token_FHfAzGzREc1ug6",
      "entity": "token",
      "token": "9KHsdPaCELeQ0t",
      "bank": null,
      "wallet": null,
      "method": "upi",
      "vpa": {
        "username": "gaurav.kumar",
        "handle": "upi",
        "name": null
      },
      "recurring": true,
      "recurring_details": {
        "status": "confirmed",
        "failure_reason": null
      },
      "auth_type": null,
      "mrn": null,
      "used_at": 1595447490,
      "created_at": 1595447490,
      "start_time": 1595447455,
      "dcc_enabled": false
    }
  ]
}
```
-------------------------------------------------------------------------------------------------------

### Delete token

```java
String CustomerId = "cust_BMB3EwbqnqZ2EI";

String TokenId = "token_FHf94Uym9tdYFJ";

instance.Customers.deleteToken(CustomerId, TokenId);
```

**Parameters:**

| Name        | Type        | Description                                 |
|-------------|-------------|---------------------------------------------|
| CustomerId* | string      | The id of the customer to be fetched |
| TokenId*    | string      | The id of the token to be fetched |

**Response:**
```json
{
    "deleted": true
}
```
-------------------------------------------------------------------------------------------------------

### Create an order to charge the customer

```java
String json = "{\n" +
              "  \"amount\": \"100\",\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"receipt\": \"Receipt No. 1\",\n" +
              "  \"notes\": {\n" +
              "    \"key1\": \"value3\",\n" +
              "    \"key2\": \"value2\"\n" +
              "  }\n" +
              "}";
              
JSONObject request = new JSONObject(json);         
       
Order order = instance.Orders.create(request);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| amount*          | integer | Amount of the order to be paid                                               |
| currency*        | string  | Currency of the order. Currently only `INR` is supported.                      |
| receipt         | string  | Your system order reference id.                                              |
| notes           | object  | A key-value pair                                                             |

**Response:**
```json
{
   "id":"order_1Aa00000000002",
   "entity":"order",
   "amount":1000,
   "amount_paid":0,
   "amount_due":1000,
   "currency":"INR",
   "receipt":"Receipt No. 1",
   "offer_id":null,
   "status":"created",
   "attempts":0,
   "notes":{
      "notes_key_1":"Tea, Earl Grey, Hot",
      "notes_key_2":"Tea, Earl Grey… decaf."
   },
   "created_at":1579782776
}
```
-------------------------------------------------------------------------------------------------------

### Create a recurring payment

```java
String json = "{\n" +
              "  \"email\": \"gaurav.kumar@example.com\",\n" +
              "  \"contact\": \"9123456789\",\n" +
              "  \"amount\": 1000,\n" +
              "  \"currency\": \"INR\",\n" +
              "  \"order_id\": \"order_1Aa00000000002\",\n" +
              "  \"customer_id\": \"cust_1Aa00000000001\",\n" +
              "  \"token\": \"token_1Aa00000000001\",\n" +
              "  \"recurring\": \"1\",\n" +
              "  \"description\": \"Creating recurring payment for Gaurav Kumar\",\n" +
              "  \"notes\": {\n" +
              "    \"note_key 1\": \"Beam me up Scotty\",\n" +
              "    \"note_key 2\": \"Tea. Earl Gray. Hot.\"\n" +
              "  }\n" +
              "}";
  
JSONObject request = new JSONObject(json);  
              
Payment payment = instance.Payments.createRecurringPayment(request);
```

**Parameters:**

| Name            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| email*          | string | The customer's email address.                                               |
| contact*        | string  | The customer's phone number.                      |
| amount*         | integer  | The amount you want to charge your customer. This should be the same as the amount in the order.                        |
| currency*        | string  | The 3-letter ISO currency code for the payment. Currently, only `INR` is supported. |
| order_id*        | string  | The unique identifier of the order created. |
| customer_id*        | string  | The `customer_id` for the customer you want to charge.  |
| token*        | string  | The `token_id` generated when the customer successfully completes the authorization payment. Different payment instruments for the same customer have different `token_id`.|
| recurring*        | string  | Determines if recurring payment is enabled or not. Possible values:<br>* `1` - Recurring is enabled.* `0` - Recurring is not enabled.|
| description*        | string  | A user-entered description for the payment.|
| notes*        | object  | Key-value pair that can be used to store additional information about the entity. Maximum 15 key-value pairs, 256 characters (maximum) each. |

**Response:**
```json
{
  "razorpay_payment_id" : "pay_1Aa00000000001",
  "razorpay_order_id" : "order_1Aa00000000001",
  "razorpay_signature" : "9ef4dffbfd84f1318f6739a3ce19f9d85851857ae648f114332d8401e0949a3d"
}
```
-------------------------------------------------------------------------------------------------------



**PN: * indicates mandatory fields**
<br>
<br>
**For reference click [here](https://razorpay.com/docs/api/recurring-payments/upi/authorization-transaction/)**