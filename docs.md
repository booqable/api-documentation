FORMAT: 1A
HOST: https://company.booqable.com/api/v1

# Booqable

The Booqable API is organized around REST. Our API is designed to have predictable, resource-oriented URLs and to use HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which can be understood by off-the-shelf HTTP clients, and we support cross-origin resource sharing to allow you to interact securely with our API from a client-side web application (though you should remember that you should never expose your secret API key in any public website's client-side code). JSON will be returned in all responses from the API, including errors (though if you're using API bindings, we will convert the response to the appropriate language-specific object).

To make the Booqable API as explorable as possible, accounts have test-mode API keys as well as live-mode API keys. These keys can be active at the same time. The requests in the sidebar actually work.

## Authentication

You authenticate to the Booqable API by providing one of your API keys in the request. You can manage your API keys from your account. You can have multiple API keys active at one time. Your API keys carry many privileges, so be sure to keep them secret!
All API requests must be made over HTTPS. Calls made over plain HTTP will fail. You must authenticate for all requests.

## Errors

Booqable uses conventional HTTP response codes to indicate success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that resulted from the provided information (e.g. a required parameter was missing, a charge failed, etc.), and codes in the 5xx range indicate an error with Booqable's servers.

## Handling errors

Our API bindings can raise exceptions for many reasons, such as invalid parameters, authentication errors, and network unavailability. We recommend always trying to gracefully handle exceptions from our API.

# Group Session
The Session object holds all information about the current session. A session object with all it's details.

