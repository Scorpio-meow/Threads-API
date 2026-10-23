# Create Replies



### Permissions

Creating replies requires the following permissions:

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_content_publish` — Required for Threads publishing endpoints only.
* `threads_manage_replies` — Required for creating replies with the `reply_to_id` parameter.

If your app has not been approved for advanced access for the `threads_content_publish` permission, you can only post on behalf of [Threads testers](https://developers.facebook.com/documentation/threads/get-started#threads-testers) on your app. After your app is published and approved, you can post on behalf of any Threads user who grants your app the permission.

In addition, to reply to a thread, you must meet one of the following requirements:

* You are the owner of the root Threads post.
* Your app has either the `threads_keyword_search` or the `threads_manage_mentions` permission.

## Respond to replies

### Step 1: Use the `reply_to_id` parameter to reply to a specific reply under the root post.

#### Example request

```bash
curl -X POST \
  -F "media_type=<MEDIA_TYPE>" \
  -F "text=<TEXT>" \
  -F "reply_to_id=<THREADS_ID>" \
  -F "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/me/threads"
```

#### Example response

```json
{
 "id": "1234567890"
}
```

### Step 2: Use the `POST /{threads-user-id}/threads_publish` endpoint to publish the reply container ID returned in the previous step.

Wait about 30 seconds before publishing to allow the Threads media pipeline to finish processing the upload. See the [media container status endpoint](https://developers.facebook.com/documentation/threads/troubleshooting#publishing-does-not-return-a-media-id) for more details.

#### Parameters

* `creation_id` —  Identifier of the Threads media container created from the `/threads` endpoint.

#### Example request

```bash
curl -i -X POST \
  -F "creation_id=<MEDIA_CONTAINER_ID>" \
  -F "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads_publish"
```

#### Example response

```json
{
  "id": "1234567" // Threads Reply Media ID
}
```