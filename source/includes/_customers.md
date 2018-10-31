# Customers

> Example of a customer

```json
{
	"customer": {
		"id": "297f2584-5f6c-475d-919f-f8791aa6a06a",
		"updated_at": "2018-01-15T15:27:52.172Z",
		"created_at": "2018-01-15T15:22:27.479Z",
		"legacy_id": null,
		"avatar_url": "https://gravatar.com/avatar/35f5782642e9fa0f6cfff5a552e2ae97.png?d=blank",
		"archived": false,
		"number": 7,
		"name": "Jane Doe",
		"email": "jane@doe.com",
		"phone": "string?",
		"tax_region_id": null,
		"discount_percentage": 0.0,
		"deposit_type": null,
		"deposit_value": 0.0,
		"tags": [
			"buisness"
		],
		"address1": null,
		"address2": null,
		"city": null,
		"region": null,
		"zipcode": null,
		"country": null,
		"order_count": 2,
		"turnover": "0.0",
		"main_address": null,
		"properties": [],
		"notes": [
			{
				"id": "e4adcf3c-d9af-496a-a4b6-d39544ae91b3",
				"body": "Some note",
				"notable_type": "Customer",
				"notable_id": "297f2584-5f6c-475d-919f-f8791aa6a06a",
				"employee_id": "044b6b43-66f8-4fd2-acf2-0250205b2248",
				"employee": {
					"id": "044b6b43-66f8-4fd2-acf2-0250205b2248",
					...
				}
			}
		],
		"orders": [
			{
				"id": "a974fe33-a267-4334-9f2b-21b2e4fed852",
				"number": 4,
				"status": "concept",
				"customer_id": "297f2584-5f6c-475d-919f-f8791aa6a06a",
				...
			}
		]
	}
}
```

The Customer object holds all information about a customer. The customer resource has the following attributes:

| Field         | Type     | Description                                   |
| ------------- | -------- | --------------------------------------------- |
| id            | Integer  | `Readonly` The identifier of the customer     |
| number        | Integer  | `Unique` The customer's number                |
| **name**      | String   | The name of the customer                      |
| email         | String   | E-mail address of the customer                |
| phone         | String   | Customers phone number                        |
| avatar_url    | String   | `Readonly` The avatar url                     |
| tax_region_id | Integer  | The associated tax region.                    |
| orders        | Array    | The customer's orders (?)                     |
| properties    | Array    | The customer's custom properties.             |
| notes         | Array    | The customer's notes.                         |
| archived      | Boolean  | `Readonly` Whether the customer is archived   |
| created_at    | DateTime | `Readonly` When the customer was created      |
| updated_at    | DateTime | `Readonly` When the customer was last updated |

Required in **bold**

## List all customers

```shell
curl --request GET \
  --url 'https://example.booqable.com/api/1/customers?page=1&per=2&api_key=example_key'
```

> This request returns JSON structured like this:

```json
{
	"customers": [
		{
			"id": "b496c71d-2211-4e27-bf80-3058e5294358",
			...
		},
		{
			"id": "49785b51-ca29-4fe8-8218-dacbf1d099ff",
			...
		}
	],
	"meta": {
		"total_count": 2,
		"facets": {
			"tag_list": {
				"_type": "terms",
				"missing": 2,
				"total": 0,
				"other": 0,
				"terms": []
			}
		}
	}
}
```

This endpoint retrieves all customers and can paginated

### HTTP Request

`GET /customers` or
`GET /customers?page=:page&per=:per`

### Query parameters

| Parameter | Default | Description                                       |
| --------- | ------- | ------------------------------------------------- |
| page      | 1       | Which page to display                             |
| per       | nil     | If set it limits the number of customers per page |

### Meta

The `meta` object contains metadata about the complete collection (not affected by pagination)

| Parameter   | Description                       |
| ----------- | --------------------------------- |
| total_count | Total amount of customers         |
| tag_list    | List of tags related to customers |

## Create a new customer

> Format of request body

