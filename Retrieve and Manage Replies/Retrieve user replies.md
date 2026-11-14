# Retrieve user replies



You can retrieve a list of a user's replies.

## Retrieve a list of a user's replies

Use the `GET /{threads-user-id}/replies` endpoint to return a paginated list of all replies created by a user.

### Fields

Here is a list of fields that can be returned for each reply.

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
| `reply_audience` | Who can reply to your post.  <br>**Values:** `EVERYONE`, `ACCOUNTS_YOU_FOLLOW`, `MENTIONED_ONLY`, `PARENT_POST_AUTHOR_ONLY`, `FOLLOWERS_ONLY`  <br>**Note:** This only appears on top-level posts and replies that you own. |
| `gif_url` | The URL of the GIF attached to the post (if any).  <br>**Note:** This only appears on posts that have a GIF attachment. |
| `poll_attachment` | The poll attachment for the post.  <br>**Note:** This only appears on posts that have a poll. |
| `topic_tag` | The topic tag for the post (if any).  <br>**Note:** This only appears on posts that have a topic tag. |
| `is_verified` | Whether the post author's profile is verified on Threads. |
| `profile_picture_url` | Returns the URL of the post author's profile picture on Threads. |

#### Example request

```bash
curl -s -X GET \
  "https://graph.threads.com/v1.0/me/replies?fields=id,media_product_type,media_type,media_url,permalink,username,text,topic_tag,timestamp,shortcode,thumbnail_url,children,is_quote_post,has_replies,root_post,replied_to,is_reply,is_reply_owned_by_me,reply_audience&since=2023-10-15&until=2023-11-18&limit=1&access_token=<ACCESS_TOKEN>"
```

#### Example response

```json
{
  "data": [
    {
      "id": "1234567",
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "permalink": "https://www.threads.com/@threadsapitestuser/post/abcdefg",
      "username": "threadsapitestuser",
      "text": "Reply Text",
      "topic_tag": "Reply Topic",
      "timestamp": "2023-10-17T05:42:03+0000",
      "shortcode": "abcdefg",
      "is_quote_post": false,
      "has_replies": false,
      "root_post": {
        "id": "1234567890"
      },
      "replied_to": {
        "id": "1234567890"
      },
      "is_reply": true,
      "is_reply_owned_by_me": true,
      "reply_audience": "EVERYONE"
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