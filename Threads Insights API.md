# Threads Insights API



The Threads Insights API allows you to read the insights from users' own Threads.

### Permissions

The Threads Insights API requires an appropriate access token and permissions based on the node you are targeting. While you are testing, you can easily generate tokens and grant your app permissions by using the Graph API Explorer.

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_manage_insights` — Required for making `GET` calls to insights endpoints.

### Limitations

* The user insights `since` and `until` parameters do not work for dates before April 13, 2024 (Unix timestamp `1712991600`).

## Media Insights

To retrieve the available insights metrics, send a `GET` request to the `/{threads-media-id}/insights` endpoint with the `metric` parameter containing a comma-separated list of metrics to be returned.

**Note:**

* Returned metrics do not capture nested replies' metrics.
* An empty array will be returned for `REPOST_FACADE` posts because they are posts made by other users.

### Available Metrics

| Name | Description |
| --- | --- |
| `views` | The number of times your post was played or displayed.<br><br>**Note:** This metric is [in development](https://www.facebook.com/business/help/metrics-labeling). |
| `likes` | The number of likes on the post. |
| `replies` | The number of replies on the post.  <br><br>**Note:** When the requested media is a root post, this number includes total replies. If the media is itself a reply, this number includes only **direct** replies. |
| `reposts` | The number of times the post was reposted. |
| `quotes` | The number of times the post was quoted. |
| `shares` | The number of shares of your Threads posts.<br><br>**Note:** This metric is [in development](https://www.facebook.com/business/help/metrics-labeling). |

### Example Request

```
curl -s -X GET \
  -F "metric=likes,replies" \
  -F "access_token=<THREADS_ACCESS_TOKEN>"
"https://graph.threads.com/v1.0/<THREADS_MEDIA_ID>/insights"
```

### Example Response

```
{
  "data": [
    {
      "name": "likes",
      "period": "lifetime",
      "values": [
        {
          "value": 100
        }
      ],
      "title": "Likes",
      "description": "The number of likes on your post.",
      "id": "<media_id>/insights/likes/lifetime"
    },
    {
      "name": "replies",
      "period": "lifetime",
      "values": [
        {
          "value": 10
        }
      ],
      "title": "Replies",
      "description": "The number of replies on your post.",
      "id": "<media_id>/insights/replies/lifetime"
    }
  ]
}
```

## User Insights

To retrieve the available user insights metrics, send a `GET` request to the `/{threads-user-id}/threads_insights` endpoint with the `metric` parameter, and optionally, the `since` and `until` parameters.  
**Warning:** User insights are not guaranteed to work before June 1, 2024.

### Parameters
| Name | Description |
| --- | --- |
| `since` | **Optional.**  <br>Used in conjunction with the `until` parameter to define a range. If you omit `since` and `until`, it defaults to a 2-day range: yesterday through today.  <br>**Note:** The earliest Unix timestamp that can be used is `1712991600`, any timestamp before that will be rejected.<br><br>**Format:** Unix Timestamp |
| `until` | **Optional.**  <br>Used in conjunction with the `since` parameter to define a range. If you omit `since` and `until`, it defaults to a 2-day range: yesterday through today.  <br>**Note:** The earliest Unix timestamp that can be used is `1712991600`, any timestamp before that will be rejected.<br><br>**Format:** Unix Timestamp |
| `metric` | **Required.**  <br>A comma-separated list of the metrics to be returned. Must be at least one of the user metrics values. |

### User Metrics
| Name | Response Type | Description |
| --- | --- | --- |
| `views` | Time Series | The number of times your profile was viewed. |
| `likes` | Total Value | The  number of likes on your posts. |
| `replies` | Total Value | The number of replies on your posts.<br><br>**Note:** This number includes only top-level replies. |
| `reposts` | Total Value | The number of times your posts were reposted. |
| `quotes` | Total Value | The number of times your posts were quoted. |
| `clicks` | Link Total Values | The number of times people clicked on URLs you shared. |
| `followers_count` | Total Value | Your total number of followers on Threads.<br><br>**Note:**<br><br>* This metric does not support the `since` and `until` parameters. |
| `follower_demographics` | Total Value | The demographic characteristics of followers, including countries, cities, and gender distribution.<br><br>**Note:**<br><br>* This metric does not support the `since` and `until` parameters.  <br>* A Threads profile must have at least 100 followers to fetch this metric.<br>* Can only have one `breakdown` parameter, which must be equal to one of the following values: `country`, `city`, `age`, or `gender`. |

### Example Request

```
curl -s -X GET \
  -F "metric=views" \
  -F "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads_insights"
```

### Example Time Series Metric Response

```
{
  "data": [
    {
      "name": "views",
      "period": "day",
      "values": [
        {
          "value": 10,
          "end_time": "2024-07-12T08:00:00+0000"
        },
        {
          "value": 20,
          "end_time": "2024-07-15T08:00:00+0000"
        },
        {
          "value": 30,
          "end_time": "2024-07-16T08:00:00+0000"
        }
      ],
      "title": "views",
      "description": "The number of times your profile was viewed.",
      "id": "37602215421583/insights/views/day"
    }
  ]
}
```

### Example Total Value Metric Response

```
{
  "data": [
    {
      "name": "views",
      "period": "day",
      "total_value" : {
        "value": 1
      }
      "title": "views",
      "description": "The number of times your profile was viewed.",
      "id": "37602215421583/insights/views/day"
    }
  ]
}
```

### Example Link Total Value Response

```
{
  "data": [
    {
      "name": "clicks",
      "period": "day",
      "link_total_values": [
        {
          "value": 11,
          "link_url": "https://ai.meta.com/blog/"
        }
      ],
      "title": "clicks",
      "description": "The number of times users clicked on a link.",
      "id": "37602215421583/insights/clicks/day"
    }
  ]
}
```