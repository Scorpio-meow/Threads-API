# Threads API insights



The Threads insights endpoints allow you to retrieve insights for Threads media objects and users. See [Threads Insights API](https://developers.facebook.com/documentation/threads/insights) for more information.

## `GET /{threads-media-id}/insights`

Retrieve insights for a Threads media object. See [Media insights](https://developers.facebook.com/documentation/threads/insights#media-insights) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads API user access token. |
| `threads-media-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads media identifier. |
| `metric`<br><br>string | **Required.**  <br>A comma-separated list of the metrics to be returned. Must be at least one of the metric values.  <br>**Values:** `views`, `likes`, `replies`, `reposts`, `quotes`, `shares` |

## `GET /{threads-user-id}/threads_insights`

Retrieve insights for a Threads user. See [User insights](https://developers.facebook.com/documentation/threads/insights#user-insights) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads API user access token. |
| `threads-user-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads user identifier. |
| `since`<br><br>datetime | **Optional.**  <br>Used in conjunction with the `until` parameter to define a range. If you omit `since` and `until`, it defaults to a 2-day range: yesterday through today.  <br>**Format:** A Unix timestamp (such as `1767225600`) or a date (such as `2026-01-01`) |
| `until`<br><br>datetime | **Optional.**  <br>Used in conjunction with the `since` parameter to define a range. If you omit `since` and `until`, it defaults to a 2-day range: yesterday through today.  <br>**Format:** A Unix timestamp (such as `1767225600`) or a date (such as `2026-01-01`) |
| `metric`<br><br>string | **Required.**  <br>A comma-separated list of the metrics to be returned. Must be at least one of the metric values.  <br>**Values:** `views`, `likes`, `replies`, `reposts`, `quotes`, `clicks`, `followers_count`, `follower_demographics`  <br>**Note:** `follower_demographics` is not compatible with the `since` and `until` parameters. |