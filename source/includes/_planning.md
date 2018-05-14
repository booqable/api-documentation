# Planning

| Field               | Type     | Description                                   |
| ------------------- | -------- | --------------------------------------------- |
| id                  | Integer  | `Readonly` Unique primary id                  |
| order_id            | Integer  | `Readonly` ID of the associated order         |
| item_id             | Integer  | ID of the associated product                  |
| quantity            | Integer  | Amount booked                                 |
| price_each_in_cents | Integer  | Price per quantity in cents                   |
| reserved            | Boolean  | Whether the planning is reserved              |
| started             | Integer  | Number of stock started                       |
| stopped             | Integer  | Number of stock stopped                       |
| charge_label        | String   | Label of the price charge                     |
| charge_length       | Integer  | Length of the price charge in seconds         |
| created_at          | DateTime | `Readonly` When the planning was created      |
| updated_at          | DateTime | `Readonly` When the planning was last updated |

## Delete a planning

> Example request

```shell
curl --request DELETE \
  --url 'https://example.booqable.com/api/1/orders/ea024c26-c322-485b-85ad-f67b890e5346/plannings/b649dcc8-2c93-45bd-88f3-35e1a8be8356'
```

Deletes a planning from an order.

### HTTP Request

`DELETE /orders/:order_id/plannings/:id`
