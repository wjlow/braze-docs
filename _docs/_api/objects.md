---
nav_title: Objects & Filters
layout: api_objects_page
excerpt_separator: ""
page_order: 2
---
{% api %}
## User Alias Object
{% apitags %}
Object, Messaging
{% endapitags %}

The User Alias Object sets or pulls specific information regarding the naming/aliasing and categorization of the user.

#### Object Body
```json
{
  "alias_name" : "sample-alias-name",
  "alias_label" : "sample-alias-label"
}
```

#### Parameter Details

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `alias_name`  | Yes | String | The user identifier. Your user's alias in Braze. |
| `alias_label`  | Yes | String | Indicates the type of alias. The labels associated with your user's alias in Braze. Users can have multiple aliases with _different_ labels, but only one `alias_name` per `alias_label`. Each `name`:`label` pair is unique across app group. |

{% endapi %}

{% api %}
## Recipient Object
{% apitags %}
Object, Messaging
{% endapitags %}

The Recipient Object defines your audience upon entry to a Canvas or receipt of a Campaign via API. Either `external_user_id` or `user_alias` is required. Requests must specify only one.

#### Object Body (Using User Alias)
```json
{
  "user_alias": {
    "alias_name" : "sample-alias-name",
    "alias_label" : "sample-alias-label"
  },
  "trigger_properties": {
    "key1": "value1",
    "key2": "value2"
  },
  "canvas_entry_properties": {
    "key11": "value11",
    "key22": "value22"
    }
}
```

#### Object Body (Using External User ID)
```json
{
  "external_user_id": ["external-id-1", "external-id-2"],
  "trigger_properties": {
    "key1": "value1",
    "key2": "value2"
  },
  "canvas_entry_properties": {
    "key11": "value11",
    "key22": "value22"
    }
}
```

#### Parameter Details

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `user_alias`  | Yes (unless you use `external_user_id`) | Object, String | The User Alias Object. Alias of the user who will receive the message.|
| `external_user_id`  | Yes (unless you use `user_alias`) | Array of Strings | The user's External User ID. External ID of the user who will receive the message. |
| `trigger_properties` | No | Object, String | The Trigger Properties Object. The personalization key-value pairs for this user when triggering a campaign. |
| `canvas_entry_properties` | No | Object, String | The Canvas Entry Properties Object. The personalization key-value pairs for this user when triggering a Canvas. |

{% endapi %}

{% api %}
## Trigger Properties Object
{% apitags %}
Object, API, Messaging
{% endapitags %}

The Trigger Properties Object is a custom object that will assist you in personalizing key-value pairs for a campaign with API Triggered Delivery. If you make an API request that contains the `trigger_properties` object, its values can then be referenced in your message body using the `api_trigger_properties` namespace in liquid.

#### Object Body

This example (when used in an appropriate endpoint) would add the word "shoes" to your message when you use the liquid snippet `{{api_trigger_properties.${product_name}}}` in the message body.

```json
{
  "trigger_properties": {
    "product_name": "shoes",
    "product_price": "79.99"
    }
  }
```

{% endapi %}

{% api %}
## Canvas Entry Properties Object
{% apitags %}
Object, API, Messaging
{% endapitags %}

The Canvas Entry Properties Object is a custom object that will assist you in personalizing key-value pairs for a Canvas Entry Step via API. If you make an API request that contains the `canvas_entry_properties` object, its values can then be referenced in your message body using the `canvas_entry_properties` namespace in liquid.

#### Object Body

This example (when used in an appropriate endpoint) would add the word "shoes" to your message when you use the liquid snippet `{{canvas_entry_properties.${product_name}}}` in the message body.

```json
{
  "canvas_entry_properties": {
    "product_name": "shoes",
    "product_price": "79.99"
    }
  }
```

{% endapi %}


{% api %}
## Schedule Object
{% apitags %}
Object, Messaging
{% endapitags %}

The parameters for the Campaign and Canvas schedule creation endpoints mirror those of the sending endpoint and add the `schedule` parameter, which allows you to specify when you want your targeted users to receive your message. If you include only the `time` parameter in the `schedule` object, all of your users will be messaged at that time.

If you set `in_local_time` or `at_optimal_time` to `true`, do __not__ provide time zone designators in the value of the time parameter (send `"2015-02-20T13:14:47"` instead of `"2015-02-20T13:14:47-05:00"`).

#### Object Body
```json
{
  "schedule": {
    "time": "2015-02-20T13:14:47",
    "in_local_time": true,
    "at_optimal_time": false
  }
}
```

#### Sample Response
```json
{
  "schedule_id": "sample-schedule-id"
}
```

#### Parameter Details

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `time`  | Yes | String in ISO 8601 | The time you want the message to send. |
| `in_local_time`  | No | Boolean | If you set `in_local_time` to be `true`, your users will receive the message at the designated date and time in their respective timezones. If `in_local_time` is true, you will get an error response if the `time` parameter has passed in your company's time zone. |
| `at_optimal_time`  | No | Boolean | If you set `at_optimal_time` to be `true`, your users will receive the message at the designated date at the [optimal time]({{ site.baseurl }}/user_guide/engagement_tools/campaigns/scheduling_and_organizing/scheduling_your_campaign/#option-3-intelligent-delivery) for them (regardless of the time you provide). |

{% endapi %}


{% api %}
## Connected Audience Object
{% apitags %}
Object, Messaging
{% endapitags %}

A Connected Audience is a selector that identifies the audience to send the message to. It is composed of either a single Connected Audience Filter, or several Connected Audience Filters in a logical expression using either "AND" or "OR" operators.


#### Object Body
```json
{
  "schedule": {
    "time": "2015-02-20T13:14:47",
    "in_local_time": true,
    "at_optimal_time": false
  }
}
```

#### Sample Response
```json
{
  "schedule_id": "sample-schedule-id"
}
```

#### Parameter Details

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `time`  | Yes | String in ISO 8601 | The time you want the message to send. |
| `in_local_time`  | No | Boolean | If you set `in_local_time` to be `true`, your users will receive the message at the designated date and time in their respective timezones. If `in_local_time` is true, you will get an error response if the `time` parameter has passed in your company's time zone. |
| `at_optimal_time`  | No | Boolean | If you set `at_optimal_time` to be `true`, your users will receive the message at the designated date at the [optimal time]({{ site.baseurl }}/user_guide/engagement_tools/campaigns/scheduling_and_organizing/scheduling_your_campaign/#option-3-intelligent-delivery) for them (regardless of the time you provide). |

{% endapi %}


{% api %}
## Connected Audience Object
{% apitags %}
Object, Messaging
{% endapitags %}

A Connected Audience is a selector that identifies the audience to send the message to. It is composed of either a single Connected Audience Filter, or several Connected Audience Filters in a logical expression using either "AND" or "OR" operators.

#### Multiple Filter Example
```json
{
  "AND":
    [
      Connected Audience Filter,
      {
        "OR" :
          [
            Connected Audience Filter,
            Connected Audience Filter
          ]
      },
      Connected Audience Filter
    ]
}
```

#### Parameter Details

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `alias_name`  | Yes | String | The user identifier. Your user's alias in Braze. |
| `alias_label`  | Yes | String | Indicates the type of alias. The labels associated with your user's alias in Braze. Users can have multiple aliases with _different_ labels, but only one `alias_name` per `alias_label`. Each `name`:`label` pair is unique across app group. |

{% endapi %}
