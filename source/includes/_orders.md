# Orders

> Here's an example order

```json
{
	"order": {
		"id": "364a726b-419f-4156-ac29-71e2f1c6aefa",
		"updated_at": "2018-01-12T13:04:40.540Z",
		"created_at": "2018-01-12T13:04:38.517Z",
		"legacy_id": null,
		"number": 1,
		"status": "concept",
		"starts_at": null,
		"stops_at": null,
		"price": 0.0,
		"price_with_tax": 0.0,
		"grand_total": 0.0,
		"grand_total_with_tax": 0.0,
		"price_in_cents": 0,
		"price_with_tax_in_cents": 0,
		"customer_id": null,
		"grand_total_in_cents": 0,
		"grand_total_with_tax_in_cents": 0,
		"paid_in_cents": 0,
		"deposit_paid_in_cents": 0,
		"discount_percentage": 0.0,
		"discount_in_cents": 0,
		"discount_with_tax_in_cents": 0,
		"deposit_in_cents": 0,
		"deposit_type": "none",
		"deposit_value": 0.0,
		"tags": [],
		"tax_region_id": null,
		"item_count": 0,
		"entirely_started": true,
		"entirely_stopped": true,
		"item_ids": [],
		"stock_item_ids": [],
		"invoice_count": 0,
		"price_as_decimal": 0,
		"price_with_tax_as_decimal": 0,
		"grand_total_as_decimal": 0,
		"grand_total_with_tax_as_decimal": 0,
		"paid_as_decimal": 0,
		"deposit_paid_as_decimal": 0,
		"discount_as_decimal": 0,
		"discount_with_tax_as_decimal": 0,
		"deposit_as_decimal": 0,
		"plannings": [],
		"notes": [],
		"tax_values": [],
		"lines": [],
		"properties": []
	}
}
```

This resource contains all the information about an order, such as the period, customer and products booked on it.
It has the following attributes:

