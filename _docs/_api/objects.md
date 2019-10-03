---
nav_title: Objects & Filters
layout: api_objects_page
excerpt_separator: ""
page_order: 2
---

{% api %}
## Apple Push Object
{% apitags %}
Objects, For Messaging Endpoints
{% endapitags %}

You must include an Apple Push Object in `messages` if you want targeted users to receive a push on their iOS devices. The total number of bytes in your `alert` string, `extra` object, and other optional parameters should not exceed `1912`. The Messaging API will return an error if you exceed the message size allowed by Apple. Messages that include the keys `ab` or `aps` in the `extra` object will be rejected.


#### Object Body

```json
{
   "badge": "3",
   "alert": "This is my alert.",
   "sound": "default",
   "extra": "",
   "content-available": "false",
   "expiry": (optional, ISO 8601 date string) if set, push messages will expire at the specified datetime,
   "custom_uri": (optional, string) a web URL, or Deep Link URI,
   "message_variation_id": (optional, string) used when providing a campaign_id to specify which message variation this message should be tracked under (must be an iOS Push Message),
   "notification_group_thread_id": (optional, string) the notification group thread ID the notification will be sent with,
   "asset_url": (optional, string) content URL for rich notifications for devices using iOS 10 or higher,
   "asset_file_type": (required if asset_url is present, string) file type of the asset - one of "aif", "gif", "jpg", "m4a", "mp3", "mp4", "png", or "wav",
   "collapse_id": (optional, string) To update a notification on the user's device once you've issued it, send another notification with the same collapse ID you used previously
   "mutable_content": (optional, boolean) if true, Braze will add the mutable-content flag to the payload and set it to 1. The mutable-content flag is automatically set to 1 when sending a rich notification, regardless of the value of this parameter.
   "send_to_most_recent_device_only": (optional, boolean) defaults to false, if set to true, Braze will only send this push to a user's most recently used iOS device, rather than all eligible iOS devices,
   "category": (optional, string) the iOS notification category identifier for displaying push action buttons,
   "buttons" : (optional, array of Apple Push Action Button Objects) push action buttons to display
}
```

#### Parameter Details

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `badge`| No | Integer | The badge count after this message. |
| `alert`| Yes <br> <br> _Unless content-available is set as `true`._ | String or Apple Push Alert Object. | The notification message. |
| `sound`| No | String | the location of a custom notification sound within the app. <br> <br> Specifying `default` in the sound field will play the standard notification sound. |
| `extra`| No | Object | Additional keys and values to be sent. |
| `content-available`| No | Boolean | If set, Braze will add the `content-available` flag to the push payload. |
| `expiry`| No | Sting in ISO 8601 datetime. | If set, push messages will expire at the specified datetime. |
| `custom_uri`| No | Sting | A web URL, or Deep Link URI. |
| `message_variation_id`| No | Sting | Used when providing a `campaign_id` to specify which message variation this message should be tracked under (must be an iOS Push Message). |
| `notification_group_thread_id`| No | Sting | The notification group thread ID the notification will be sent with.
| `asset_url`| No | String | Content URL for rich notifications for devices using iOS 10 or higher. |
| `asset_file_type` | Yes, if `asset_url` is present. | String | File type of the asset - one of `aif`, `gif`, `jpg`, `m4a`, `mp3`, `mp4`, `png`, or `wav`. |
| `collapse_id`| No | Sting | To update a notification on the user's device once you've issued it, send another notification with the same collapse ID you used previously
| `mutable_content`| No | Boolean | If `true`, Braze will add the mutable-content flag to the payload and set it to `1`. The mutable-content flag is automatically set to `1` when sending a rich notification, regardless of the value of this parameter. |
| `send_to_most_recent_device_only`| No | Boolean | Defaults to `false`. If set to `true`, Braze will only send this push to a user's most recently used iOS device, rather than all eligible iOS devices. |
| `category`| No | String | The iOS notification category identifier for displaying push action buttons. |
| `buttons` | No | Array of Apple Push Action Button Objects. | Push action buttons to display. |

{% endapi %}


