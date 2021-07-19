---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the OpenDigitalPay.io API! 

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# OpenPay
## Create balance account
```shell
curl -X POST http://opendigitalpay.io/api/v1/order \
-H "Content-Type: application/json" --data-raw \
'{
      "customer_id" : 1231231,
      "business_id" : 13123131
      "reference_id": "my-order-001",
      "line_items": [
        {
          "name": "New York Strip Steak",
          "quantity": "1",
          "base_price_money": {
            "amount": 1599,
            "currency": "USD"
          }
        }
      ]
      metadata: {}
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": 1142342135234
}
```

This endpoint creates an payment order

## Get order detail

```shell
curl -X GET http://opendigitalpay.io/api/v1/user/{id}
```

> The above command returns JSON structured like this:

```json
{
      "id"          : 1212131231,
      "customer_id" : 1231231,
      "business_id" : 13123131
      "reference_id": "my-order-001",
      "line_items": [
        {
          "name": "New York Strip Steak",
          "quantity": "1",
          "base_price_money": {
            "amount": 1599,
            "currency": "USD"
          }
        }
      ],
      "metadata": {}
}
```
This endpoint retrieves detail info for an order.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://opendigitalpay.io/api/v1/order/{id}`

### URL Parameters

Parameter | Description
--------- | -----------
id | The order id 

## Pay an order

```shell
curl "http://opendigitalpay.io/api/v1/orders/{order_id}/pay" \
  -X POST \
'{
    "payment_source": {
        "type": "TOKEN"
        "value": "tok_xxxx"
        or 
        "type": "PAYMENT_METHOD_ID"
        "value": "123232"
        or 
        "type"  "BALANCE_ACCOUNT_ID"
        "value": "1232ddd32"
        or 
        "type"  "Interact"
        "value": "interactServiceRequestId"

    }
}
'
```

> The above command returns JSON structured like this:

```json
{
    "id": 13412123100, 
    "created_at": 1212312993
}
```

This endpoint initiates submit a payment request for a given order
<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://opendigitalpay.io/api/v1/orders/{order_id}/pay`

### URL Parameters

Parameter | Description
--------- | -----------
order_id | The order id 

# OpenBalance

## Create balance account
```shell
curl -X POST http://opendigitalpay.io/api/v1/user \
-H "Content-Type: application/json" --data-raw \
'{
    "email": "x@gmail.com", 
    "phone": "423423",      
    "userName" "coderx"     
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": 134124141241,
    "email": "x@gmail.com",
    "phone": "423423",
    "userName": "coderx",
    "created_at": 123192912991
}
```

This endpoint create balance accounts for a user.

## Get balance account Detail

```shell
curl -X GET http://opendigitalpay.io/api/v1/user/{id}
```

> The above command returns JSON structured like this:

```json
{
    "id": 134124141241,
    "email": "x@gmail.com",
    "phone": "423423",
    "userName": "coderx",
    "created_at": 1342423423,
    "updated_at": 123192912991
    "meta": {
        
    }
    "balanceAccounts": [
        {
            "balance": 123234200,
            "currency": "CAD",
            "type": "CASH",
            "meta": {

            },
            "state": "active"
        }
    ]
}

```

This endpoint retrieves balance account detail for a user.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://opendigitalpay.io/api/v1/user/{id}`

### URL Parameters

Parameter | Description
--------- | -----------
id | The user id 

## Try a topup txn

```shell
curl "http://opendigitalpay.io/api/v1/topup/try" \
  -X POST \
'{
    "userId": 1212412412,
    "amount": 11231200,
    "currency": "CAD",
    "meta: {

    }
}'
```

> The above command returns JSON structured like this:

```json
{
    "id": 13412123100, 
    "created_at": 1212312993
}
```

This endpoint initiate a try operation for a topup transaction

## Commit a Topup txn

```shell
curl "http://opendigitalpay.io/api/v1/topup/commit" \
  -X POST \
'{
    "id": 13412123100, 
    "meta": {
    }
}'
```

This endpoint perform a commit operation for a topup transaction


## Cancel a Topup Txn

```shell
curl "http://opendigitalpay.io/api/v1/topup/cancel" \
  -X POST \
'{
    "id": 13412123100, 
    "meta": {
    }
}'
```

This endpoint perform a cancel operation for a topup transaction