| Field              | Type     | Description                   |
|--------------------|----------|-------------------------------|
| `token`            | String   | Current session identifier    |
| `currency`         | Object   | Currency data                 |
| `settings`         | Object   | See [Settings](#reference/settings) |
| `plan`             | Object   | The companies current plan    |
| `company`          | Object   | See [Company](#reference/company) |
| `employee`         | Object   | Currently signed in employee. See [Employee](#reference/employee) |

## Session [/session]

### Retrieve the Session [GET]
+ Response 200 (application/json)

    + Body

            {
              token: "1418154074",
              currency: {
                name: "EUR",
                decimal: ",",
                thousand: ".",
                symbol: "€"
              },
              settings: {
                dashboard.orders.period: "all",
                wizard.customers: "true",
                wizard.orders: "true",
                wizard.products: "true",
                wizard.settings: "true"
              },
              plan: {
                name: "1 employee",
                amount: "$25.00",
                next_payment_due: "2014-12-20"
              },
              company: {
                id: 1,
                updated_at: "2014-12-08T14:06:42.965Z",
                created_at: "2014-11-19T21:27:59.777Z",
                name: "Demo Company",
                slug: "Demo Company",
                email: "john@demo.com",
                phone: "+3102011111111",
                address_line_1: "Demo Street 1",
                address_line_2: "Unit 1",
                zipcode: "9000AA",
                city: "Amsterdam",
                country: "Netherlands",
                logo_url: "/uploads/50e3370a06ffd6288fb729ecde5c25f8/company/logo/1/0062a741-bb09-4d43-b4b4-1e226252a589.jpeg",
                timezone: "Europe/London",
                timezone_offset: "+00:00",
                currency: "eur",
                financial_line_1: "",
                financial_line_2: "",
                card_last_digits: "4242",
                card_holder: "John",
                card_expiry_date: "2/2016",
                card_type: "Visa",
                vat_number: "",
                in_europe: true,
                trial_ends_at: "2014-11-17T10:39:55.277Z",
                activated: true
              },
              employee: {
                id: 1,
                updated_at: "2014-12-09T19:41:14.059+00:00",
                created_at: "2014-11-19T21:28:02.040+00:00",
                name: "Johan van Zonneveld",
                email: "johan@demo.com",
                avatar_url: "https://gravatar.com/avatar/8d1da8e3b4f75d2574c0025d4f497eb1.png?d=blank"
              }
            }


# Group Company
The Company object holds all information about a company. The Company resource has the following attributes:

| Field              | Type     | Description                   |
|--------------------|----------|-------------------------------|
| `id`               | Integer  |`Readonly` The identifier of the company |
| `name`             | String   | The name of the company       |
| `slug`             | String   | `Readonly` The slug of the company       |
| `email`            | String   | E-mail address of the company; all communication to customers will be sent from this mail address |
| `phone`            | String   | The phone number of the company |
| `address_line_1`   | String   | First address line            |
| `address_line_2`   | String   | Second address line           |
| `zipcode`          | String   | Zipcode                       |
| `city`             | String   | City                          |
| `country`          | String   | Country                       |
| `logo_url`         | String   | `Readonly` Logo url                      |
| `timezone`         | String   | The timezone                  |
| `timezone_offset`  | String   | `Readonly` The timezone offset |
| `currency`         | String   | The currency |
| `financial_line_1` | String   | Financial line 1 |
| `financial_line_2` | String   | Financial line 2 |
| `card_last_digits` | String   | `Readonly` Credict card last digits |
| `card_holder`      | String   | `Readonly` Credit card holder |
| `card_expiry_date` | String   | `Readonly` Credit card expiry date |
| `card_type`        | String   | `Readonly` Credit card type |
| `vat_number`       | String   | Vat number; We'll add VAT to invoices for europe customers without a VAT number |
| `in_europe`        | Boolean  | `Readonly` Whether company is situated in te EU |
| `trial_ends_at`    | DateTime | `Readonly` When the trial ends |
| `activated`        | Boolean  | `Readonly` Whether company added credit card details |
| `created_at`       | DateTime | `Readonly` When the company was created |
| `updated_at`       | DateTime | `Readonly` When the company was last updated |

## Company [/companies/{id}]

+ Parameters

    + id (required, number, `1`) ... Numeric `id` of the Company to perform action with. Has example value.

### Update a Company [PUT]

  + Request (application/json)

          {
            company: {
              name: "Demo Company",
              slug: "Demo Company",
              email: "john@demo.com",
              phone: "+3102011111111",
              address_line_1: "Demo Street 1",
              address_line_2: "Unit 1",
              zipcode: "9000AA",
              city: "Amsterdam",
              country: "Netherlands",
              timezone: "Europe/London",
              currency: "eur",
              financial_line_1: "",
              financial_line_2: "",
              vat_number: ""
            }
          }

  + Response 200 (application/json)

      + Body

              {
                company: {
                  id: 1,
                  updated_at: "2014-12-08T14:06:42.965Z",
                  created_at: "2014-11-19T21:27:59.777Z",
                  name: "Demo Company",
                  slug: "Demo Company",
                  email: "john@demo.com",
                  phone: "+3102011111111",
                  address_line_1: "Demo Street 1",
                  address_line_2: "Unit 1",
                  zipcode: "9000AA",
                  city: "Amsterdam",
                  country: "Netherlands",
                  logo_url: "/uploads/50e3370a06ffd6288fb729ecde5c25f8/company/logo/1/0062a741-bb09-4d43-b4b4-1e226252a589.jpeg",
                  timezone: "Europe/London",
                  timezone_offset: "+00:00",
                  currency: "eur",
                  financial_line_1: "",
                  financial_line_2: "",
                  card_last_digits: "4242",
                  card_holder: "John",
                  card_expiry_date: "2/2016",
                  card_type: "Visa",
                  vat_number: "",
                  in_europe: true,
                  trial_ends_at: "2014-11-17T10:39:55.277Z",
                  activated: true
                }
              }

# Group Settings
Settings are always listed or updated in a batch. You can also save your own settings. List of valid settings:

| Setting                    | Default  | Valid options | Description                   |
|----------------------------|----------|---------------|-------------------------------|
| `documents.footnote`       | ""       | String        | Footnote displayed on every document |
| `documents.contract_terms` | ""       | String        | Terms displayed on every contract |
| `pricing.tax_strategy`     | "exclusive" | "exclusive", "inclusive" | Whether taxes are added to or substracted from prices |

## Settings [/settings]

### List settings [GET]

+ Response 200 (application/json)

    + Body

            settings: {
              pricing.tax_strategy: "exclusive"
            }

### Update settings [POST]

+ Request (application/json)

        settings: {
          pricing.tax_strategy: "inclusive"
        }

+ Response 200 (application/json)

    + Body

            settings: {
              pricing.tax_strategy: "inclusive"
            }

# Group Employees
The Employee object holds all information about an employee. The Employee resource has the following attributes:

| Field              | Type     | Description                   |
|--------------------|----------|-------------------------------|
| `id`               | Integer  |`Readonly` The identifier of the employee |
| `name` *           | String   | The name of the employee       |
| `email` *          | String   | E-mail address of the employee |
| `active`           | Boolean  | `Readonly` Whether employee is active |
| `owner`            | Boolean  | `Readonly` Whether employee is account owner |
| `avatar_url`       | String   | `Readonly` The avatar url |
| `created_at`       | DateTime | `Readonly` When the company was created |
| `updated_at`       | DateTime | `Readonly` When the company was last updated |

\* required

## Employees [/employees]

### Create an employee [POST]
The employee will receive an e-mail after creation with password setup instructions.

+ Request (application/json)

        {
          employee: {
            name: "Arjen Oosterkamp",
            email: "mail@arjen.me"
          }
        }

+ Response 200

    [Employee][]

### List employees [GET]

+ Response 200 (application/json)

    + Body

            {
              employees: [
                {
                  id: 2,
                  updated_at: "2015-01-07T09:26:48.389+01:00",
                  created_at: "2014-11-01T10:39:25.980+01:00",
                  name: "Arjen Oosterkamp",
                  email: "mail@arjen.me",
                  avatar_url: "https://gravatar.com/avatar/a6debab4b3faa4fa3a21effe925982f9.png?d=blank",
                  active: true,
                  owner: false
                },
                {
                  id: 1,
                  updated_at: "2015-01-07T09:26:48.389+01:00",
                  created_at: "2014-11-01T10:34:41.366+01:00",
                  name: "Johan van Zonneveld",
                  email: "johan@42rockers.com",
                  avatar_url: "https://gravatar.com/avatar/8d1da8e3b4f75d2574c0025d4f497eb1.png?d=blank",
                  active: true,
                  owner: true
                }
              ],
              meta: {
                total_count: 2
              }
            }

## Employee [/employees/{id}]

+ Model (application/hal+json)

    + Parameters

      + id (required, number, `1`) ... Numeric `id` of the Employee to perform action with. Has example value.

    + Body

            {
              employee: {
                id: 2,
                updated_at: "2015-01-07T09:26:48.389+01:00",
                created_at: "2014-11-01T10:39:25.980+01:00",
                name: "Arjen Oosterkamp",
                email: "mail@arjen.me",
                avatar_url: "https://gravatar.com/avatar/a6debab4b3faa4fa3a21effe925982f9.png?d=blank",
                active: true,
                owner: false
              }
            }

### Retreive employee [GET]

+ Response 200

    [Employee][]

### Update an employee [PUT]

+ Request (application/json)

        {
          employee: {
            name: "Arjen Oosterkamp",
            email: "mail@arjen.me"
          }
        }

+ Response 200

    [Employee][]

## Deactivate an Employee [/employees/{id}/deactivate]

### Deactivate an employee [POST]

+ Response 200

    [Employee][]

## Reactivate an Employee [/employees/{id}/reactivate]

### Reactivate an employee [POST]

+ Response 200

    [Employee][]

# Group Customers

The Customer object holds all information about a customer. The customer resource has the following attributes:

| Field              | Type     | Description                   |
|--------------------|----------|-------------------------------|
| `id`               | Integer  |`Readonly` The identifier of the employee |
| `number`           | Integer  | `Unique` The customer's number |
| `name` *           | String   | The name of the employee       |
| `email`            | String   | E-mail address of the employee |
| `phone`            | String   | Employees phone number |
| `avatar_url`       | String   | `Readonly` The avatar url |
| `tax_region_id`    | Integer  | The associated tax region. See [TaxRegion](#reference/tax_region) |
| `properties`       | Array    | See [Property](#reference/property) |
| `archived`         | Boolean  | `Readonly` Whether the customer is archived |
| `created_at`       | DateTime | `Readonly` When the company was created |
| `updated_at`       | DateTime | `Readonly` When the company was last updated |

\* required

## Customers [/customers]

### Create a customer [POST]

+ Request (application/json)

        {
          customer: {
            name: "Arjen Oosterkamp",
            email: "mail@arjen.me",
            tax_region_id: 1,
            properties: [
              {
                type: "Property::Address"
                name: "Main"
                address1: "Pieter stuyvesantweg 153"
                address2: "Unit 504"
                zipcode: 8937AH
                city: "Leeuwarden"
                country: "Netherlands"
              }
            ]
          }
        }

+ Response 200

    [Customer][]

### List customers [GET]

+ Response 200 (application/json)

    + Body

            {
              customers: [
                {
                  id: 3,
                  updated_at: "2014-12-22T10:28:41.110+00:00",
                  created_at: "2014-12-22T10:28:41.110+00:00",
                  avatar_url: "https://gravatar.com/avatar/cadc7e3a922ee445a81ab70138c3928e.png?d=blank",
                  archived: false,
                  number: 3,
                  name: "Johanson",
                  email: "johan@vzonneveld.nl",
                  phone: null,
                  tax_region_id: null
                },
                {
                  id: 2,
                  updated_at: "2014-12-08T18:12:28.980+00:00",
                  created_at: "2014-12-08T18:12:28.980+00:00",
                  avatar_url: "https://gravatar.com/avatar/a6debab4b3faa4fa3a21effe925982f9.png?d=blank",
                  archived: false,
                  number: 2,
                  name: "Arjen Oosterkamp",
                  email: "mail@arjen.me",
                  phone: null,
                  tax_region_id: null
                },
                {
                  id: 1,
                  updated_at: "2014-12-05T14:59:48.534+00:00",
                  created_at: "2014-11-24T13:07:42.032+00:00",
                  avatar_url: "https://gravatar.com/avatar/d41d8cd98f00b204e9800998ecf8427e.png?d=blank",
                  archived: false,
                  number: 1,
                  name: "John Doe",
                  email: null,
                  phone: null,
                  tax_region_id: 2
                }
              ],
              meta: {
                total_count: 3
              }
            }

## Customer [/customers/{id}]

+ Model (application/hal+json)

    + Parameters

      + id (required, number, `1`) ... Numeric `id` of the Customer to perform action with. Has example value.

    + Body

            {
              customer: {
                  id: 1,
                  updated_at: "2014-12-05T14:59:48.534+00:00",
                  created_at: "2014-11-24T13:07:42.032+00:00",
                  avatar_url: "https://gravatar.com/avatar/d41d8cd98f00b204e9800998ecf8427e.png?d=blank",
                  archived: false,
                  number: 1,
                  name: "John Doe",
                  email: john@doe.com,
                  phone: null,
                  tax_region_id: 2
                }
            }

### Retreive a customer [GET]

+ Response 200

    [Customer][]

### Update a customer [PUT]

+ Request (application/json)

        {
          customer: {
            name: "Arjen Oosterkamp",
            email: "arjen@arjen.me"
          }
        }

+ Response 200

    [Customer][]

## Archive a Customer [/customers/{id}/archive]

### Archive a customer [DELETE]

+ Response 200

    [Customer][]

## Restore a Customer [/customers/{id}/restore]

### Restores a customer [POST]

+ Response 200

    [Customer][]

# Group Documents

# Group Charges
The Charge object holds all information about a charge. The Charge resource has the following attributes:

| Field               | Type     | Description                   |
|---------------------|----------|-------------------------------|
| `id`                | Integer  |`Readonly` The identifier of the employee |
| `amount_in_cents` * | Integer  | The amount in cents (can also be negative) |
| `status`*           | String   | Can be one of `success`, `pending`, `failure` |
| `document_id` *     | Integer  | The id of the assocaciated document |
| `invoice`           | Object   | `Readonly` The associated invoice. See [Invoice](#reference/invoice) |
| `created_at`        | DateTime | `Readonly` When the company was created |
| `updated_at`        | DateTime | `Readonly` When the company was last updated |

\* required

## Charges [/charges]

### Create a charge [POST]

+ Request (application/json)

          {
            charge: {
              charge_type: "Creditcard",
              amount_in_cents: 9075,
              document_id: 1
              status: "success"
            }
          }

+ Response 200 (application/json)

  + Body

            {
              charge: {
                id: 2,
                updated_at: "2015-01-07T09:26:48.389+01:00",
                created_at: "2014-11-01T10:39:25.980+01:00",
                charge_type: "Creditcard",
                amount_in_cents: 9075,
                document_id: 1
                status: "success",
                invoice: {
                  address: null
                  archived: false
                  date: "2014-12-08"
                  finalized: true
                  id: 54
                  name: "John Doe"
                  number: 9
                  order_id: 3
                  paid_in_cents: 9075
                  price_in_cents: 7500
                  price_with_tax_in_cents: 9075
                  reference: null
                  sent: false
                  status: "Paid"
                  to_be_paid_in_cents: 0
                  type: "Document::Invoice"
                }
              }
            }

### List charges [GET]

+ Response 200 (application/json)

  + Body

              {
                charges: [
                    {
                      id: 27,
                      created_at: "2014-12-09T09:47:24.045+00:00",
                      amount_in_cents: 15125,
                      charge_type: "card",
                      status: "success",
                      document_id: 59
                    }
                ],
                meta: {
                  total_count: 1
                }
              }

# Group Orders

# Group Product Groups

# Group Products

# Group Stock Items

# Group Price Structures

# Group Tax Categories

# Group Tax Regions

# Group Emails

# Group Email Templates

# Group Notes
Notes related resources of the **Notes API**

## Notes Collection [/notes{?customer_id,order_id,item_id,document_id,page,per}]

+ Parameters
    + customer_id (optional, number, `1`) ... Numeric `customer_id` list or create notes for specific customer.
    + order_id (optional, number, `1`) ... Numeric `order_id` list or create notes for specific order.
    + item_id (optional, number, `1`) ... Numeric `item_id` list or create notes for specific item (Product Group, Product).
    + document_id (optional, number, `1`) ... Numeric `document_id` list or create notes for specific document.
    + page (optional, number, `1`) ... Numeric `page` the page. Defaults to `1`.
    + per (optional, number, `1`) ... Numeric `per` results per page. Defaults to `15`.

### Listing Notes [GET]

+ Response 200 (application/json)

        [{
          "id": 1, "title": "Jogging in park"
        }, {
          "id": 2, "title": "Pick-up posters from post-office"
        }]

### Create a Note [POST]
+ Request (application/json)

        { "title": "Buy cheese and bread for breakfast." }

+ Response 201 (application/json)

        { "id": 3, "title": "Buy cheese and bread for breakfast." }

## Note [/notes/{id}]
A single Note object with all its details

+ Parameters
    + id (required, number, `1`) ... Numeric `id` of the Note to perform action with. Has example value.

### Retrieve a Note [GET]
+ Response 200 (application/json)

    + Header

            X-My-Header: The Value

    + Body

            { "id": 2, "title": "Pick-up posters from post-office" }

### Remove a Note [DELETE]
+ Response 204