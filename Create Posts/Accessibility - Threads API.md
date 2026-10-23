# Accessibility - Threads API



To aid users who are visually impaired, you can use Threads API to set the accessibility label or alt text for each image or video that is attached to your post.

## Permissions

Publishing posts with alt text requires the following permissions:

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_content_publish` — Required for Threads publishing endpoints only.

If your app has not been approved for advanced access for the `threads_content_publish` permission, you can only post on behalf of [Threads testers](https://developers.facebook.com/documentation/threads/get-started#threads-testers) on your app. After your app is published and approved, you can post on behalf of any Threads user who grants your app the permission.

### Limitations

This feature isn't available for text-only posts. It will only work on image, video, and carousel posts.

## Publishing

Alt text can be configured when making a request to the `POST /threads` endpoint to [create a media object](https://developers.facebook.com/documentation/threads/posts#step-1--create-a-threads-media-container). Make sure to include the following parameter with your API request:

* `alt_text` — (For images and videos only.) The accessibility text label or description for an image or video in a Threads post.

### Example Request

```
curl -i -X POST \
  "https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads?media_type=IMAGE&image_url=https://www.example.com/images/bronz-fonz.jpg&text=BronzFonz&access_token=<ACCESS_TOKEN>"
  -d alt_text="Photograph of Bronze Fonz Statue"
```

### Example Response

```
{
  "id": "1234567" // Threads Media Container ID
}
```

The request above creates a Threads post container that, [once published](https://developers.facebook.com/documentation/threads/posts#step-2--publish-a-threads-media-container), will add a custom accessibility label to your media.

## Media Retrieval

The value for alt text can be retrieved when making a request to the `GET /threads` or `GET /{threads_media_id}` endpoint to retrieve media object(s). Make sure to include the following field with your API request:

* `alt_text` — The accessibility text label or description for an image or video in a Threads post.

### Example Request

```
curl -s -X GET \
  "https://graph.threads.com/v1.0/<THREADS_MEDIA_ID>?fields=id,alt_text&access_token=<ACCESS_TOKEN>"
```

### Example Response

```
{
   "id": "12312312312123",
   "alt_text": "Photograph of Bronze Fonz Statue",
}
```