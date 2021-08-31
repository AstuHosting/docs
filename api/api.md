---
description: 'Some API things :)'
---

# API

{% api-method method="get" host="https://your.domain.com" path="/api/userinfo" %}
{% api-method-summary %}
Get userinfo
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get information on a user!
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Your Authentication token, type: Bearer
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
The Discord ID of the user
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Userinfo successfully retrieved.
{% endapi-method-response-example-description %}

```
{
  "status": "success",
  "package": {
    "ram": 0,
    "disk": 0,
    "cpu": 0,
    "servers": 0
  },
  "extra": {
    "ram": 0,
    "disk": 0,
    "cpu": 0,
    "servers": 0
  },
  "userinfo": ...,
  "coins": 0
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
No ID specified
{% endapi-method-response-example-description %}

```
{ "status": "missing id" }
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
A user with the ID given doesn't exist.
{% endapi-method-response-example-description %}

```
{ "status": "invalid id" }
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

