# Product Groups

> Here's an example product group

```json
{
  "product_group": {
    "id": "6107b3cc-03a8-4935-906c-20e2c33db7e0",
    "updated_at": "2018-01-16T14:51:23.917Z",
    "created_at": "2018-01-12T15:58:01.753Z",
    "legacy_id": null,
    "name": "Blackmagic Pocket Cinema Camera",
    "slug": "blackmagic-pocket-cinema-camera-fda66bb8-d3c3-48e8-998a-2ab6b9106713",
    "sku": "BLACKMAGIC_POCKET_CINEMA_CAMERA",
    "lag_time": 1800,
    "lead_time": 360,
    "always_available": false,
    "trackable": true,
    "archived": false,
    "archived_at": null,
    "extra_information": null,
    "search_highlight": null,
    "photo_url": null,
    "description": null,
    "show_in_store": true,
    "base_price_in_cents": 5000,
    "price_wrapper_id": null,
    "price_type": "simple",
    "price_period": "day",
    "tax_category_id": null,
    "flat_fee_price_in_cents": 5000,
    "structure_price_in_cents": 0,
    "deposit_in_cents": 0,
    "products_count": 1,
    "stock_count": 10,
    "has_variations": false,
    "variation_fields": [],
    "stock_item_properties": [],
    "tags": [],
    "base_price_as_decimal": 50.0,
    "flat_fee_price_as_decimal": 50.0,
    "structure_price_as_decimal": 0,
    "deposit_as_decimal": 0,
    "products": [
    ...
    ],
    "properties": [],
    "notes": []
  }
}
```

Product groups define the kind of products that are available but not individual stock items.
A product will always belong to a product group.


| Field               | Type     | Description                                                                                            |
| ------------------- | -------- | ------------------------------------------------------------------------------------------------------ |
| id                  | Integer  | `Readonly` The identifier of the product group                                                         |
| **name**            | String   | Name of the product group                                                                              |
| sku                 | String   | SKU of the product group. Only applies when the product group has no variations                        |
| lag_time            | Integer  | Lag time in seconds                                                                                    |
| lead_time           | Integer  | Lead time in seconds                                                                                   |
| trackable           | Boolean  | Whether the product group has trackable (unique) stock                                                 |
| base_price_in_cents | Integer  | Base price in cents. This is used for price calculation                                                |
| price_id            | Integer  | ID of the associated price structure                                                                   |
| price_type          | String   | Price setting. Options are: blank, 'simple' or 'structure'                                             |
| price_period        | String   | Only applies when `price_type` is set to simple. Options are: 'hour', 'day', 'week', 'month' or 'year' |
| archived            | Boolean  | Whether the product group is archived                                                                  |
| archived_at         | DateTime | When the product group was archived                                                                    |
| quantity            | Integer  | Amount of stock                                                                                        |
| variation_values    | Array    | Only applies when the product is a variation. Example: `['128GB', 'Spacegray']`                        |
| tax_category_id     | Integer  | ID of the associated tax category                                                                      |
| created_at          | DateTime | `Readonly` When the product group was created                                                          |
| updated_at          | DateTime | `Readonly` When the product group was last updated                                                     |

Required in **bold**

## List all product groups

> Example request

```shell
curl --request GET \
  --url 'https://example.booqable.com/api/1/product_groups'
```

> This request returns JSON structured like this

```json
{
  "product_groups": [
    {
      "id": "9c27c177-c6b5-4925-b67b-e69053c88399",
      "name": "Arriflex 16SR3",
      ...

    },
    {
      "id": "6107b3cc-03a8-4935-906c-20e2c33db7e0",
      "name": "Blackmagic Pocket Cinema Camera",
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
      },
      "status": {
        "_type": "terms",
        "missing": 0,
        "total": 5,
        "other": 0,
        "terms": [
          {
            "term": "active",
            "count": 2
          },
          {
            "term": "with_stock",
            "count": 1
          },
          {
            "term": "trackable",
            "count": 1
          },
          {
            "term": "bulk",
            "count": 1
          }
        ]
      }
    }
  }
}
```

This endpoint retrieves all product groups and can paginated

### HTTP Request

`GET /product_groups` or
`GET /product_groups?per=:per&page=:page`

### Query parameters

| Parameter | Default | Description                                            |
| --------- | ------- | ------------------------------------------------------ |
| page      | 1       | Which page to display                                  |
| per       | nil     | If set it limits the number of product groups per page |

### Meta

The meta object contains metadata about the complete collection (not affected by pagination)

