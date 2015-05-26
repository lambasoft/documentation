---
title: Docs | ProcessOut

language_tabs:
  - shell
  - ruby
  - python

toc_footers:
  - <a href='https://secure.processout.com/signup'>Sign Up on ProcessOut</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

```
,--.   ,--.       ,--.
|  |   |  | ,---. |  | ,---. ,---. ,--,--,--. ,---.
|  |.'.|  || .-. :|  || .--'| .-. ||        || .-. :
|   ,'.   |\   --.|  |\ `--.' '-' '|  |  |  |\   --.
'--'   '--' `----'`--' `---' `---' `--`--`--' `----'
```

Welcome to the ProcessOut documentation. The code provided here will mostly be based
on libraries using our API endpoints, which can be found [here](http://docs.processout.apiary.io).

Language bindings and libraries examples can be found on the right side of this page.
You may switch between them thanks to the menu at the top of this right pane.

## Helper libraries

> Code samples of these libraries will be shown on this pane. Feel free to choose
> which language you wish to see by selecting it in the top bar of this pane.

ProcessOut provides a set of API bindings and libraries created to help
developers easily integrate our service into their applications. These libraries
can be found on the ProcessOut's GitHub page:

- PHP:
    - [processout-php](https://github.com/ProcessOut/ProcessOut-php)
- Python:
    - [processout-python](https://github.com/ProcessOut/ProcessOut-python)
- Javascript:
    - [processout-javascript-modal](https://github.com/ProcessOut/ProcessOut-javascript-modal)

## Making requests

ProcessOut's current API (v1) is entirely *RESTful*. This means that you may perform
`GET`, `POST`, `PUT` and `DELETE` requests and expect the adequate response when available.

Furthermore, `POST`, `PUT` and `DELETE` can contain a json body if they have the
`Content-Type: application/json` header.

## Responses

> Response of a successful request *(200)*

```json
{
  "success": true,
  "message": null
}
```

> Response of a failed request *(4xx)*

```json
{
  "success": false,
  "message": "<Error message>"
}
```

Responses are always **JSON encoded**.

Responses should always contain at least the following keys:

- `success`: A boolean indicating if the request was successful
- `message`: A string giving more information about the error. Null if successful.

**HTTP codes** will also be used, so you should check the response code to get
a quick idea of the request's problem.

- `200`: *OK*. All good.
- `400`: *Bad request*. Your request body is most likely invalid or does not contain
the required values. Check the response message for more information.
- `401`: *Unauthorized*. Your API keys are most likely invalid, or not sent correctly.
- `404`: *Not found*. The item you are trying to fetch does not exist.

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace `meowmeowmeow` with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Isis",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/3"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Isis",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the cat to retrieve

