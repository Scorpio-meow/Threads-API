# Threads Posts



You can use the Threads API to publish image, video, text, or carousel posts.

This document covers:

* [Single Thread Posts](#single-thread-posts)
* [Carousel Posts](#carousel-posts)
* [Topic Tags, Links, and GIFs](#topic-tags--links--and-gifs)
* [Media Specifications](#media-specifications)

## Permissions

Publishing posts requires the following permissions:

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_content_publish` — Required for Threads publishing endpoints only.

If your app has not been approved for advanced access for the `threads_content_publish` permission, you can only post on behalf of [Threads testers](https://developers.facebook.com/documentation/threads/get-started#threads-testers) on your app. After your app is published and approved, you can post on behalf of any Threads user who grants your app the permission.

## Single thread posts

Publishing a single image, video, or text post is a two-step process:

1. Create a media container with text only or with an image or video hosted on your public server with optional text using the `POST /{threads-user-id}/threads` endpoint.
2.  Publish the media container using the `POST /{threads-user-id}/threads_publish` endpoint.

### Limitations

* Text posts are limited to 500 characters.
* Emojis are counted as the [number of UTF-8 bytes](https://www.npmjs.com/package/grapheme-splitter).

### Step 1: Create a Threads media container

Use the `POST /{threads-user-id}/threads` endpoint to create a Threads media container.

#### Parameters

| Name | Description |
| --- | --- |
| `is_carousel_item`<br><br>Boolean | **Required.**  <br>Indicates that images and/or videos will appear in a carousel.<br><br>**Values:** `true`, `false` (*default* for single thread posts) |
| `media_type`<br><br>string | **Required.**  <br>Indicates the current media type.<br><br>**Values:** `TEXT`, `IMAGE`, `VIDEO`<br><br>**Note:** `CAROUSEL` is not available for single thread posts. |
| `image_url`<br><br>URL | **Optional. Required for `media_type=IMAGE`.**  <br>The URL path to the image.<br><br>**Note:** Threads retrieves your image from the URL provided, so it must be on a public server. |
| `video_url`<br><br>URL | **Optional. Required for `media_type=VIDEO`.**  <br>The URL path to the video.<br><br>**Note:** Threads retrieves your video from the URL provided, so it must be on a public server. |
| `text`<br><br>string | **Optional. Required for `media_type=TEXT`.**  <br>The text associated with the post. If any URLs are included, the first URL in the `text` field will be used as the link preview for the post.<br><br>**Note:** For the post character limit, emojis are counted as the [number of UTF-8 bytes](https://www.npmjs.com/package/grapheme-splitter). |

Refer to the [`POST /{threads-user-id}/threads` endpoint reference](https://developers.facebook.com/documentation/threads/reference/publishing#post---threads-user-id--threads) for additional supported parameters.

#### Example request

```html
curl -i -X POST \
  -d "media_type=IMAGE" \
  -d "image_url=<IMAGE_URL>" \
  -d "text=<TEXT>" \
  -d "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

#### Example response

```json
{
  "id": "<THREADS_MEDIA_CONTAINER_ID>"
}
```

### Step 2: Publish the Threads media container

Use the `POST /{threads-user-id}/threads_publish` endpoint to publish the media container ID returned in the previous step.

It is recommended to wait on average 30 seconds before publishing a Threads media container to give our server enough time to fully process the upload. See the [media container status endpoint](https://developers.facebook.com/documentation/threads/troubleshooting#publishing-does-not-return-a-media-id) for more details.

#### Parameters

| Name | Description |
| --- | --- |
| `creation_id`<br><br>int | **Required.**  <br>The Threads media container ID. |

#### Example request

```html
curl -i -X POST \
  -d "creation_id=<MEDIA_CONTAINER_ID>" \
  -d "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads_publish"
```

#### Example response

```json
{
  "id": "<THREADS_MEDIA_ID>"
}
```

## Carousel posts

You may publish up to 20 images, videos, or a mix of the two in a carousel post. Publishing carousels is a three-step process:

1. Create the individual media containers for each image and video that should appear in the carousel using the `POST /{threads-user-id}/threads` endpoint.
2. Create a single carousel container to contain the media containers using the `POST /{threads-user-id}/threads` endpoint.
3. Publish the carousel container using the `POST /{threads-user-id}/threads_publish` endpoint.

**Note:** Carousel posts count as a single post against a profile's [rate limit](https://developers.facebook.com/documentation/threads/overview#rate-limiting).

### Limitations

* Carousels are limited to 20 images, videos, or a mix of the two.
* Carousels require a minimum of two children.

### Step 1: Create a media container

Use the `POST /{threads-user-id}/threads` endpoint to create a media container for each of the images and/or videos that will appear in the carousel.

#### Parameters

| Name | Description |
| --- | --- |
| `is_carousel_item`<br><br>Boolean | **Required.**  <br>Indicates that images and/or videos will appear in a carousel when set to `true`.<br><br>**Values:** `true`, `false` |
| `media_type`<br><br>string | **Required.**  <br>Indicates the current media type.<br><br>**Values:** `IMAGE`, `VIDEO`<br><br>**Note:** `CAROUSEL` is not available for single thread posts. |
| `image_url`<br><br>URL | **Optional. Required for `media_type=IMAGE`.**  <br>The URL path to the image.<br><br>**Note:** Threads retrieves your image from the URL provided, so it must be on a public server. |
| `video_url`<br><br>URL | **Optional. Required for `media_type=VIDEO`.**  <br>The URL path to the video.<br><br>**Note:** Threads retrieves your video from the URL provided, so it must be on a public server. |
| `text`<br><br>string | **Optional.**  <br>The text associated with the post. If any URLs are included, the first URL in the `text` field will be used as the link preview for the post.<br><br>**Note:** For the post character limit, emojis are counted as the [number of UTF-8 bytes](https://www.npmjs.com/package/grapheme-splitter). |

Refer to the [`POST /{threads-user-id}/threads` endpoint reference](https://developers.facebook.com/documentation/threads/reference/publishing#post---threads-user-id--threads) for additional supported parameters.

#### Example request

```html
curl -i -X POST \
  -d "image_url=<IMAGE_URL>" \
  -d "is_carousel_item=true" \
  -d "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

#### Example response

```json
{
  "id": "<THREADS_MEDIA_CONTAINER_ID>"
}
```

If the operation is successful, the API will return a media container ID, which can be used when creating the carousel container.

Repeat this process for each image and/or video that will appear in the carousel.

### Step 2: Create a carousel container

Use the `POST /{threads-user-id}/threads` endpoint to create a carousel container.

#### Parameters

| Name | Description |
| --- | --- |
| `media_type`<br><br>string | **Required.**  <br>Indicates the current media type.<br><br>**Value:** `CAROUSEL` |
| `children`<br><br>list<int> | **Required.**  <br>A comma-separated list of the media container IDs of the images and/or videos that should appear in the published carousel.<br><br>**Note:** Carousels must have at least 2 and no more than 20 total images, videos, or a mix of the two. |
| `text`<br><br>string | **Optional.**  <br>The text associated with the post. |

Refer to the [`POST /{threads-user-id}/threads` endpoint reference](https://developers.facebook.com/documentation/threads/reference/publishing#post---threads-user-id--threads) for additional supported parameters.

#### Example request

```html
curl -i -X POST \
  -d "media_type=CAROUSEL" \
  -d "children=<MEDIA_ID_1>,<MEDIA_ID_2>,<MEDIA_ID_3>,..." \
  -d "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

#### Example response

```json
{
  "id": "<THREADS_CAROUSEL_CONTAINER_ID>"
}
```

### Step 3: Publish the carousel container

Use the `POST /{threads-user-id}/threads_publish` endpoint to publish a carousel post.

**Note:** Profiles are limited to 250 published posts within a 24-hour period. Publishing a carousel counts as a single post.

#### Parameters

| Name | Description |
| --- | --- |
| `creation_id`<br><br>int | **Required.**  <br>The Threads carousel container ID. |

#### Example request

```html
curl -i -X POST \
  -d "creation_id=<MEDIA_CONTAINER_ID>" \
  -d "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads_publish"
```

#### Example response

```json
{
  "id": "<THREADS_MEDIA_ID>"
}
```

If the operation is successful, the API will return the carousel album's Threads media ID.

## Topic tags, links, and GIFs {#topic-tags--links--and-gifs}

Topics and links appear in posts in such a way as to encourage engagement.

### Topic tags

Topics make posts more social by allowing central topics of discussion. You can include a topic in a post either by using the `topic_tag` parameter or by including a tag within the text of a post.

#### Using the `topic_tag` parameter

**Note:** Topic tags must be at least 1 character and no more than 50 characters long. The following characters are not allowed:

* Periods (.)
* Ampersands (&)

##### Example request

```html
curl -i -X POST \
  -d "media_type=TEXT" \
  -d "text=<Text>" \
  -d "access_token=<ACCESS_TOKEN>" \
  -d "topic_tag=<TAG>" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

#### Using an in-text topic tag

**Warning:** This method is not preferred but is kept for backward compatibility.

A topic can also be attached to a post by including it in-line within the text of the post. Only one topic tag is allowed per post, so the first valid tag included in a post of any type (text-only, image, video, carousel) via the API is treated as the tag for that post.

Information to keep in mind when adding a topic to a post using an in-text tag:

* Valid tags start with a hash sign (#).  
* The text is also configured in the app without the hash sign.
* Topic must be at least 1 character and no more than 50 characters long.
* Whole numbers that are preceded by a hash sign (i.e., #1) will not be converted into a tag. This is because it is assumed that # is signifying a number sign in this scenario.
* The following characters are not allowed when using in-text tags with the Threads API, so any in-text tag that starts with a hash sign will end just before these characters:

* Spaces, Tabs, New Line Characters
* Periods (.)
* Ampersands (&)
* At Signs (@)
* Exclamation Marks (!)
* Question Marks (?)
* Commas (,)
* Semi-Colons (;)
* Colons (:)

### Links

To attach a link to your post, use the `link_attachment` parameter when creating a media container.
If no `link_attachment` parameter is provided, then the first link made in a text-only post via the API is configured as the link attachment, which displays as a preview card, to make it easier to engage with and click on.

#### Limitations

* This feature is only available for text-only posts. It will not work with image, video, or carousel posts.
* The number of links is restricted to 5 or fewer.

**Warning:** Starting December 22, 2025, Threads posts containing more than 5 links will fail to post during the media creation step (`POST /{threads-user-id}/threads`) with the error code: `THREADS_API__LINK_LIMIT_EXCEEDED`.

How links are counted:

* All unique URLs found in the text field are counted as links.
* If the `link_attachment` field contains a URL that is different from all URLs in the text field, it is counted as an additional link.
* If the `link_attachment` URL is the same as any URL in the text field, it is only counted once, rather than twice.

Examples:

* If the `text` field contains only www.facebook.com, and the `link_attachment` is also www.facebook.com, this counts as 1 link.
* If the `text` field contains www.instagram.com and www.threads.com, and the `link_attachment` is www.facebook.com, this counts as 3 links.
* If the `text` field contains www.example.com, www.example.com, and www.test.com, and the `link_attachment`  is www.test.com, this counts as 2 links (www.example.com and www.test.com are each counted once).

If you receive this error, reduce the number of unique links in your post to 5 or fewer.

#### Publishing

Links can be attached when making an API call to the `POST /{threads-user-id}/threads` endpoint to [create a media container](https://developers.facebook.com/documentation/threads/posts#step-1--create-a-threads-media-container).

| Name | Description |
| --- | --- |
| `link_attachment`<br><br>URL | **Optional.**  <br>The URL that should be attached to a Threads post and displayed as a link preview. This must be a valid, publicly accessible URL.<br><br>**Note:** Can only be used for `media_type=TEXT` posts. |

##### Example request

```html
curl -i -X POST \
  -d "media_type=TEXT" \
  -d "text=<TEXT>" \
  -d "access_token=<ACCESS_TOKEN>" \
  -d "link_attachment=<URL> \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

##### Example response

```json
{
  "id": "<THREADS_MEDIA_CONTAINER_ID>"
}
```

The request above creates a Threads media container that, once [published](https://developers.facebook.com/documentation/threads/posts#step-2--publish-a-threads-media-container), will attach a link preview to your media.

#### Media Retrieval

The value for the `link_attachment` URL can be retrieved by making a request to the `GET /threads` or `GET /{threads_media_id}` endpoint to [retrieve media object(s)](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts).

| Name | Description |
| --- | --- |
| `link_attachment_url`<br><br>URL | The URL attached to a Threads post. |

##### Example request

```html
curl -s -X GET \
"https://graph.threads.com/v1.0/<THREADS_MEDIA_ID>?fields=id,link_attachment_url&access_token=<ACCESS_TOKEN>"
```

##### Example response

```json
{
   "id": "<THREADS_MEDIA_ID>",
   "link_attachment_url": "<LINK_ATTACHMENT_URL>",
}
```

### GIFs

GIFs make posts more engaging by allowing users to express reactions, emotions, or ideas visually.

#### Limitations

* This feature is only available for text-only posts. It will not work on image, video, or carousel posts.
* [GIPHY](https://developers.giphy.com/docs/api) is currently the only available GIF provider.

#### Publishing

GIFS can be attached when making an API call to the `POST /{threads-user-id}/threads` endpoint to [create a media container](https://developers.facebook.com/documentation/threads/posts#step-1--create-a-threads-media-container).

| Name | Description |
| --- | --- |
| `gif_attachment`<br><br>object | **Optional.**  <br>The ID and GIF provider for the GIF to attach to the post.<br><br>**Fields:** `gif_id`, `provider` |

##### Example request

```html
curl -i -X POST \
  -d "media_type=TEXT" \
  -d "text=<Text> \
  -d "access_token=<ACCESS_TOKEN>" \
  -d "gif_attachment={"gif_id":"<GIF_ID>","provider":"GIPHY"}" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

**Note:** The value of the `id` field you receive from the GIF provider's API response should be used as the `<GIF_ID>` in the API call.

##### Example response

```json
{
 "id": "<THREADS_MEDIA_ID>"
}
```

The request above creates a Threads media container that, once [published](https://developers.facebook.com/documentation/threads/posts#step-2--publish-a-threads-media-container), will attach a GIF to your media.

## Media Specifications

### Image Specifications

* **Format:** JPEG and PNG image types are the officially supported formats for image posts.
* **File Size:** 8 MB maximum.
* **Aspect Ratio Limit:** 10:1
* **Minimum Width:** 320 (will be scaled up to the minimum if necessary)
* **Maximum Width:** 1440 (will be scaled down to the maximum if necessary)
* **Height:** Varies (depending on width and aspect ratio)
* **Color Space:** sRGB. Images using other color spaces will have their color spaces converted to sRGB.

### Video Specifications

* **Container:** MOV or MP4 (MPEG-4 Part 14), no edit lists, moov atom at the front of the file.
* **Audio Codec:** AAC, 48khz sample rate maximum, 1 or 2 channels (mono or stereo).
* **Video Codec:** HEVC or H264, progressive scan, closed GOP, 4:2:0 chroma subsampling.
* **Frame Rate:** 23-60 FPS
* **Picture Size:**
    * Maximum Columns (horizontal pixels): 1920
    * Required aspect ratio is between 0.01:1 and 10:1 but we recommend 9:16 to avoid cropping or blank space.
* **Video Bitrate:** VBR, 100 Mbps maximum.
* **Audio Bitrate:** 128 kbps.
* **Duration:** 300 seconds (5 minutes) maximum, minimum longer than 0 seconds.
* **File Size:** 1 GB maximum.


## Learn more

* [Reposts](https://developers.facebook.com/documentation/threads/posts/reposts)
* [Quote Posts](https://developers.facebook.com/documentation/threads/posts/quote-posts)
* [Polls](https://developers.facebook.com/documentation/threads/create-posts/polls)
* [Spoilers](https://developers.facebook.com/documentation/threads/create-posts/spoilers)
* [Text Attachments](https://developers.facebook.com/documentation/threads/create-posts/text-attachments)