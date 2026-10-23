# Retrieve and Manage Replies



The Threads Reply Management API allows you to read and manage replies to users' own Threads.

## Permissions

The Threads Reply Management API requires an appropriate access token and permissions based on the node you are targeting. While you are testing, you can generate tokens and grant your app permissions by using the Graph API Explorer.

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_content_publish` — Required for Threads publishing endpoints only.
* `threads_manage_replies` — Required for making `POST` calls to reply endpoints.
* `threads_read_replies` — Required for making `GET` calls to reply endpoints.

## Rate limits

Threads profiles are limited to 1,000 API-published replies within a 24-hour moving period. You can retrieve a profile's current Threads replies rate limit usage with the `GET /{threads-user-id}/threads_publishing_limit` endpoint.

**Note:** This endpoint requires the `threads_basic`, `threads_content_publish`, and `threads_manage_replies` permissions.

#### Fields

| Name | Description |
| --- | --- |
| `reply_quota_usage` | Threads reply publishing count over the last 24 hours. |
| `reply_config` | Threads reply publishing rate limit config object, which contains the `quota_total` and `quota_duration` fields. |

#### Example request

```
curl -s -X GET \
  "https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads_publishing_limit?fields=reply_quota_usage,reply_config&access_token=<ACCESS_TOKEN>"
```

#### Example response

```
{
  "data": [
    {
      "reply_quota_usage": 1,
      "reply_config": {
        "quota_total": 1000,
        "quota_duration": 86400
      }
    }
  ]
}
```

## Next steps

* [Create Replies](https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/create-replies)
* [Retrieve Replies and Conversations](https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/replies-and-conversations)
* [Reply Management](https://developers.facebook.com/documentation/threads/reply-management)