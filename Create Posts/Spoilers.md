# Spoilers



You can create posts with spoilers using the Threads API. Spoilers can be added to text in a post or can be used with media types like images and videos.

This document covers:

* [Text and Media Spoilers](#text-and-media-spoilers)
* [Single Threads Posts with Spoilers](#single-threads-posts)
* [Carousel Posts with Spoilers](#threads-carousel-posts)

## Permissions

Publishing posts with spoilers requires the following permissions:

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_content_publish` — Required for Threads publishing endpoints only.

If your app has not been approved for advanced access for the `threads_content_publish` permission, you can only post on behalf of [Threads testers](https://developers.facebook.com/documentation/threads/get-started#threads-testers) on your app. After your app is published and approved, you can post on behalf of any Threads user who grants your app the permission.

### Limitations

* Media spoilers only work with a `media_type` of `IMAGE`, `VIDEO`, or `CAROUSEL`.
* The maximum number of text spoiler entities per post is limited to 10.

## Text and media spoilers

### Create a spoiler within a text field

To create a text post with a spoiler, use the `text_entities` parameter. This parameter takes a list of `entity_type`, `offset`, and `length` values. Each entry represents part of the text post where the API applies the spoiler.

#### Parameters

| Name | Description |
| --- | --- |
| `entity_type`<br><br>string | Indicates the kind of `entity_type`.<br><br>**Values:** `SPOILER`, `spoiler` |
| `offset`<br><br>int | The starting position of the spoiler.<br><br>**Values:** Positive whole numbers, such as 1 and 2. |
| `length`<br><br>int | The length of the spoiler text starting from the `offset` position.<br><br>**Values:** Positive whole numbers, such as 1 and 2. |

### Create a media spoiler

To create a post with spoilers for media objects such as an image or video, use the `is_spoiler_media` parameter.

#### Parameters

| Name | Description |
| --- | --- |
| `is_spoiler_media`<br><br>Boolean | Indicates if the media should be a spoiler or not.<br><br>**Values:** `true`, `false` |

## Single Threads posts

### Step 1: Create a Threads media container

Spoilers for single Threads posts need to be provided during the [Threads media container creation phase](https://developers.facebook.com/documentation/threads/posts#step-1--create-a-threads-media-container).

* If a spoiler needs to be added in the text field of the post, use the `text_entities` parameter.
* If a spoiler needs to be added to the media object in the post, use the `is_spoiler_media` parameter.
* If a spoiler needs to be added to the text and media objects in the post, use both the `text_entities` and `is_spoiler_media` parameters.

#### Example requests

##### Spoiler only in the text field

```bash
curl -i -X POST \
  -d "access_token=<ACCESS_TOKEN>" \
  -d "media_type=TEXT" \
  -d "text=<TEXT>" \
  -d "text_entities=[
    {
      "entity_type": "SPOILER",
      "offset": 0,
      "length": 2
    },
    {
      "entity_type": "SPOILER",
      "offset": 2,
      "length": 7
    }
  ]" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

##### Spoiler only for a media object (image/video)

```bash
curl -i -X POST \
  -d "access_token=<ACCESS_TOKEN>" \
  -d "media_type=IMAGE" \
  -d "image_url=<IMAGE_URL>" \
  -d "text=<TEXT>" \
  -d "is_spoiler_media=true" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

##### Spoiler for both text and a media object (image/video)

```bash
curl -i -X POST \
  -d "access_token=<ACCESS_TOKEN>" \
  -d "media_type=IMAGE" \
  -d "image_url=<IMAGE_URL>" \
  -d "text=<TEXT>" \
  -d "is_spoiler_media=true" \
  -d "text_entities=[
    {
      "entity_type": "SPOILER",
      "offset": 0,
      "length": 2
    },
    {
      "entity_type": "SPOILER",
      "offset": 2,
      "length": 7
    }
  ]" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

#### Response

If the API call is successful, the Threads media container ID will be returned.

### Step 2: Publish the Threads media container

You can now [publish](https://developers.facebook.com/documentation/threads/posts#step-2--publish-a-threads-media-container) using the returned Threads media container ID to create your single Threads post with spoilers.

## Threads carousel posts

### Step 1: Create a Threads media container

[Create a Threads media container](https://developers.facebook.com/documentation/threads/posts#step-1-create-an-media-container) for each of the items to be included in the carousel.

### Step 2: Create the carousel container

Spoilers for Threads carousel posts need to be provided during the [carousel container creation phase](https://developers.facebook.com/documentation/threads/posts#step-2-create-a-carousel-container).

* If a spoiler needs to be added in the text field of the post, use the `text_entities` parameter.
* If a spoiler needs to be added to the media object in the post, use the `is_spoiler_media` parameter.
* If a spoiler needs to be added to the text and media objects in the post, use both the `text_entities` and `is_spoiler_media` parameters.

**Note:** If `is_spoiler_media` is set to `true` all attached media such as images and videos will be marked as spoilers.

#### Example requests

##### Spoiler only in the text field

```bash
curl -i -X POST \
  -d "access_token=<ACCESS_TOKEN>" \
  -d "media_type=CAROUSEL" \
  -d "children=<MEDIA_ID_1>,<MEDIA_ID_2>,<MEDIA_ID_3>" \
  -d "text=<TEXT>" \
  -d "text_entities=[
    {
      "entity_type": "SPOILER",
      "text": "spoiler",
      "offset": 0,
      "length": 2
    },
    {
      "entity_type": "SPOILER",
      "text": "spoiler",
      "offset": 2,
      "length": 7
    }
  ]" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

##### Spoiler only for a media object (image/video)

```bash
curl -i -X POST \
  -d "access_token=<ACCESS_TOKEN>" \
  -d "media_type=CAROUSEL" \
  -d "children=<MEDIA_ID_1>,<MEDIA_ID_2>,<MEDIA_ID_3>" \
  -d "is_spoiler_media=true" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

##### Spoiler for both text and a media object (image/video)

```bash
curl -i -X POST \
  -d "access_token=<ACCESS_TOKEN>" \
  -d "media_type=CAROUSEL" \
  -d "children=<MEDIA_ID_1>,<MEDIA_ID_2>,<MEDIA_ID_3>" \
  -d "text=<TEXT>" \
  -d "is_spoiler_media=true" \
  -d "text_entities=[
    {
      "entity_type": "SPOILER",
      "text": "spoiler",
      "offset": 0,
      "length": 2
    },
    {
      "entity_type": "SPOILER",
      "text": "spoiler",
      "offset": 2,
      "length": 7
    }
  ]" \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

#### Response

If the API call is successful, the Threads media container ID will be returned.

### Step 3: Publish the Threads media container

You can now [publish](https://developers.facebook.com/documentation/threads/posts#step-2--publish-a-threads-media-container) using the returned Threads media container ID to create your Threads carousel post with spoilers.

## Learn more

* [Posts](https://developers.facebook.com/documentation/threads/posts)
* [Retrieve User Posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts)