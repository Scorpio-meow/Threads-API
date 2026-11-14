# Quote posts



You can use the Threads API to quote another post.

## Permissions

Publishing quote posts requires the following permissions:

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_content_publish` — Required for Threads publishing endpoints only.

If your app has not been approved for advanced access for the `threads_content_publish` permission, you can only post on behalf of [Threads testers](https://developers.facebook.com/documentation/threads/get-started#threads-testers) on your app. After your app is published and approved, you can post on behalf of any Threads user who grants your app the permission.

## Publishing

You can quote another post when making a request to the `POST /threads` endpoint to [create a media object](https://developers.facebook.com/documentation/threads/posts#step-1-create-a-threads-media-container). Make sure to include the following parameter with your API request:

* `quote_post_id` — ID of another post that you want to quote.

### Example request

```bash
curl -i -X POST \
  "https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads?media_type=IMAGE&image_url=https://www.example.com/images/bronz-fonz.jpg&text=BronzFonz&access_token=<ACCESS_TOKEN>" \
  -d quote_post_id="1234567"
```

### Example response

```json
{
  "id": "1234567" // Threads Media Container ID
}
```

The request above creates a Threads media container that, once [published](https://developers.facebook.com/documentation/threads/posts#step-2-publish-the-threads-media-container), has a quote reference to the specified post.

## Media retrieval

All quote posts are labeled accordingly when retrieved. Make a request to the `GET /threads` or `GET /{threads-media-id}` endpoint to [retrieve media object(s)](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts). Make sure to include the following fields with your API request:

* `is_quote_post` — A Boolean field indicating whether a post is a quote post.
* `quoted_post` — Media ID of the post that was quoted.

### Example request

```bash
curl -s -X GET \
  "https://graph.threads.com/v1.0/<THREADS_MEDIA_ID>?fields=id,is_quote_post,quoted_post&access_token=<ACCESS_TOKEN>"
```

### Example response

```json
{
  "id": "12312312312123",
  "is_quote_post": true,
  "quoted_post": {
    "id": "22312312312123"
  }
}
```