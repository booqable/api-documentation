# Order Lines

| Field                   | Type     | Description                                                                                  |
| ----------------------- | -------- | -------------------------------------------------------------------------------------------- |
| id                      | Integer  | `Readonly` Unique primary id                                                                 |
| title                   | String   | `Readonly` ID of the associated order                                                        |
| quantity                | Integer  | Amount booked                                                                                |
| price_each_in_cents     | Integer  | Price per quantity in cents                                                                  |
| price_in_cents          | Boolean  | `Readonly` Total price in cents                                                              |
| price_with_tax_in_cents | Integer  | `Readonly` Total price with tax in cents                                                     |
| display_price_in_cents  | Integer  | `Readonly` Display price in cents, depending if prices are set to including or excluding tax |
| position                | String   | Position of the line on the order                                                            |
| planning_id             | Integer  | `Readonly` ID of the associated planning. May be blank if there is no planning associated    |
| order_id                | Integer  | `Readonly` ID of the associated order                                                        |
| tax_category_id         | Integer  | ID of the associated tax category                                                            |
| created_at              | DateTime | `Readonly` When the planning was created                                                     |
| updated_at              | DateTime | `Readonly` When the planning was last updated                                                |

When retrieving a specific line it will also include the associated order and tax category.

## Create a new line

> Request body example

```json
{
  "line": {
    "title": "Nikon FE",
    "quantity": 1,
    "price_each_in_cents": 500
  }
}
```

> Example request

```shell
curl --request POST \
  --url 'https://example.booqable.com/api/1/orders/ea024c26-c322-485b-85ad-f67b890e5346/lines' \
  --header 'content-type: application/json' \
  --data '{
      "line": {
        "title": "Nikon FE",
        "quantity": 1,
        "price_each_in_cents": 500
      }
    }'
```

> This request returns JSON structured like this

```json
{
  "line": {
    "id": "83a3915a-80af-4c4f-ac77-35b1b2498964",
    "title": "Nikon FE",
    "quantity": 1.0,
    "price_each_in_cents": 500,
    "order_id": "ea024c26-c322-485b-85ad-f67b890e5346",
    ...
    "order": {
      "id": "ea024c26-c322-485b-85ad-f67b890e5346",
      "item_ids": [
        "23b6445d-c846-404b-8628-acb9023d8e5c"
      ],
      ...
      "customer": {
        "id": "63a28c67-259c-4a27-a482-2aac3c5d705d",
        "number": 3,
        "name": "Customer Deee",
        "email": "two@world.global",
        ...
        "orders": [
          {
            "id": "ea024c26-c322-485b-85ad-f67b890e5346",
            "number": 2,
            "status": "concept",
            "customer_id": "63a28c67-259c-4a27-a482-2aac3c5d705d",
            ...
          }
        ]
      },
      "plannings": [
        {
          "id": "12e8c770-9025-4243-8b3b-91de340218db",
          ...
          },
          "stock_item_plannings": []
        }
      ],
      "notes": [],
      "tax_values": [],
      "lines": [
        {
          "id": "83a3915a-80af-4c4f-ac77-35b1b2498964",
          "title": "Nikon FE",
          "quantity": 1.0,
          "order_id": "ea024c26-c322-485b-85ad-f67b890e5346",
          ...
        },
        {
          "id": "80879b22-5355-4902-88b2-b6c0f3e5dca5",
          "title": "Arri Alexa",
          "quantity": 1.0,
          "order_id": "ea024c26-c322-485b-85ad-f67b890e5346",
          ...
        }
      ],
      "properties": []
    }
  }
}
```

Creates a new line in an order with the provided details.

### HTTP Request

`POST /orders/:order_id/lines`

## Update a line

> Request body example

```json
{
  "line": {
    "quantity": 2
  }
}
```

> Example request

```shell
curl --request PATCH \
  --url 'https://example.booqable.com/api/1/orders/ea024c26-c322-485b-85ad-f67b890e5346/lines/83a3915a-80af-4c4f-ac77-35b1b2498964' \
  --header 'content-type: application/json' \
  --data '{
      "line": {
        "quantity": 2
      }
    }'
```

### HTTP Request

`PUT /orders/:order_id/lines/:id` or
`PATCH /orders/:order_id/lines/:id`

<aside class="notice">
	Sending a <code>PUT</code> request will return the resource with any changes that were made, but sending a <code>PATCH</code> request will always return a <code>204 NO CONTENT</code>
</aside>

## Update line positions

> Example request

```shell
curl --request POST \
  --url 'https://company.booqable.com/api/1/orders/ea024c26-c322-485b-85ad-f67b890e5346/lines/update_positions?ids[]=24fdbdf2-290e-423d-864b-7214a3ae96b3&ids[]=80879b22-5355-4902-88b2-b6c0f3e5dca5
```

Updates the order of lines in an order.



### HTTP Request

`POST /orders/:order_id/lines/update_positions?ids[]=:id1&ids[]=:id2...`

### Query Parameters

| Parameter | Description                                                                                  |
| --------- | -------------------------------------------------------------------------------------------- |
| **ids[]** | Line id, each line id needs it's own `ids[]` and their order determines the update positions |

Required in **bold**


## Remove a line

> Example request

```shell
curl --request DELETE \
  --url 'https://example.booqable.com/api/1/orders/ea024c26-c322-485b-85ad-f67b890e5346/lines/83a3915a-80af-4c4f-ac77-35b1b2498964'
```
Delete specified line

### HTTP Request

`DELETE /orders/:order_id/lines/:id`
