# Retrieve media replies and conversations



There are two ways of retrieving a thread's replies: `GET /{threads-media-id}/replies` and `GET /{threads-media-id}/conversation`.

`GET /{threads-media-id}/replies` only returns the top-level replies under the Threads media ID provided in the request, while `GET /{threads-media-id}/conversation` returns all replies, regardless of the depth, either in chronological or reverse chronological order.

## Parameters
These parameters are for both `GET /{threads-media-id}/replies` and `GET /{threads-media-id}/conversation`.

| Name | Description |
| --- | --- |
| `reverse`<br><br>Boolean | **Optional.**  <br>Whether to sort replies in reverse chronological order.  <br>**Values:** `true` *(default)*, `false` |

## Fields
These fields are for both `GET /{threads-media-id}/replies` and `GET /{threads-media-id}/conversation`.

| Name | Description |
| --- | --- |
| `id` *(default)* | The media's ID. |
| `text` | Represents text for a Threads reply. This is optional on image, video, and carousel replies. |
| `username` | Username of the Threads user who created the post.  <br>**Note:** This only works for public users and your own user. |
| `permalink` | Permanent link to the post. Omitted if the media contains copyrighted material or has been flagged for a copyright violation.  <br>**Note:** This only works for public users and your own user. |
| `timestamp` | The publish date and time of the post in ISO 8601 format. |
| `media_product_type` | Surface where the media is published. In the case of Threads, the value is `THREADS`. |
| `media_type` | The media type for a Threads reply is one of these values: `TEXT_POST`, `IMAGE`, `VIDEO`, `CAROUSEL_ALBUM`, or `AUDIO`. |
| `media_url` | The post's media URL. This only shows for image, video, and carousel replies. |
| `shortcode` | Shortcode of the media. |
| `thumbnail_url` | URL of thumbnail. This only shows for Threads replies with video. |
| `children` | List of child posts. This only shows for carousel replies. |
| `is_quote_post` | Whether the media is a quote reply made by another user. |
| `quoted_post` | Media ID of the post that was quoted.  <br>**Note:** This only appears on quote posts. |
| `has_replies` | Whether the Threads post or reply has replies that you can see. |
| `root_post` | Media ID of the top-level post or original thread in the reply tree.  <br>**Note:** This only appears on replies. |
| `replied_to` | Media ID of the immediate parent of the reply.  <br>**Note:** This only appears on replies. |
| `is_reply` | Whether the Threads media is a reply rather than a top-level post. |
| `is_reply_owned_by_me` | Whether your user owns the Threads reply.  <br>**Note:** This only appears on replies. |
| `hide_status` | Whether the reply is hidden.  <br>**Values:** `NOT_HUSHED`, `UNHUSHED`, `HIDDEN`, `COVERED`, `BLOCKED`, `RESTRICTED`  <br>**Note:** This only appears on replies. |
| `reply_audience` | Who can reply to your post.  <br>**Values:** `EVERYONE`, `ACCOUNTS_YOU_FOLLOW`, `MENTIONED_ONLY`, `PARENT_POST_AUTHOR_ONLY`, `FOLLOWERS_ONLY`  <br>**Note:** This only appears on top-level posts and replies that you own. |
| `gif_url` | The URL of the GIF attached to the post (if any).  <br>**Note:** This only appears on posts that have a GIF attachment. |
| `poll_attachment` | The poll attachment for the post.  <br>**Note:** This only appears on posts that have a poll. |
| `topic_tag` | The topic tag for the post (if any).  <br>**Note:** This only appears on posts that have a topic tag. |
| `is_verified` | Whether the post author's profile is verified on Threads.  <br>**Note:** Only available on direct replies. |
| `profile_picture_url` | Returns the URL of the post author's profile picture on Threads.  <br>**Note:** Only available on direct replies. |

## A thread's replies

Use `GET /{threads-media-id}/replies` to fetch a paginated list of all top-level replies.

This endpoint is applicable to the use cases that focus on the depth level of the replies. The endpoint returns the immediate replies of the requested Threads media ID. `has_replies` indicates whether a post has nested replies or not and the field can be used to decide to chain subsequent `GET` calls to retrieve replies located in the deeper levels.

### Example request

