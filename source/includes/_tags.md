# Tags

POST /tags/add?order_id=1&name=delivery

POST /tags/remove?order_id=1&name=delivery

## Add a tag

Adds a tag to a resource.
A resource could be an order, customer, product group, bundle or document.

### Resource parameters

Supply one of the following parameters to add a tag to a resource.

| Parameter              | Description                                           |
|------------------------|-------------------------------------------------------|
| **order_id**           | Id of the order you want to add the tag to.           |
| **customer_id**        | Id of the customer you want to add the tag to.        |
| **product_group_id**   | Id of the product group you want to add the tag to.   |
| **bundle_id**          | Id of the bundle you want to add the tag to.          |
| **document_id**        | Id of the document you want to add the tag to.        |

`POST /tags/add?order_id=:order_id&name=:name`

### Query Parameters

| Parameter              | Description                                                           |
|------------------------|-----------------------------------------------------------------------|
| **order_id**           | Id of the order you want to add the tag to (or any other resource id) |
| **name**               | Name of the tag you want to add.                                      |

## Remove a tag

Removes a tag from an order.

`POST /tags/remove?order_id=:order_id&name=:name`

### Query Parameters

| Parameter            | Description                                                           |
|----------------------|-----------------------------------------------------------------------|
| **order_id**         | Id of the order you want to add the tag to (or any other resource id) |
| **name**             | Name of the tag you want to remove.                                   |
