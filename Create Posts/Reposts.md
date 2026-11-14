# Reposts



You can use the Threads API to repost another post.

## Permissions

Reposting requires the following permissions:

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_content_publish` — Required for Threads publishing endpoints only.

If your app has not been approved for advanced access for the `threads_content_publish` permission, you can only post on behalf of [Threads testers](https://developers.facebook.com/documentation/threads/get-started#threads-testers) on your app. After your app is published and approved, you can post on behalf of any Threads user who grants your app the permission.

## Publishing

You can repost another post when making a request to the `POST /{threads-media-id}/repost` endpoint. Make sure to include the Threads post ID with your API request:

### Example request

```bash
curl -i -X POST \
  "https://graph.threads.com/v1.0/<THREADS_POST_ID>/repost?access_token=<ACCESS_TOKEN>"
```

### Example response

```json
{
  "id": "1234567" // Threads Repost ID
}
```

The request above reposts an original Threads post. Once done, the reposted post appears under the **Reposts** tab of the user's Threads profile.

## Media retrieval

All reposts have the media type of `REPOST_FACADE` when retrieved. Make a request to the `GET /threads` endpoint to retrieve the reposts. Make sure to include the following fields with your API request:

* `media_type` — The type of Threads post.
* `reposted_post` — Media ID of the post that was reposted.

### Example request

```bash
curl -s -X GET \
  "https://graph.threads.com/v1.0/<THREADS_MEDIA_ID>?fields=id,media_type,reposted_post&access_token=<ACCESS_TOKEN>"
```

### Example response

```json
{
  "id": "12312312312123",
  "media_type": "REPOST_FACADE",
  "reposted_post": {
    "id": "22312312312123"
  }
}
```