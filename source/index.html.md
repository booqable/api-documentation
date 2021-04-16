---
title: Booqable API

language_tabs: # must be one of https://git.io/vQNgJ
#  - shell

# toc_footers:
#   - <a href='https://github.com/booqable/api-documentation'>Documentation on GitHub</a>

includes:
  - customers
  - products
  - orders
  - planning
  - lines

search: false
---

# Introduction

The Booqable API is a RESTful API and as such is designed to have predictable, resource-oriented URLs and to use HTTP response codes to indicate API errors. We use standard HTTP features, like HTTP authentication and HTTP verbs, which can be understood by off-the-shelf HTTP clients, and we support cross-origin resource sharing to allow you to interact securely with our API from a client-side web application.

<aside class="warning">
  <b>WARNING:</b> Booqable's API is still in Beta we might introduce non-backwards compatible changes in the future!
</aside>

## Creating an API key
To interact with our API, first, you have to have a means of authentification, here's how to create a shiny new API key.

1. Go to your account settings page
`{company-name-here}.booqable.com/account/edit`
2. Name your new key
3. Click "Create new key"

<aside class="success">
  You now have a <b>Booqable API key!</b>
</aside>

You can manage your API keys from your account.
You can have multiple API keys active at one time.

<aside class="warning">
  Your API keys carry many privileges, so be sure to keep them secret! <br>
  <b>Don't expose your API key in any public websites client-side code.</b>
</aside>

## Contributing

The API is going to be a very important part of our eco system. We've designed the docs in a way every developer is able to contribute to our API. If you find a bug or you have a great suggestion open an issue or pull request on Github. Check [our github repository](https://github.com/booqable/api-documentation) for a readme on how to participate. We love to see your additions!

# Endpoint

All API requests need to be directed to the correct company-specific endpoint.
The format is as follows:

`https://{company_slug}.booqable.com/api/1/`

<aside class="notice">
  You must replace <code>{company_slug}</code> with the name of your company.
</aside>

# Authentication

> Example of an authorized request

```shell
curl --request GET \
  --url 'https://company.booqable.com/api/1/customers?api_key=API_KEY_HERE'
```

You authenticate to the Booqable API by providing on of your API keys in the request.
This can be done by appending `?api_key=API_KEY_HERE` to the end of your request URL.

<aside class="notice">
  A request sent with a correct API key will recieve a session cookie in the response. You can use this cookie for further requests.
</aside>

<aside class="notice">
  Unless otherwise specified all further examples will omit authentication for the sake of brevity
</aside>