| Parameter   | Description                                                                                    |
| ----------- | ---------------------------------------------------------------------------------------------- |
| total_count | Total amount of product groups                                                                 |
| tag_list    | List of tags and ammount of products tagged                                                    |
| status      | Info about what kind of tracking mechanism product groups are using and how many are available |

## Create a new product group

> Request body structure

```json
{
	"product_group": {
		"name": "Arriflex 16SR3",
		"sku": "ARRIFLEX_16_SR3",
		"base_price_in_cents": "130000",
		"price_type": "simple",
		"price_period": "day"
	}
}
```

> Example request

```shell
curl --request POST \
  --url 'https://example.booqable.com/api/1/product_groups' \
  --header 'content-type: application/json' \
  --data '{
	"product_group": {
		"name": "Arriflex 16SR3",
		"sku": "ARRIFLEX_16_SR3",
		"base_price_in_cents": "130000",
		"price_type": "simple",
		"price_period": "day"
	}
}'
```

> This request returns JSON structured like this

```json
{
  "product_group": {
    "id": "aff93024-a928-4da7-917a-799ea5d189ae",
    "name": "Arriflex 16SR3",
    "sku": "ARRIFLEX_16_SR3",
    "trackable": false,
    "base_price_in_cents": 130000,
    "price_type": "simple",
    "price_period": "day",
    "base_price_as_decimal": 1300.0,
    "products_count": 1,
    ...
    "products": [
      {
        "id": "9bd04569-8c85-4b01-b0c5-f7070c319bcc",
        "name": "Arriflex 16SR3",
        ...
      }
    ],
    "properties": [],
    "notes": []
  }
}
```

Creates a new product group with the provided properties

### HTTP Request

`POST /product_groups`

<aside class="notice">
  It's important to note that the <code>trackable</code> property, while not required, will default to <code>false</code> and can't be changed later
</aside>

## Get a single product group

> Example request

```shell
curl --request GET \
  --url 'https://example.booqable.com/api/1/product_groups/6107b3cc-03a8-4935-906c-20e2c33db7e0'
```

> This request returns JSON structured like this

```json
{
  "product_group": {
    "id": "6107b3cc-03a8-4935-906c-20e2c33db7e0",
    "name": "Blackmagic Pocket Cinema Camera",
    ...
    "products": [
      {
        "id": "c560ea83-5231-4052-831e-c26db0121c1b",
        "name": "Blackmagic Pocket Cinema Camera",
        "quantity": 10,
        "product_group_id": "6107b3cc-03a8-4935-906c-20e2c33db7e0",
        ...
        "stock_items": [
          {
            "id": "38b8a49f-9e39-4bf3-8336-2df392b1bee8",
            "identifier": "10",
            "item_id": "c560ea83-5231-4052-831e-c26db0121c1b",
            "status": "available",
            ...
          },
          {
            "id": "2bfbbf9f-4736-45eb-bf57-22b5355c41c8",
            "identifier": "9",
            "item_id": "c560ea83-5231-4052-831e-c26db0121c1b",
            "status": "available",
            ...
          },
          ...
        ]
      }
    ],
    "properties": [],
    "notes": []
  }
}
```

This endpoint will retrieve a single product group by id

### HTTP Request

`GET /product_groups/:id`

## Update product group

> Request body structure

```json
{
	"product_group": {
		"sku": "BM_POCKET_CINEMA_CAMERA"
	}
}
```

> Example request

```shell
curl --request PATCH \
  --url 'https://example.booqable.com/api/1/product_groups/6107b3cc-03a8-4935-906c-20e2c33db7e0' \
  --header 'content-type: application/json' \
  --cookie 'request_method=GET; _rental_api_session=NFBoY2IxclJiQTBjdzZ4aWkxUmFUNzNZYjlXckJPbU9sUUh2OTVlS2c4NElRMW4wRGFMYlE5Mnozam9JMm9GSUhlVU9HYjNudFJJS3NhSzNGUDdaYVQzZk5tWjVwUmdQRXlvaGZXVDRXb2hmYWVIZ0t1eVYyaU54b0w3bXJ5Tm9mK0lseWhSOTZ0L28yU1pkOUYrbVdWUW5nbDNHQlU3K0d1RHdPdVJqbGdRZERwWVhsTGYyNlpsSHlxclBVck5zeVp1NXJ0N0g5eHNtaFljeDh1ekp4MWxYd3QxZTlKM2xXMFUxRkx5N1NRTkVVQjB0RnduaGFzOTNlSmJQYkYzcVdxMmRWWFVpbCsrSldxcEY4ZWJPaWM0VjRpQnZVMisyQTlEWVhjc3kxQ0Q5N1R5SFF6eSs1R2lDdjBzVDduNVJ4ejJ1eWJ5STFFdzVNWTBrQTJvSW02c3ZralRockQ0bWRUZ3RQdXBHMVdJPS0tNVhVTXY1RGthZEYxSXBBOEtmN0tiZz09--620dd5ead23e2e80caa59daed438a2e1f502797c' \
  --data '{
	"product_group": {
		"sku": "BM_POCKET_CINEMA_CAMERA"
	}
}'
```

