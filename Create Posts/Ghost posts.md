# Ghost posts



You can create ghost posts using the Threads API. Ghost posts allow you to create text posts which will be auto-archived after 24 hours.

## Permissions

Publishing ghost posts requires the following permissions:

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_content_publish` — Required for Threads publishing endpoints only.

If your app has not been approved for advanced access for the `threads_content_publish` permission, you can only post on behalf of [Threads testers](https://developers.facebook.com/documentation/threads/get-started#threads-testers) on your app. After your app is published and approved, you can post on behalf of any Threads user who grants your app the permission.

## Limitations

* Ghost posts are text-only posts.
* You cannot reply to any post with a ghost post.
* The only feature supported with ghost posts is [text spoilers](https://developers.facebook.com/documentation/threads/create-posts/spoilers).

## Create a ghost post

### Step 1: Create a media container

Use the `POST /{threads-user-id}/threads` endpoint to create a media container with the `is_ghost_post` parameter.

#### Example request

```bash
curl -i -X POST \
  -d "media_type=TEXT" \
  -d "text=<TEXT>" \
  -d "access_token=<ACCESS_TOKEN>" \
  -d "is_ghost_post=true" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

#### Example response

```json
{
  "id": "<MEDIA_CONTAINER_ID>"
}
```

The `POST /{threads-user-id}/threads` request creates a Threads media container that, once [published](https://developers.facebook.com/documentation/threads/posts#step-2--publish-a-threads-media-container), will create a ghost post.

### Step 2: Publish the media container

You can [publish](https://developers.facebook.com/documentation/threads/posts#step-2--publish-a-threads-media-container) using the returned Threads media container ID to create your ghost post.

## Learn more

* [Retrieve a List of an App-Scoped User's Ghost Posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts#retrieve-a-list-of-an-app-scoped-user-s-ghost-posts)