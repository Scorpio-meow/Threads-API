# Publish with the Threads API



The Threads publishing endpoints allow you to upload and publish Threads media objects and check their status. See [Post to Threads](https://developers.facebook.com/documentation/threads/posts) for more information.

## `POST /{threads-user-id}/threads`
Upload media and create media containers. See [Posts](https://developers.facebook.com/documentation/threads/posts) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `threads-user-id`<br><br>string | **Required.**  <br>The path parameter of the Threads user identifier. |
| `media_type`<br><br>string | **Required.**  <br>**Values:** `TEXT`, `IMAGE`, `VIDEO`, `CAROUSEL` |
| `text`<br><br>string | **Optional.**  <br>The text associated with the post. Uses [UTF-8 encoding](https://www.npmjs.com/package/grapheme-splitter). For text-only posts, this parameter is **required**.<br><br>**Note:** For the post character limit, emojis are counted as the number of UTF-8 bytes. |
| `image_url`<br><br>string | **Optional.**  <br>Required if `media_type=IMAGE`. |
| `video_url`<br><br>string | **Optional.**  <br>Required if `media_type=VIDEO`. |
| `is_carousel_item`<br><br>Boolean | **Optional.**  <br>**Values:** `true`, `false` (default) |
| `children`<br><br>array | **Optional.**  <br>Required if `media_type=CAROUSEL`. |
| `reply_to_id`<br><br>string | **Optional.**  <br>Required if replying to a post. |
| `reply_control`<br><br>string | **Optional.**  <br>Can be used to specify who can reply to a post.  <br>**Values:** `everyone`, `accounts_you_follow`, `mentioned_only`, `parent_post_author_only`, `followers_only` |
| `allowlisted_country_codes`<br><br>list<string> | **Optional.**  <br>A string list of valid [ISO 3166-1 alpha-2 country codes](https://www.iso.org/obp/ui/#search) that represents the countries where this media should be shown. If this parameter is passed in, the media will not be shown to Threads profiles in countries outside of this list. |
| `alt_text`<br><br>string | **Optional.**  <br>The accessibility text label or description for an image or video in a Threads post.  <br>**Note:** The maximum length of `alt_text` is 1,000 characters. |
| `link_attachment`<br><br>string | **Optional.**  <br>The URL attached to a Threads post. |
| `quote_post_id`<br><br>string | **Optional.**  <br>ID of the post to quote. |
| `poll_attachment`<br><br>object | **Optional.**  <br>The options for a post with a poll attachment. |
| `auto_publish_text`<br><br>Boolean | **Optional.**  <br>When this optional flag is passed, a Threads post is published automatically when a Threads [media container](https://developers.facebook.com/documentation/threads/posts#step-1--create-a-threads-media-container) is created without needing to go through the extra [publish step](https://developers.facebook.com/documentation/threads/posts#step-2--publish-a-threads-media-container).  <br>**Note:** This only works for text posts. |
| `topic_tag`<br><br>string | **Optional.**  <br>The topic to add to a post.  <br>**Note:** The following characters are not allowed in topic tags:<br><br>* Periods (.)<br>* Ampersands (&) |
| `is_spoiler_media`<br><br>Boolean | **Optional.**  <br>Indicates if the media should be a spoiler or not.<br><br>**Values:** `true`, `false` |
| `text_entities`<br><br>object | **Optional.**  <br>The spoiler settings for the post. |
| `text_attachment`<br><br>object | **Optional.**  <br>The text attachment for the post. |
| `gif_attachment`<br><br>object | **Optional.**  <br>The ID and GIF provider for the GIF to attach to the post.<br><br>**Fields:** `gif_id`, `provider` |
| `is_ghost_post`<br><br>Boolean | **Optional.**  <br>Indicates if the post is a ghost post or not.<br><br>**Values:** `true`, `false` |
| `enable_reply_approvals`<br><br>Boolean | **Optional.**  <br>Indicates if the post should have reply approvals enabled.<br><br>**Values:** `true`, `false` |
| `crossreshare_to_ig`<br><br>Boolean | **Optional.**  <br>Cross-shares a Threads post to a linked Instagram account as a Story when set to `true`.  <br>**Values:** `true`, `false` (*default*) |
| `crossreshare_to_ig_dark_mode`<br><br>Boolean | **Optional.**  <br>Cross-shares a Threads post to a linked Instagram account as a Story in dark mode when set to `true`.  <br>**Values:** `true`, `false` (*default*) |
| `location_id`<br><br>string | **Optional.**  <br>The ID of the location to tag.  <br>**Note:** Use the [`GET /location_search`](https://developers.facebook.com/documentation/threads/reference/location-search) endpoint to find location IDs. |

## `POST /{threads-user-id}/threads_publish`
Publish uploaded media using their media containers. See [Posts](https://developers.facebook.com/documentation/threads/posts) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `threads-user-id`<br><br>string | **Required.**  <br>The path parameter of the Threads user identifier. |
| `creation_id`<br><br>string | **Required.**  <br>Identifier of the Threads media container. |

## `GET /{threads-container-id}?fields=status`
Check the Threads media container publishing eligibility and status.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `threads-container-id`<br><br>string | **Required.**  <br>The path parameter of the Threads media container identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `id` *(default)*, `status` *(default)*, `error_message` |

## `POST /{threads-media-id}/repost`

Repost a Threads post that was previously published. See [Reposts](https://developers.facebook.com/documentation/threads/posts/reposts) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `threads-media-id`<br><br>string | **Required.**  <br>The path parameter of the Threads media identifier. |

## `DELETE /{threads-media-id}`

Delete a Threads post. See [Delete Posts](https://developers.facebook.com/documentation/threads/posts/delete-posts) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `threads-media-id`<br><br>string | **Required.**  <br>The path parameter of the Threads media identifier. |