{% api %}
## Apple Push Alert Object
{% apitags %}
Objects, For Messaging Endpoints
{% endapitags %}


The Apple Push Alert Object is the notification message contained within an Apple Push Object with the parameter `alert`.

In most cases, `alert` can just be specified in an `apple_push` object as a string. You should specify `alert` as an object only in cases where you need specific localization or Apple Watch customization.

#### Object Body

```json
{
   "body": "This is the text of your message.",
   "title": "This is the purpose of the notification.",
   "title_loc_key": "your_localizable_string",
   "title_loc_args": "array_of_varible_string_values",
   "action_loc_key": "alert_will_include_buttons",
   "loc_key": "alert-message_string",
   "loc_args": "format_specifiers_in_loc_key"
}
```

#### Parameter Details

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `body` | Yes, unless `content-available` is `true` in the Apple Push Object. | String | the text of the alert message,
| `title` | No | String |  a short string describing the purpose of the notification, displayed as part of the Apple Watch notification interface,
| `title_loc_key` | No | String |  the key to a title string in the `Localizable.strings` file for the current localization,
| `title_loc_args` | No | Array of Strings | variable string values to appear in place of the format specifiers in title_loc_key,
| `action_loc_key` | No | String |  if a string is specified, the system displays an alert that includes the Close and View buttons, the string is used as a key to get a localized string in the current localization to use for the right button’s title instead of "View",
| `loc_key` | No | String |  a key to an alert-message string in a Localizable.strings file for the current localization,
| `loc_args` | No | Array of Strings | variable string values to appear in place of the format specifiers in loc_key

{% endapi %}




{% api %}
## Canvas Entry Properties Object
{% apitags %}
Objects, For Messaging Endpoints
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
## Connected Audience Object & Filter
{% apitags %}
Objects, For Messaging Endpoints, Filters
{% endapitags %}

A Connected Audience is a selector that identifies the audience to send the message to. It is composed of either a single Connected Audience Filter, or several Connected Audience Filters in a logical expression using either `AND`/`OR` operators.

The Connected Audience filters are `AND`/`OR` operators used to create an Connected Audience Object using custom attributes to segment your audience. You can create a campaign and populate its content and segmentation values dynamically with a single API call.


#### Multiple Filter Body Layout Example
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

#### Example with Custom Attributes

This filter will segment an audience for your campaign for recipients with either green or brown eyes.

```json
"OR":
[
  {
    "custom_attribute": {
      "custom_attribute_name": "eye_color",
      "comparison": "equals",
      "value": "green"
      }
    },
  {
    "custom_attribute": {
      "custom_attribute_name": "eye_color",
      "comparison": "equals",
      "value": "brown"
      }
    }
]
```

{% endapi %}

{% api %}
## Custom Attribute Filter
{% apitags %}
Filters, For Messaging Endpoints
{% endapitags %}

This filter allows you to segment based on a user's custom attribute.

#### Filter Body
```json
{
  "custom_attribute":
    {
      "custom_attribute_name": "your_custom_attribute_name",
      "comparison": "equals",
      "value": "set_value"
    }
}
```

#### Parameter Details

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `custom_attribute_name` | Yes | String | The name of the custom attribute you wish to use as a filter. |
| `comparison` | Yes | String | One of the allowed comparisons to make against the provided value. The `comparison` must be taken from the allowed list of Custom Attribute Type Details below. |
| `value` | Yes | String, Numeric, or Boolean | The value to be compared using the provided comparison. <br> <br> A `value` is not required when using the `exists` or `does_not_exist` comparisons. A `value` must be an ISO 8601 DateTime string when using the `before` and `after` comparisons. |


##### Custom Attribute Type Details
The custom attribute's type determines the comparisons that are valid for a given filter.