| Field                     | Type     | Description                   |
|---------------------------|----------|-------------------------------|
| `id`                      | Integer  | `Readonly` Unique primary id |
| `number`                  | Integer  | `Unique` Order number |
| `status`                  | String   | `Readonly` Status of the order |
| `customer`                | Customer | Associated customer. See [Customer](#customers) |
| `customer_id`             | Integer  | `Optional` ID of the associated customer |
| `starts_at`               | DateTime | Start date and time of the order |
| `stops_at`                | DateTime | Stop date and time of the order |
| `price_in_cents`          | Integer  | `Readonly` Price in cents without tax |
| `price_with_tax_in_cents` | Integer  | `Readonly` Price in cents with tax |
| `created_at`              | DateTime | `Readonly` When the order was created |
| `updated_at`              | DateTime | `Readonly` When the order was last updated |

When retrieving an order it will include more attributes:

| Field                     | Type     | Description                   |
|---------------------------|----------|-------------------------------|
| `plannings`               | Array    | Associated planning. See [Planning](#planning) |
| `lines`                   | Array    | Associated order lines. See [OrderLine](#orderline) |
| `tax_values`              | Array    | Associated tax values. See [TaxValue](#taxvalues) |
| `notes`                   | Array    | Associated notes. See [Note](#notes) |

## List all orders

> Example request

```shell
curl --request GET \
  --url 'https://example.booqable.com/api/1/orders'
```

> This request returns JSON structured like this

```json
{
    "orders": [
        {
            "id": "364a726b-419f-4156-ac29-71e2f1c6aefa",
            "number": 1,
            "status": "concept",
            ...
        },
        {
            "id": "ea024c26-c322-485b-85ad-f67b890e5346",
            "number": 2,
            "status": "started",
            "starts_at": "2018-01-26T13:45:00.000Z",
            "stops_at": "2018-01-30T13:45:00.000Z",
            "customer_id": "63a28c67-259c-4a27-a482-2aac3c5d705d",
            ...
            "customer": {
                "id": "63a28c67-259c-4a27-a482-2aac3c5d705d",
                "name": "Customer Deee",
                ...
            }
        }
    ],
    "meta": {
        "total_count": 2,
        "total_item_count": 1.0,
        "facets": {
            "tag_list": {
                ...
            },
            "status": {
                "_type": "terms",
                "missing": 0,
                "total": 2,
                "other": 0,
                "terms": [
                    {
                        "term": "started",
                        "count": 1
                    },
                    {
                        "term": "concept",
                        "count": 1
                    }
                ]
            }
        }
    }
}
```

This endpoint retrieves all orders and can paginated

### HTTP Request

`GET /orders` or
`GET /orders?per=:per&page=:page` or
`GET /orders?q=:query`

### Query parameters

| Parameter | Default | Description                                       |
| --------- | ------- | ------------------------------------------------- |
| page      | 1       | Which page to display                             |
| per       | nil     | If set it limits the number of orders per page    |
| q         | nil     | Allows to search orders for a term, for example `q=John` would return all orders where the term `John` shows up |

### Meta

The meta object contains metadata about the complete collection (not affected by pagination)

| Parameter   | Description                                                |
| ----------- | -----------------------------------------------------------|
| total_count | Total amount of orders                                     |
| tag_list    | List of tags and ammount of orders tagged                  |
| status      | Shows the ammount of orders with the corresponding statuses|


## Create a new order

> Example request

```shell
curl --request POST \
--url 'https://example.booqable.com/api/1/orders' \
--header 'content-type: application/json' \
--data '
    {
        "order": {
            "customer_id": 1,
            "starts_at": "01-01-2018 9:00",
            "stops_at": "01-02-2018 9:00"
        }
    }'
```

> This request returns JSON structured like this

```json
{
	"order": {
		"id": "b1bf94ea-8595-4e17-acb3-b9ab425ed0bf",
		"status": "new",
		"starts_at": "2018-01-01T08:00:00.000Z",
		"stops_at": "2018-02-01T08:00:00.000Z",
        ...
	}
}
```

Creates a new order with the provided details

### HTTP Request

`POST /orders`

<aside class="notice">
    Orders default to the status <code>new</code> and need to be changed to <code>concept</code> before become available in the app
</aside>


## Get a single order

> Example request

```shell
curl --request GET \
  --url 'https://example.booqable.com/api/1/orders/364a726b-419f-4156-ac29-71e2f1c6aefa'
```

> This request returns JSON structured like this

```json
{
	"order": {
		"id": "364a726b-419f-4156-ac29-71e2f1c6aefa",
		"number": 1,
		"status": "concept",
        ...
	}
}
```

This endpoint will retrieve a single order by id or number

### HTTP Request

`GET /orders/:id` or
`GET /orders/:number`

## Update order

> Request body example

```json
{
    "order": {
        "stops_at":"2018-01-18T10:15:00.000Z"
    }
}
```

> Example request

```shell
curl --request PATCH \
--url 'https://example.booqable.com/api/1/orders/364a726b-419f-4156-ac29-71e2f1c6aefa' \
--header 'content-type: application/json' \
--data '{
    "order": {
        "stops_at":"2018-01-18T10:27:18.238Z"
    }
}'
```

### HTTP Request

`PUT /orders/:id` or
`PATCH /orders/:id`

<aside class="notice">
	Sending a <code>PUT</code> request will return the resource with any changes that were made, but sending a <code>PATCH</code> request will always return a <code>204 NO CONTENT</code>
</aside>

## Book order's items

> Request body example

```json
{
	"ids": {
		// Book a bulk product by providing a product ID and quantity
		"23b6445d-c846-404b-8628-acb9023d8e5cc": 2,
		// Book a trackable product by providing a producct ID and quantity
		"cdda5942-19d1-4bc8-ac1b-0324a14ba6d5": 1,
		// Book a trackable product by providing a product ID and an array of StockItem IDs
		"cdda5942-19d1-4bc8-ac1b-0324a14ba6d5": [
			"a098b498-6f9f-4552-9a24-ec4614260e2e"
		]
	}
}
```

> Example request

```shell
curl --request POST \
  --url 'https://example.booqable.com/api/1/orders/ea024c26-c322-485b-85ad-f67b890e5346/book'
```

> This request returns JSON structured like this

Reserves given items for the duration of the order.

Bulk items can be booked with just a item group id and quantity, but trackable items offer the choice between just providing an item group id and quantity and then providing the specific item ids when starting the items or providing the item group ids as well as the item ids right away to reserve specific inventory items. You can also mix the two methods for the same item.

### HTTP Request

`POST /orders/:id/book`

## Save an order as a concept

> Example request

```shell
curl --request POST \
  --url 'https://example.booqable.com/api/1/orders/364a726b-419f-4156-ac29-71e2f1c6aefa/concept'
```

> This request returns JSON structured like this

```json
{
	"order": {
		"id": "364a726b-419f-4156-ac29-71e2f1c6aefa",
		"number": 1,
		"status": "concept",
        ...
	}
}
```

A newly created order is by default <code>new</code> and unlisted. To make it viewable for everyone you'll need to save it as a <code>concept</code>.

### HTTP Request

`POST /orders/:id/concept`

## Reserve an order

> Example request

```shell
curl --request POST \
  --url 'https://company.booqable.com/api/1/orders/364a726b-419f-4156-ac29-71e2f1c6aefa/reserve'
```

> This request returns JSON structured like this

```json
{
	"order": {
		"id": "364a726b-419f-4156-ac29-71e2f1c6aefa",
		"number": 1,
		"status": "reserved",
        ...
	}
}
```

> Items not available error example

```json
{
    "error": {
        "status": "items_not_available",
        "data": {
            "2": {
                "available": 99,
                "need": 199
            }
        }
    }
}
```

Reserves an order and books all the products in it. This action is only allowed when the order status is either <code>new</code> or <code>concept</code>

If 1 or more products aren't available in the necessary quantity to fulfill the order a <code>items_not_available</code> error will be raised.

### HTTP Request

`POST /orders/:id/reserve`

## Start order

> Request body example

```json
{
  "ids": {
    // Bulk products just need the product ID and quantity
    // bulk_product_id: quantity
    "23b6445d-c846-404b-8628-acb9023d8e5cc": 2,
    // Trackable products need both the product and individual stock item ids
    // trackable_product_id: [ stock_item_id_1, stock_item_id_2 ]
    "cdda5942-19d1-4bc8-ac1b-0324a14ba6d5": [
      "1953296d-98ea-4f08-b27e-0b7d6d9379df",
      "a098b498-6f9f-4552-9a24-ec4614260e2e"
    ]
  }
}
```

> Example request

```shell
curl --request POST \
  --url 'https://example.booqable.com/api/1/orders/364a726b-419f-4156-ac29-71e2f1c6aefa/start' \
  --header 'content-type: application/json' \
  --data '{
	"ids": {
		"23b6445d-c846-404b-8628-acb9023d8e5cc": 2,
		"cdda5942-19d1-4bc8-ac1b-0324a14ba6d5": [
			"1953296d-98ea-4f08-b27e-0b7d6d9379df",
			"a098b498-6f9f-4552-9a24-ec4614260e2e"
		]
	}
}'
```

> This request returns JSON structured like this

```json
{
	"order": {
		"id": "364a726b-419f-4156-ac29-71e2f1c6aefa",
		"number": 1,
		"status": "started",
		"starts_at": "2018-01-01T08:00:00.000Z",
		"stops_at": "2018-01-18T10:15:00.000Z",
		"customer_id": "297f2584-5f6c-475d-919f-f8791aa6a06a",
		"item_count": 4,
    ...
	}
}
```

To start the oder we need to let the API know which products are being started and in what quantities.
We can do this by sending the `ids` parameter.
The API expects a product group id and the quantity for bulk products, but for trackable products it expects both a product group id as well as the product ids of each item being started.

### HTTP Request

`POST /orders/:id/start`

<aside class="notice">
    You don't have to start all the products in the order at once, you can start some now and then start others later.
</aside>

## Stop order



> Request body example

```json
{
  "ids": {
    // Bulk products just need the product ID and quantity
    // bulk_product_id: quantity
    "23b6445d-c846-404b-8628-acb9023d8e5cc": 2,
    // Trackable products need both the product and individual stock item ids
    // trackable_product_id: [ stock_item_id_1, stock_item_id_2 ]
    "cdda5942-19d1-4bc8-ac1b-0324a14ba6d5": [
      "1953296d-98ea-4f08-b27e-0b7d6d9379df",
      "a098b498-6f9f-4552-9a24-ec4614260e2e"
    ]
  }
}
```

> Example request

```shell
curl --request POST \
  --url 'https://example.booqable.com/api/1/orders/364a726b-419f-4156-ac29-71e2f1c6aefa/stop' \
  --header 'content-type: application/json' \
  --data '{
  "ids": {
    "23b6445d-c846-404b-8628-acb9023d8e5cc": 2,
    "cdda5942-19d1-4bc8-ac1b-0324a14ba6d5": [
      "1953296d-98ea-4f08-b27e-0b7d6d9379df",
      "a098b498-6f9f-4552-9a24-ec4614260e2e"
    ]
  }
}'
```

> This request returns JSON structured like this

```json
{
  "order": {
    "id": "364a726b-419f-4156-ac29-71e2f1c6aefa",
    "number": 1,
    "status": "reserved",
    "starts_at": "2018-01-01T08:00:00.000Z",
    "stops_at": "2018-01-18T10:15:00.000Z",
    "customer_id": "297f2584-5f6c-475d-919f-f8791aa6a06a",
    "item_count": 4,
    ...
  }
}
```

To stop the oder we need to let the API know which products are being stopped and in what quantities.
We can do this by sending the `ids` parameter.
The API expects a product group id and the quantity for bulk products, but for trackable products it expects both a product group id as well as the product ids of each item being stopped.

### HTTP Request

`POST /orders/:id/stop`

## Cancel order

> Example request

```shell
curl --request POST \
  --url https://example.booqable.com/api/1/orders/364a726b-419f-4156-ac29-71e2f1c6aefa/cancel \
```

> This request returns JSON structured like this

```json
{
	"order": {
		"id": "364a726b-419f-4156-ac29-71e2f1c6aefa",
		"number": 1,
		"status": "canceled",
		"starts_at": "2018-01-01T08:00:00.000Z",
		"stops_at": "2018-01-18T10:15:00.000Z",
		"customer_id": "297f2584-5f6c-475d-919f-f8791aa6a06a",
		"item_count": 4,
    ...
	}
}
```

Cancels an order, can only be called on orders with any of these statues: `new`, `concept`, `reserved`.
Canceling a reserved order will free all the products that were reserved with it and cancel all plannings.

### HTTP Request

`POST /orders/:id/cancel`

## Revert order to a given status

> Example request

```shell
curl --request POST \
  --url 'https://example.booqable.com/api/1/orders/ea024c26-c322-485b-85ad-f67b890e5346/revert?status=concept'
```

> This request returns JSON structured like this

```json
{
	"order": {
		"id": "ea024c26-c322-485b-85ad-f67b890e5346",
		"number": 2,
		"status": "concept",
    ...
	}
}
```

What status an order can be reverted to depends on it's current status:

| Current status | Available statuses         |
| ---------------|--------------------------- |
| reserved       | concept                    |
| started        | concept, reserved          |
| stopped        | concept, reserved, started |

### HTTP Request

`POST /orders/:id/revert?status=:status`

### Query parameters

| Parameter | Description         |
| --------- | ------------------- |
| status    | Status to revert to |

## Archive an order

> Example request

```shell
curl --request POST \
  --url 'https://example.booqable.com/api/1/orders/ea024c26-c322-485b-85ad-f67b890e5346/archive'
```

Archives an order

### HTTP Request

`POST /orders/:id/archive`

## Duplicate an order

> Example request

```shell
curl --request POST \
  --url 'https://example.booqable.com/api/1/orders/ea024c26-c322-485b-85ad-f67b890e5346/duplicate'
```

> This request returns JSON structured like this

```json
{
	"order": {
		"id": "2c0006d9-d93a-40ea-b9c8-ed4a9d06d3f3",
		"number": 3,
		"status": "concept",
    ...
	}
}
```

Duplicates an existing order to create a new order

### HTTP Request

`POST /orders/:id/duplicate`

## Check availability

> Example request

```shell
curl --request GET \
  --url 'https://example.booqable.com/api/1/orders/ea024c26-c322-485b-85ad-f67b890e5346/available'
```

> This request returns JSON structured like this

```json
{
  // Bulk product group ID and quanity
	"23b6445d-c846-404b-8628-acb9023d8e5c": {
		"available": 5
	},
  // Trackable product group ID, quantities, and the IDs of the individual products
	"cdda5942-19d1-4bc8-ac1b-0324a14ba6d5": {
		"available": 10,
		"available_stock_ids": [
			"53dde854-cc61-4a11-8357-181c0142c249",
			"a394aaab-3804-4dcb-9178-774502ebe126",
			"85dc0d2e-2dfb-42b2-be18-0217002cb66f",
			"a680bcfd-c56a-4efa-8107-3331109b1895",
			"1c202cfe-8563-4654-bbb9-b6a28fab5458",
			"8dea39ad-5228-4aae-96bb-5e8c8b186c6f",
			"7bad5f7e-1039-4c62-9359-3a1a3f35b7c1",
			"faf41263-e811-4f4a-8d6d-95c4efb68817",
			"1953296d-98ea-4f08-b27e-0b7d6d9379df",
			"a098b498-6f9f-4552-9a24-ec4614260e2e"
		]
	}
}
```

Gets all the available products for the duration of the given order.

### HTTP Request

`GET /orders/:id/available`

## Recalculate prices

> Example request

```shell
curl --request POST \
  --url 'https://company.booqable.com/api/1/orders/ea024c26-c322-485b-85ad-f67b890e5346/recalculate_prices'
```

Recalculates the prices for the given order

### HTTP Request

`POST /orders/:id/recalculate_prices`
