# Retrieve User Posts



This document shows you how to retrieve:

* [A list of all threads created by an app-scoped user](#retrieve-a-list-of-an-app-scoped-user-s-threads)
* [A list of all threads created by a public profile](#retrieve-a-list-of-a-public-profile-s-threads)
* [A single Threads media object](#retrieve-a-single-threads-media-object)
* [A list of all ghost posts created by an app-scoped user](#retrieve-a-list-of-an-app-scoped-user-s-ghost-posts)

**Note:** To retrieve posts that are replies, refer to [Retrieve User Replies](https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/retrieve-replies).

## Retrieve a list of an app-scoped user's Threads {#retrieve-a-list-of-an-app-scoped-user-s-threads}

Use the `GET /{threads-user-id}/threads` endpoint to return a paginated list of all threads created by a user.

### Permissions

The Threads Retrieval API requires an appropriate access token and permissions based on the node you are targeting. While you are testing, you can generate tokens and grant your app permissions by using the Graph API Explorer.

* `threads_basic` — Required for making any calls to all Threads API endpoints.

### Limitations

* You may only fetch a paginated list of all threads created by the app-scoped user.

### Fields
Here's a list of fields that can be returned for each Thread.

| Name | Description |
| --- | --- |
| `id` (default) | The media's ID. |
| `media_product_type` | Surface where the media is published. In the case of Threads, the value is `THREADS`. |
| `media_type` | The media type for a Threads post will be one of these values: `TEXT_POST`, `IMAGE`, `VIDEO`, `CAROUSEL_ALBUM`, `AUDIO`, or `REPOST_FACADE`.<br><br>**Note:** `media_type` will return `TEXT_POST` for posts containing GIFs and polls. |
| `media_url` | The post's media URL. |
| `permalink` | Permanent link to the post. Will be omitted if the media contains copyrighted material or has been flagged for a copyright violation. |
| `owner` | Threads user ID who created the post.  <br><br>**Note:** This is only available on top-level posts that you own. |
| `username` | Threads username who created the post. |
| `text` | Represents text for a Threads post. |
| `timestamp` | Post time. The publish date in ISO 8601 format. |
| `shortcode` | Shortcode of the media. |
| `thumbnail_url` | URL of thumbnail. This only shows up for Threads media with video. |
| `children` | List of child posts. This only shows up for carousel posts. |
| `is_quote_post` | Indicates if the media is a quoted post made by another user. |
| `quoted_post` | Media ID of the post that was quoted.  <br><br>**Note**: This only appears on quote posts. |
| `reposted_post` | Media ID of the post that was reposted.  <br><br>**Note**: This only appears on reposts. |
| `alt_text` | The accessibility text label or description for an image or video in a Threads post. |
| `link_attachment_url` | The URL attached to a Threads post. |
| `gif_url` | The URL of the GIF attached to the post (if any).  <br><br>**Note:** This will only show up on posts that have a GIF attachment. |
| `poll_attachment` | The poll attachment for the post.  <br><br>**Note:** This will only show up on posts that have a poll. |
| `topic_tag` | The topic tag in the post's header (if any).  <br><br>**Note:** This will only show up on posts that have a topic tag. |
| `is_spoiler_media` | Indicates if media objects were posted as spoilers. |
| `text_entities` | Indicates if spoilers are present in the text field of the posts. |
| `text_attachment` | The text attachment for the post. |
| `ghost_post_status` | The status of a ghost post.<br><br>**Values:**<br><br>* `ACTIVE` — An active ghost post.<br>* `ARCHIVED` — An expired ghost post.<br><br>**Note:** This will only show for posts that are ghost posts. |
| `ghost_post_expiration_timestamp` | Timestamp of when the post will or has expired in ISO 8601 format.<br><br>**Note:** This will only show for posts that are ghost posts. |
| `is_verified` | Returns `true` if the post author's profile is verified on Threads. |
| `profile_picture_url` | Returns the URL of the post author's profile picture on Threads. |

### Example request

```html
curl -s -X GET \
"https://graph.threads.com/v1.0/me/threads?fields=id,media_product_type,media_type,media_url,permalink,owner,username,text,topic_tag,timestamp,shortcode,thumbnail_url,children,is_quote_post&since=2023-10-15&until=2023-11-18&limit=1&access_token=<ACCESS_TOKEN>"
```

### Example response

```json
{
  "data": [
    {
      "id": "1234567",
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "permalink": "https://www.threads.com/@threadsapitestuser/post/abcdefg",
      "owner": {
        "id": "1234567"
      },
      "username": "threadsapitestuser",
      "text": "Today Is Monday",
      "topic_tag": "Mondays",
      "timestamp": "2023-10-17T05:42:03+0000",
      "shortcode": "abcdefg",
      "is_quote_post": false
    },
  ],
  "paging": {
    "cursors": {
      "before": "BEFORE_CURSOR",
      "after": "AFTER_CURSOR"
    }
  }
}
```

## Retrieve a list of a public profile's Threads {#retrieve-a-list-of-a-public-profile-s-threads}

Use the `GET /profile_posts?username=...` endpoint to look up a public profile and retrieve a paginated list of their posts on Threads.

### Permissions

The Threads Profile Discovery API requires an appropriate access token and permissions based on the node you are targeting. While you are testing, you can generate tokens and grant your app permissions by using the Graph API Explorer.

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_profile_discovery` — Required for making any calls to all Threads Profile Discovery API endpoints.

With [standard access](https://developers.facebook.com/documentation/development/graph-api/overview/access-levels), only posts from some of the official Meta accounts can be retrieved. These include @meta, @threads, @instagram, and @facebook.

### Limitations

* Only returns public profiles with at least 100 followers.
* A user can send a maximum of 1,000 requests within a rolling 24-hour period. Once a query is sent, it will count against this limit for 24 hours.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `username`<br><br>string | **Required.**  <br>Unique username on Threads. Must be an exact match. |

### Fields

The same fields as those for an [app-scoped user's posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts#fields) can be retrieved except for the `owner` field.

### Example request

```html
curl -i -X GET \
  "https://graph.threads.com/v1.0/profile_posts?access_token=<THREADS_TESTER_ACCESS_TOKEN>&username=<THREADS_USERNAME>&fields=id,media_product_type,media_type,media_url,permalink,username,text,topic_tag,timestamp,shortcode,thumbnail_url,children,is_quote_post&since=2023-10-15&until=2023-11-18&limit=1"
```

### Example response

```json
{
  "data": [
    {
      "id": "1234567",
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "permalink": "https://www.threads.com/@meta/post/abcdefg",
      "username": "meta",
      "text": "Today Is Monday",
      "topic_tag": "Mondays",
      "timestamp": "2023-10-17T05:42:03+0000",
      "shortcode": "abcdefg",
      "is_quote_post": true
    },
  ],
  "paging": {
    "cursors": {
      "before": "BEFORE_CURSOR",
      "after": "AFTER_CURSOR"
    }
  }
}
```

## Retrieve a single Threads media object

You can also use the `GET /{threads-media-id}` endpoint to return a single Threads media object.

### Permissions

The Threads Retrieval API requires an appropriate access token and permissions based on the node you are targeting. While you are testing, you can generate tokens and grant your app permissions by using the Graph API Explorer.

* `threads_basic` — Required for making any calls to all Threads API endpoints.

If your app has not been approved for [advanced access](https://developers.facebook.com/documentation/development/graph-api/overview/access-levels) for the `threads_basic` permission, only posts created by a Threads tester are retrievable. After approval, public posts created by other users will be retrievable.

### Fields

The same fields as those for an [app-scoped user's posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts#fields) can be retrieved.

### Example request

```html
curl -s -X GET \
"https://graph.threads.com/v1.0/<THREADS_MEDIA_ID>?fields=id,media_product_type,media_type,media_url,permalink,owner,username,text,topic_tag,timestamp,shortcode,thumbnail_url,children,is_quote_post&access_token=<ACCESS_TOKEN>"
```

### Example response

```json
{
  "id": "1234567",
  "media_product_type": "THREADS",
  "media_type": "TEXT_POST",
  "permalink": "https://www.threads.com/@threadsapitestuser/post/abcdefg",
  "owner": {
    "id": "1234567"
  },
  "username": "meta",
  "text": "Today Is Monday",
  "topic_tag": "Mondays",
  "timestamp": "2023-10-09T23:18:27+0000",
  "shortcode": "abcdefg",
  "is_quote_post": false
}
```

## Retrieve a list of an app-scoped user's ghost posts {#retrieve-a-list-of-an-app-scoped-user-s-ghost-posts}

Use the `GET /{threads-user-id}/ghost_posts` endpoint to return a paginated list of all ghost post threads created by an app-scoped user.

To create a ghost post, see [Create Ghost Posts](https://developers.facebook.com/documentation/threads/create-posts/ghost-posts) for more information.

### Permissions

The Threads Ghost Posts API requires an appropriate access token and permissions based on the node you are targeting. While you are testing, you can easily generate tokens and grant your app permissions by using the [Graph API Explorer](https://developers.facebook.com/tools/explorer/).

* `threads_basic` — Required for making any calls to all Threads API endpoints.

If your app has not been approved for advanced access for the `threads_basic` permission, only posts created by a Threads tester are retrievable. After approval, public posts created by other users will be retrievable.

### Fields

The same fields as those for an [app-scoped user's posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts#fields) can be retrieved.

### Example request

```html
curl -GET \
  -d "fields=id,media_product_type,media_type,media_url,permalink,owner,username,text,timestamp,shortcode,thumbnail_url,ghost_post_status,ghost_post_expiration_timestamp" \
  -d "since=<START_DATE>" \
  -d "until=<END_DATE>" \
  -d "limit=1" \
  -d "access_token=<ACCESS_TOKEN>"
"https://graph.threads.com/v1.0/me/ghost_posts"
```

### Example response

```json
{
  "data": [
    {
      "id": "<MEDIA_ID>",
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "permalink": "https://www.threads.com/<THREADS_USERNAME>/post/<POST_ID>",
      "owner": {
        "id": "<THREADS_USER_ID>"
      },
      "username": "<THREADS_USERNAME>",
      "text": "<TEXT>",
      "timestamp": "<TIMESTAMP>",
      "shortcode": "<MEDIA_SHORTCODE>",
      "ghost_post_status": "ARCHIVED",
      "ghost_post_expiration_timestamp": "<EXPIRATION_TIMESTAMP>"
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