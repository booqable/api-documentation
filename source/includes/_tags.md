# Tags

POST /tags/add?order_id=1&name=delivery

POST /tags/remove?order_id=1&name=delivery

## Add a tag

Adds a tag to an order.

`POST /tags/add?order_id=:order_id&name=:name`

### Query Parameters

| Parameter     | Description                                     |
| ------------- | ----------------------------------------------- |
| **order_id**  | Id of the order you want to add the tag to.     |
| **name**      | Name of the tag you want to add.                |

## Remove a tag

Removes a tag from an order.

`POST /tags/remove?order_id=:order_id&name=:name`

### Query Parameters

| Parameter     | Description                                        |
| ------------- | -------------------------------------------------- |
| **order_id**  | Id of the order you want to remove the tag from.   |
| **name**      | Name of the tag you want to remove.                |
