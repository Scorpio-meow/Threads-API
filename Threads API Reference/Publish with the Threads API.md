# Publish with the Threads API



The Threads publishing endpoints allow you to upload and publish Threads media objects, check their status, and repost and delete posts. See [Post to Threads](https://developers.facebook.com/documentation/threads/posts) for more information.

## Common parameters

These parameters work the same way on every endpoint on this page that uses them. Each endpoint lists the ones it uses.

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads API user access token. |

## `POST /{threads-user-id}/threads`

Upload media and create media containers. See [Posts](https://developers.facebook.com/documentation/threads/posts) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`.

| Name | Description |
| --- | --- |
| `threads-user-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads user identifier. |
| `media_type`<br><br>string | **Required.**  <br>The type of media container to create.  <br>**Values:** `TEXT`, `IMAGE`, `VIDEO`, `CAROUSEL` |
| `text`<br><br>string | **Optional.**  <br>The text associated with the post. Uses [UTF-8 encoding](https://www.npmjs.com/package/grapheme-splitter). Required for text-only posts.<br><br>**Note:** For the post character limit, emojis are counted as the number of UTF-8 bytes. |
| `image_url`<br><br>URL string | **Optional.**  <br>The public URL of the image. Required if `media_type=IMAGE`. |
| `video_url`<br><br>URL string | **Optional.**  <br>The public URL of the video. Required if `media_type=VIDEO`. |
| `is_made_with_ai`<br><br>Boolean | **Optional.**  <br>Set to `true` to disclose that a post contains AI-generated content and display the AI info label. Supported for `TEXT`, `IMAGE`, `VIDEO`, and `CAROUSEL` posts.<br><br>**Values:** `true`, `false` *(default)*<br><br>Set this parameter when creating the media container, not when calling `POST /{threads-user-id}/threads_publish`. For carousels, set it on the parent container. Setting `is_made_with_ai=true` on an individual carousel item (`is_carousel_item=true`) returns an error.<br><br>Omitting this parameter or setting it to `false` does not add an AI self-disclosure. It does not prevent automatic AI labeling. See [Label AI-generated content](https://developers.facebook.com/documentation/threads/posts#label-ai-generated-content) for an example. |
| `is_carousel_item`<br><br>Boolean | **Optional.**  <br>Set to `true` if this container is an item in a carousel.  <br>**Values:** `true`, `false` *(default)* |
| `children`<br><br>list of numeric strings | **Optional.**  <br>A comma-separated list of the media container IDs of the carousel items. Required if `media_type=CAROUSEL`. |
| `reply_to_id`<br><br>numeric string | **Optional.**  <br>The ID of the post to reply to. Required if replying to a post. |
| `reply_control`<br><br>string | **Optional.**  <br>Specifies who can reply to the post.  <br>**Values:** `everyone`, `accounts_you_follow`, `mentioned_only`, `parent_post_author_only`, `followers_only` |
| `allowlisted_country_codes`<br><br>list of strings | **Optional.**  <br>A list of valid [ISO 3166-1 alpha-2 country codes](https://www.iso.org/obp/ui/#search) that represents the countries where this media should be shown. If this parameter is passed in, the media is not shown to Threads profiles in countries outside of this list. |
| `alt_text`<br><br>string | **Optional.**  <br>The accessibility text label or description for an image or video in a Threads post.  <br>**Note:** The maximum length of `alt_text` is 1,000 characters. |
| `link_attachment`<br><br>URL string | **Optional.**  <br>The URL attached to a Threads post. |
| `quote_post_id`<br><br>numeric string | **Optional.**  <br>ID of the post to quote. |
| `poll_attachment`<br><br>object | **Optional.**  <br>The options for a post with a poll attachment. |
| `auto_publish_text`<br><br>Boolean | **Optional.**  <br>When set to `true`, a Threads post is published automatically when a Threads [media container](https://developers.facebook.com/documentation/threads/posts#step-1-create-a-threads-media-container) is created without needing to go through the extra [publish step](https://developers.facebook.com/documentation/threads/posts#step-2-publish-the-threads-media-container).  <br>**Note:** This only works for text posts. |
| `topic_tag`<br><br>string | **Optional.**  <br>The topic to add to a post.  <br>**Note:** The following characters are not allowed in topic tags:<br><br>* Periods (.)<br>* Ampersands (&) |
| `is_spoiler_media`<br><br>Boolean | **Optional.**  <br>Whether the media should be a spoiler.<br><br>**Values:** `true`, `false` |
| `text_entities`<br><br>object | **Optional.**  <br>The spoiler settings for the post. |
| `text_attachment`<br><br>object | **Optional.**  <br>The text attachment for the post. |
| `gif_attachment`<br><br>object | **Optional.**  <br>The ID and GIF provider for the GIF to attach to the post.<br><br>**Fields:** `gif_id`, `provider` |
| `is_ghost_post`<br><br>Boolean | **Optional.**  <br>Whether the post is a ghost post.<br><br>**Values:** `true`, `false` |
| `enable_reply_approvals`<br><br>Boolean | **Optional.**  <br>Whether the post should have reply approvals enabled.<br><br>**Values:** `true`, `false` |
| `crossreshare_to_ig`<br><br>Boolean | **Optional.**  <br>Cross-shares a Threads post to a linked Instagram account as a Story when set to `true`.  <br>**Values:** `true`, `false` *(default)* |
| `crossreshare_to_ig_dark_mode`<br><br>Boolean | **Optional.**  <br>Cross-shares a Threads post to a linked Instagram account as a Story in dark mode when set to `true`.  <br>**Values:** `true`, `false` *(default)* |
| `location_id`<br><br>numeric string | **Optional.**  <br>The ID of the location to tag.  <br>**Note:** Use the [`GET /location_search`](https://developers.facebook.com/documentation/threads/reference/location-search) endpoint to find location IDs. |

## `POST /{threads-user-id}/threads_publish`

Publish uploaded media using their media containers. See [Posts](https://developers.facebook.com/documentation/threads/posts) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`.

| Name | Description |
| --- | --- |
| `threads-user-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads user identifier. |
| `creation_id`<br><br>numeric string | **Required.**  <br>Identifier of the Threads media container. |

## `GET /{threads-container-id}?fields=status`

Check the Threads media container publishing eligibility and status.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`.

| Name | Description |
| --- | --- |
| `threads-container-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads media container identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `id` *(default)*, `status` *(default)*, `error_message` |

## `POST /{threads-media-id}/repost`

Repost a Threads post that was previously published. See [Reposts](https://developers.facebook.com/documentation/threads/posts/reposts) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`.

| Name | Description |
| --- | --- |
| `threads-media-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads media identifier. |

## `DELETE /{threads-media-id}`

Delete a Threads post. See [Delete posts](https://developers.facebook.com/documentation/threads/posts/delete-posts) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`.

| Name | Description |
| --- | --- |
| `threads-media-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads media identifier. |