```json
{
	"customer": {
		"name": "Jack Doe",
		"email": "jack@doe.com",
		"phone": "1598580108",
		"properties_attributes": [
			{
				"type": "Property::Address",
        "name": "Main",
        "address1": "Pieter stuyvesantweg 153",
        "address2": "Unit 504",
        "zipcode": "8937AH",
        "city": "Leeuwarden",
        "country": "Netherlands"
			}
		]
	}
}
```

> Example request

```shell
curl --request POST \
  --url 'https://example.booqable.com/api/1/customers' \
  --header 'content-type: application/json' \
  --data '{
	"customer": {
		"name": "Jane Doe",
		"email": "jane@doe.com",
		"tax_region_id": 1,
		"properties_attributes": [
			{
				"type": "Property::Address",
        "name": "Main",
        "address1": "Pieter stuyvesantweg 153",
        "address2": "Unit 504",
        "zipcode": "8937AH",
        "city": "Leeuwarden",
        "country": "Netherlands"
			}
		]
	}
}'
```

> This request returns JSON structured like this

```json
{
	"customer": {
		"id": "297f2584-5f6c-475d-919f-f8791aa6a06a",
		"name": "Jane Doe",
		"email": "jane@doe.com",
		...
	}
}
```

Creates a new customer with the provided properties

### HTTP Request

`POST /customers`

### Required parameters

**`name`**


## Get a single customer

> Get a customer using their id

```shell
curl --request GET \
  --url 'https://example.booqable.com/api/1/customers/b496c71d-2211-4e27-bf80-3058e5294358'
```

> Get a customer using their number

```shell
curl --request GET \
  --url 'https://example.booqable.com/api/1/customers/1'
```

> This request returns JSON structured like this

```json
{
	"customer": {
		"id": "b496c71d-2211-4e27-bf80-3058e5294358",
		"number": 1,
		"name": "Jane Doe",
		...
	}
}
```

This endpoint will retrieve a single customer by id or number

### HTTP Request

`GET /customers/:id` or
`GET /customers/:number`

## Update customer

> Format of request body

```json
{
	"customer": {
		"phone": "06 11223344"
	}
}
```
> Example request

```shell
curl --request PATCH \
  --url https://example.booqable.com/api/1/customers/297f2584-5f6c-475d-919f-f8791aa6a06a \
  --header 'content-type: application/json' \
  --data '{
	"customer": {
		"phone": "06 11223344"
	}
}'
```

> This request returns JSON structured like this

```json
{
	"customer": {
		"id": "297f2584-5f6c-475d-919f-f8791aa6a06a",
		"name": "Jane Doe",
		"phone": "06 11223344",
		...
	}
}
```

Update the details of a customer

### HTTP Request
`PUT /customers/:id` or
`PATCH /customer/:id`

<aside class="notice">
	Sending a <code>PUT</code> request will return the resource with any changes that were made, but sending a <code>PATCH</code> request will always return a <code>204 NO CONTENT</code>
</aside>

## Archive customer

> Example request

```shell
curl --request DELETE \
  --url 'https://example.booqable.com/api/1/customers/b496c71d-2211-4e27-bf80-3058e5294358/archive'
```

> This request returns JSON structured like this

```json
{
	"customer": {
		"id": "b496c71d-2211-4e27-bf80-3058e5294358",
		"name": "John Doe",
		"archived": true,
    ...
	}
}
```

Archives a customer hiding it from searches, getting this customer by id will still find it, and it can still be updated

### HTTP Request

`DELETE /customers/:id/archive`

## Restore customer

> Example request

```shell
curl --request POST \
  --url 'https://example.booqable.com/api/1/customers/b496c71d-2211-4e27-bf80-3058e5294358/restore'
```

> This request returns JSON structured like this

```json
{
	"customer": {
		"id": "b496c71d-2211-4e27-bf80-3058e5294358",
		"name": "John Doe",
		"archived": false,
    ...
	}
}
```

Restores an archived customer

### HTTP Request

`POST /customers/:id/restore`
