# Reply management (reference) - Threads API



The Threads reply management endpoints allow you to retrieve replies and conversations and hide/unhide replies. See [Threads Reply Management API](https://developers.facebook.com/documentation/threads/reply-management) for more information.

## `GET /{threads-media-id}/replies`

Retrieve a paginated list of all top-level replies for a Threads media object. See [Replies](https://developers.facebook.com/documentation/threads/reply-management#replies) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `threads-media-id`<br><br>string | **Required.**  <br>The path parameter of the Threads media identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to return.  <br>**Values:** `id` *(default)*, `media_product_type`, `media_type`, `media_url`, `permalink`, `username`, `text`, `timestamp`, `shortcode`, `thumbnail_url`, `children`, `is_quote_post`, `has_replies`, `root_post`, `replied_to`, `is_reply`, `is_reply_owned_by_me`, `hide_status`, `reply_audience`, `quoted_post`, `reposted_post`, `gif_url`, `topic_tag`, `is_verified`, `profile_picture_url` |
| `reverse`<br><br>Boolean | **Optional.**  <br>Whether replies should be sorted. Sorts replies in reverse chronological order.  <br>**Values:** `true` *(default)*, `false` |
| `before` | **Optional.**  <br>A cursor for pagination. Both `before` and `after` parameters cannot be passed at the same time. |
| `after` | **Optional.**  <br>A cursor for pagination. Both `before` and `after` parameters cannot be passed at the same time. |

## `GET /{threads-media-id}/conversation`
Retrieve a paginated and flattened list of all top-level and nested replies for a Threads media object. See [Conversations](https://developers.facebook.com/documentation/threads/reply-management#conversations) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `threads-media-id`<br><br>string | **Required.**  <br>The path parameter of the Threads media identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to return.  <br>**Values:** `id` *(default)*, `media_product_type`, `media_type`, `media_url`, `permalink`, `username`, `text`, `timestamp`, `shortcode`, `thumbnail_url`, `children`, `is_quote_post`, `has_replies`, `root_post`, `replied_to`, `is_reply`, `is_reply_owned_by_me`, `hide_status`, `reply_audience`, `quoted_post`, `reposted_post`, `gif_url`, `topic_tag`, `is_verified`, `profile_picture_url` |
| `reverse`<br><br>Boolean | **Optional.**  <br>Sorts replies in reverse chronological order.  <br>**Values:** `true` *(default)*, `false` |
| `before` | **Optional.**  <br>A cursor for pagination. Both `before` and `after` parameters cannot be passed at the same time. |
| `after` | **Optional.**  <br>A cursor for pagination. Both `before` and `after` parameters cannot be passed at the same time. |

## `POST /{threads-reply-id}/manage_reply`
Hide or unhide a top-level reply on your Threads post. See [Hide Replies](https://developers.facebook.com/documentation/threads/reply-management#hide-replies) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `threads-reply-id`<br><br>string | **Required.**  <br>The path parameter of the Threads reply media identifier. |
| `hide`<br><br>Boolean | **Required.**  <br>Set to `true` to hide a reply and set to `false` to unhide a reply.  <br>**Values:** `true`, `false` |

## `GET /{threads-media-id}/pending_replies`

Fetch a paginated list of all pending replies. See [Reply Approvals](https://developers.facebook.com/documentation/threads/reply-management#reply-approvals) for more information.

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `threads-media-id`<br><br>string | **Required.**  <br>The path parameter of the Threads media identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to return.  <br>**Values:** `id` *(default)*, `media_product_type`, `media_type`, `media_url`, `permalink`, `username`, `text`, `timestamp`, `shortcode`, `thumbnail_url`, `children`, `is_quote_post`, `has_replies`, `root_post`, `replied_to`, `is_reply`, `is_reply_owned_by_me`, `hide_status`, `reply_audience`, `quoted_post`, `reposted_post`, `gif_url`, `topic_tag`, `is_verified`, `profile_picture_url`, `reply_approval_status` |
| `reverse`<br><br>Boolean | **Optional.**  <br>Sorts replies in reverse chronological order.  <br>**Values:** `true` *(default)*, `false` |
| `before` | **Optional.**  <br>A cursor for pagination. Both `before` and `after` parameters cannot be passed at the same time. |
| `after` | **Optional.**  <br>A cursor for pagination. Both `before` and `after` parameters cannot be passed at the same time. |

## `POST /{threads-reply-id}/manage_pending_reply`

Approve or ignore a pending reply on your Threads post. See [Reply Approvals](https://developers.facebook.com/documentation/threads/reply-management#reply-approvals) for more information.

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `threads-reply-id`<br><br>string | **Required.**  <br>The path parameter of the Threads reply media identifier. |
| `approve`<br><br>Boolean | **Required.**  <br>Set to `true` to approve a reply, and set to `false` to ignore a reply.  <br>**Values:** `true`, `false` |