Update the properties of a product group

### HTTP Request

`PUT /product_groups/:id` or
`PATH /product_groups/:id`

<aside class="notice">
	Sending a <code>PUT</code> request will return the resource with any changes that were made, but sending a <code>PATCH</code> request will always return a <code>204 NO CONTENT</code>
</aside>

## Archive product group

> Example request

```shell
curl --request DELETE \
  --url 'https://example.booqable.com/api/1/product_groups/6107b3cc-03a8-4935-906c-20e2c33db7e0/archive'
```

Archives a product group

### HTTP Request

`DELETE /product_groups/:id/archive`

## Restore product group

> Example request

```shell
curl --request POST \
  --url 'https://company.booqable.com/api/1/product_groups/6107b3cc-03a8-4935-906c-20e2c33db7e0/restore'
```

### HTTP Request

`POST /product_groups/:id/restore`

## Check availability

> Example request

```shell
curl --request GET \
  --url 'https://company.booqable.com/api/1/products/23b6445d-c846-404b-8628-acb9023d8e5c/availability?interval=month&till=01-02-2018&from=01-01-2018
```

> This request returns JSON structured like this

```json
{
	"2017-12-01 00:00:00 +0100": {
		"reserved": 0,
		"concept": 0,
		"date": "2017-12-01T00:00:00.000+01:00",
		"available": 5,
		"total": 5,
		"interval": "month"
	},
	"2018-01-01 00:00:00 +0100": {
		"reserved": 2,
		"concept": 0,
		"date": "2018-01-01T00:00:00.000+01:00",
		"available": 3,
		"total": 5,
		"interval": "month"
	},
	"2018-02-01 00:00:00 +0100": {
		"reserved": 0,
		"concept": 2,
		"date": "2018-02-01T00:00:00.000+01:00",
		"available": 5,
		"total": 5,
		"interval": "month"
	},
	"2018-03-01 00:00:00 +0100": {
		"reserved": 0,
		"concept": 0,
		"date": "2018-03-01T00:00:00.000+01:00",
		"available": 5,
		"total": 5,
		"interval": "month"
	}
}
```

Provides an availability overview of the specified product in the provided timeframe

### HTTP Request

`GET /products/:product_id/availablility/?from=:from&till=:till` or
`GET /products/:product_id/availablility/?from=:from&till=:till&interval=:interval`

### Query parameters

| Parameter  | Description                                  | Available options                        |
| ---------- | -------------------------------------------- | ---------------------------------------- |
| **from**   | Start date                                   |                                          |
| **till**   | End date                                     |                                          |
| interval   | Specifies intervals to split up timeframe in | `minute`, `hour`, `day`, `week`, `month` |

Required in **bold**

<aside class="notice">An empty response will be sent if the request is not valid</aside>

## Show product pricing structures

> Example request

```shell
curl --request GET \
  --url 'https://example.booqable.com/api/1/products/c560ea83-5231-4052-831e-c26db0121c1b/prices'
```

> This request returns JSON structured like this

```json
{
  "price_structures": [
    {
      "id": null,
      "updated_at": null,
      "created_at": null,
      "legacy_id": null,
      "tiles": [
        {
          "id": null,
          "updated_at": null,
          "created_at": null,
          "name": null,
          "length": 86400,
          "multiplier": "1.0",
          "quantity": "1.0",
          "period": "day",
          "price_in_cents": 5000,
          "price_id": null
        },
        {
          "id": null,
          "updated_at": null,
          "created_at": null,
          "name": null,
          "length": 172800,
          "multiplier": "2.0",
          "quantity": "2.0",
          "period": "day",
          "price_in_cents": 10000,
          "price_id": null
        },
        ...
      ]
    }
  ]
}
```
Allows you to get the pricing structure of the product

### HTTP Request

`GET /products/:product_id/prices`

<aside class="notice">
  The <code>product_id</code> is not the same as <code>product_group_id</code>
</aside>