```bash
curl -s -X GET \
  "https://graph.threads.com/v1.0/<MEDIA_ID>/replies?fields=id,text,topic_tag,timestamp,media_product_type,media_type,media_url,shortcode,thumbnail_url,children,has_replies,root_post,replied_to,is_reply,hide_status&reverse=false&access_token=<ACCESS_TOKEN>"
```

### Example response

```json
{
  "data": [
    {
      "id": "1234567890",
      "text": "First Reply",
      "topic_tag": "First Topic",
      "timestamp": "2024-01-01T18:20:00+0000",
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "shortcode": "abcdefg",
      "has_replies": true,
      "root_post": {
        "id": "1234567890"
      },
      "replied_to": {
        "id": "1234567890"
      },
      "is_reply": true,
      "hide_status": "NOT_HUSHED"
    },
    {
      "id": "1234567890",
      "text": "Second Reply",
      "topic_tag": "Second Topic",
      "timestamp": "2024-01-01T18:20:00+0000",
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "shortcode": "abcdefg",
      "has_replies": false,
      "root_post": {
        "id": "1234567890"
      },
      "replied_to": {
        "id": "1234567890"
      },
      "is_reply": true,
      "hide_status": "HIDDEN"
    },
    {
      "id": "1234567890",
      "text": "Third Reply",
      "topic_tag": "Third Topic",
      "timestamp": "2024-01-01T18:20:00+0000",
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "shortcode": "abcdefg",
      "has_replies": false,
      "root_post": {
        "id": "1234567890"
      },
      "replied_to": {
        "id": "1234567890"
      },
      "is_reply": true,
      "hide_status": "UNHUSHED"
    }
  ],
  "paging": {
    "cursors": {
      "before": "BEFORE_CURSOR",
      "after": "AFTER_CURSOR"
    }
  }
}
```

## A thread's conversations

Use `GET /{threads-media-id}/conversation` to fetch a paginated and flattened list of all top-level and nested replies.

This endpoint is applicable to specific use cases that do not focus on the knowledge of the depth of the replies.

**Note:** This endpoint is only intended to be used on root-level posts that have replies.

### Example request

```bash
curl -s -X GET \
  "https://graph.threads.com/v1.0/<MEDIA_ID>/conversation?fields=id,text,timestamp,media_product_type,media_type,media_url,shortcode,thumbnail_url,children,has_replies,root_post,replied_to,is_reply,hide_status&reverse=false&access_token=<ACCESS_TOKEN>"
```

### Example response

```json
{
  "data": [
    {
      "id": "1234567890",
      "text": "First Reply",
      "topic_tag": "First Topic",
      "timestamp": "2024-01-01T18:20:00+0000",
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "shortcode": "abcdefg",
      "has_replies": true,
      "root_post": {
        "id": "1234567890"
      },
      "replied_to": {
        "id": "1234567890"
      },
      "is_reply": true,
      "hide_status": "NOT_HUSHED"
    },
    {
      "id": "1234567890",
      "text": "Second Reply",
      "topic_tag": "Second Topic",
      "timestamp": "2024-01-01T18:20:00+0000",
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "shortcode": "abcdefg",
      "has_replies": false,
      "root_post": {
        "id": "1234567890"
      },
      "replied_to": {
        "id": "1234567890"
      },
      "is_reply": true,
      "hide_status": "HIDDEN"
    },
    {
      "id": "1234567890",
      "text": "Third Reply",
      "topic_tag": "Third Topic",
      "timestamp": "2024-01-01T18:20:00+0000",
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "shortcode": "abcdefg",
      "has_replies": false,
      "root_post": {
        "id": "1234567890"
      },
      "replied_to": {
        "id": "1234567890"
      },
      "is_reply": true,
      "hide_status": "UNHUSHED"
    },
    {
      "id": "1234567890",
      "text": "Nested Reply",
      "topic_tag": "Nested Topic",
      "timestamp": "2024-01-01T18:20:00+0000",
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "shortcode": "abcdefg",
      "has_replies": false,
      "root_post": {
        "id": "1234567890"
      },
      "replied_to": {
        "id": "1234567890"
      },
      "is_reply": true,
      "hide_status": "NOT_HUSHED"
    }
  ],
  "paging": {
    "cursors": {
      "before": "BEFORE_CURSOR",
      "after": "AFTER_CURSOR"
    }
  }
}
```