| Custom Attribute Type | Allowed Comparisons |
| ---------------------| --------------- |
| String | `equals`, `not_equal`, `matches_regex`, `does_not_match_regex`, `exists`, `does_not_exist` |
| Array | `includes_value`, `does_not_include_value`, `exists`, `does_not_exist` |
| Numeric | `equals`, `not_equal`, `greater_than`, `greater_than_or_equal_to`, `less_than`, `less_than_or_equal_to`, `exists`, `does_not_exist` |
| Boolean | `equals`, `does_not_equal`, `exists`, `does_not_exist` |
| Time | `less_than_x_days_ago`, `greater_than_x_days_ago`, `less_than_x_days_in_the_future`, `greater_than_x_days_in_the_future`, `after`, `before`, `exists`, `does_not_exist`


#### Custom Attribute Example
```json
{
  "custom_attribute":
    {
      "custom_attribute_name": "eye_color",
      "comparison": "equals",
      "value": "blue"
    }
}

{
  "custom_attribute":
  {
    "custom_attribute_name": "favorite_foods",
    "comparison": "includes_value",
    "value": "pizza"
  }
}

{
  "custom_attribute":
  {
    "custom_attribute_name": "last_purchase_time",
    "comparison": "less_than_x_days_ago",
    "value": 2
  }
}
```
{% endapi %}

{% api %}
## Email Subscription Filter
{% apitags %}
Filters, For Messaging Endpoints
{% endapitags %}

This filter allows you to segment based on a user's email subscription status.

#### Filter Body

```json
{
  "email_subscription_status":
  {
    "comparison": "is",
    "value": "opted_in"
  }
}
```

#### Parameter Details

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `comparison` | Yes | String | One of the allowed comparisons to make against the provided value. The `comparison` must be taken from the allowed list of Allowed Comparisons below. |
| `value` | Yes | String, Numeric, or Boolean | The value to be compared using the provided comparison. <br> <br> The `value` must be taken from the allowed list of Allowed Comparisons below. |


##### Allowed Comparisons

| Allowed Comparisons | Allowed Values |
| ---------------------| --------------- |
| `is`, `is_not` | `opted_in`, `subscribed`, `unsubscribed` |

{% endapi %}


{% api %}
## Last Used App Filter
{% apitags %}
Filters, For Messaging Endpoints
{% endapitags %}

This filter allows you to segment based on the last time a user used your app.

#### Filter Body

```json
{
  "last_used_app":
  {
    "comparison": "after",
    "value": "2019-09-15T15:53:00"
  }
}
```

#### Parameter Details

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `comparison` | Yes | String | One of the allowed comparisons to make against the provided value. The `comparison` must be taken from the allowed list of Allowed Comparisons below. |
| `value` | Yes | String, Numeric, or Boolean | The value to be compared using the provided comparison. <br> <br> The `value` must be a datetime in ISO 8601 string. |


##### Allowed Comparisons

| Allowed Comparisons | Allowed Values |
| ---------------------| --------------- |
| `after`, `before` | Datetime (ISO 8601 string). |

{% endapi %}



{% api %}
## Push Subscription Filter
{% apitags %}
Filters, For Messaging Endpoints
{% endapitags %}

This filter allows you to segment based on a user's push subscription status. These filters contain two fields:

#### Filter Body

```json
{
  "push_subscription_status":
  {
    "comparison": "is",
    "value": "opted_in"
  }
}
```

#### Parameter Details

| Parameter | Required | Data Type | Description |
|---|---|---|---|
| `comparison` | Yes | String | One of the allowed comparisons to make against the provided value. The `comparison` must be taken from the allowed list of Allowed Comparisons below. |
| `value` | Yes | String, Numeric, or Boolean | The value to be compared using the provided comparison. <br> <br> The `value` must be taken from the allowed list of Allowed Comparisons below. |


##### Allowed Comparisons

| Allowed Comparisons | Allowed Values |
| ---------------------| --------------- |
| `is`, `is_not` | `opted_in`, `subscribed`, `unsubscribed` |

{% endapi %}



{% api %}
## Recipient Object
{% apitags %}
Objects, For Messaging Endpoints
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
## Schedule Object
{% apitags %}
Objects, For Messaging Endpoints
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
## Trigger Properties Object
{% apitags %}
Objects, For Messaging Endpoints
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
## User Alias Object
{% apitags %}
Objects, For Messaging Endpoints
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
