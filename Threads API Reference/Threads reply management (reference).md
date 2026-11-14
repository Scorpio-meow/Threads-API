# Threads reply management (reference)



The Threads reply management endpoints allow you to retrieve replies and conversations, hide or unhide replies, and approve or ignore pending replies. See [Threads Reply Management API](https://developers.facebook.com/documentation/threads/reply-management) for more information.

## Common parameters

These parameters work the same way on every endpoint on this page that uses them. Each endpoint lists the ones it uses.

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads API user access token. |
| `reverse`<br><br>Boolean | **Optional.**  <br>Whether to sort replies in reverse chronological order.  <br>**Values:** `true` *(default)*, `false` |
| `before`<br><br>string | **Optional.**  <br>A cursor for pagination. You cannot pass both `before` and `after` in the same request. |
| `after`<br><br>string | **Optional.**  <br>A cursor for pagination. You cannot pass both `before` and `after` in the same request. |

## `GET /{threads-media-id}/replies`

Retrieve a paginated list of all top-level replies for a Threads media object. See [Replies](https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/replies-and-conversations#a-threads-replies) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`, `reverse`, `before`, and `after`.

| Name | Description |
| --- | --- |
| `threads-media-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads media identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `id` *(default)*, `media_product_type`, `media_type`, `media_url`, `permalink`, `username`, `text`, `timestamp`, `shortcode`, `thumbnail_url`, `children`, `is_quote_post`, `has_replies`, `root_post`, `replied_to`, `is_reply`, `is_reply_owned_by_me`, `hide_status`, `reply_audience`, `quoted_post`, `reposted_post`, `gif_url`, `topic_tag`, `is_verified`, `profile_picture_url` |

## `GET /{threads-media-id}/conversation`

Retrieve a paginated and flattened list of all top-level and nested replies for a Threads media object. See [Conversations](https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/replies-and-conversations#a-threads-conversations) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`, `reverse`, `before`, and `after`.

| Name | Description |
| --- | --- |
| `threads-media-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads media identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `id` *(default)*, `media_product_type`, `media_type`, `media_url`, `permalink`, `username`, `text`, `timestamp`, `shortcode`, `thumbnail_url`, `children`, `is_quote_post`, `has_replies`, `root_post`, `replied_to`, `is_reply`, `is_reply_owned_by_me`, `hide_status`, `reply_audience`, `quoted_post`, `reposted_post`, `gif_url`, `topic_tag`, `is_verified`, `profile_picture_url` |

## `POST /{threads-reply-id}/manage_reply`

Hide or unhide a top-level reply on your Threads post. See [Hide replies](https://developers.facebook.com/documentation/threads/reply-management#hide-replies) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`.

| Name | Description |
| --- | --- |
| `threads-reply-id`<br><br>numeric string | **Required.**  <br>The path parameter of the media identifier of the Threads reply. |
| `hide`<br><br>Boolean | **Required.**  <br>Set to `true` to hide a reply and set to `false` to unhide a reply.  <br>**Values:** `true`, `false` |

## `GET /{threads-media-id}/pending_replies`

Retrieve a paginated list of all pending replies for a Threads media object. See [Reply approvals](https://developers.facebook.com/documentation/threads/reply-management#reply-approvals) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`, `reverse`, `before`, and `after`.

| Name | Description |
| --- | --- |
| `threads-media-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads media identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `id` *(default)*, `media_product_type`, `media_type`, `media_url`, `permalink`, `username`, `text`, `timestamp`, `shortcode`, `thumbnail_url`, `children`, `is_quote_post`, `has_replies`, `root_post`, `replied_to`, `is_reply`, `is_reply_owned_by_me`, `hide_status`, `reply_audience`, `quoted_post`, `reposted_post`, `gif_url`, `topic_tag`, `is_verified`, `profile_picture_url`, `reply_approval_status` |

## `POST /{threads-reply-id}/manage_pending_reply`

Approve or ignore a pending reply on your Threads post. See [Reply approvals](https://developers.facebook.com/documentation/threads/reply-management#reply-approvals) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`.

| Name | Description |
| --- | --- |
| `threads-reply-id`<br><br>numeric string | **Required.**  <br>The path parameter of the media identifier of the Threads reply. |
| `approve`<br><br>Boolean | **Required.**  <br>Set to `true` to approve a reply, and set to `false` to ignore a reply.  <br>**Values:** `true`, `false` |