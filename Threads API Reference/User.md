# User



The Threads user endpoints allow you to retrieve a Threads user's profile, posts, replies, mentions, ghost posts, and publishing limit, and to look up public profiles and their posts. See [Threads profiles](https://developers.facebook.com/documentation/threads/threads-profiles) for more information.

## Common parameters

These parameters work the same way on every endpoint on this page that uses them. Each endpoint lists the ones it uses.

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads API user access token. |
| `since`<br><br>datetime | **Optional.**  <br>The start date for retrieval, as a Unix timestamp (such as `1767225600`) or a date (such as `2026-01-01`). Must be on or after `1688540400` and before `until`. |
| `until`<br><br>datetime | **Optional.**  <br>The end date for retrieval, as a Unix timestamp (such as `1767225600`) or a date (such as `2026-01-01`). Must be after `since` and no later than the current time. |
| `limit`<br><br>int | **Optional.**  <br>The maximum number of media objects or records to return. The default is `25` and the maximum is `100`. Only non-negative numbers are allowed. |
| `before`<br><br>string | **Optional.**  <br>A cursor for pagination. You cannot pass both `before` and `after` in the same request. |
| `after`<br><br>string | **Optional.**  <br>A cursor for pagination. You cannot pass both `before` and `after` in the same request. |

## `GET /{threads-user-id}/threads`

Retrieve a paginated list of all Threads posts created by a user. See [Retrieve a list of an app-scoped user's posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts#retrieve-a-list-of-an-app-scoped-user-s-threads) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`, `since`, `until`, `limit`, `before`, and `after`.

| Name | Description |
| --- | --- |
| `threads-user-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads user identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `id` *(default)*, `media_product_type`, `media_type`, `media_url`, `permalink`, `owner`, `username`, `text`, `timestamp`, `shortcode`, `thumbnail_url`, `children`, `is_quote_post`, `alt_text`, `link_attachment_url`, `has_replies`, `reply_audience`, `quoted_post`, `reposted_post`, `gif_url`, `is_spoiler_media`, `text_entities`, `text_attachment`, `is_verified`, `profile_picture_url` |

## `GET /{threads-user-id}?fields=id,username,...` {#get---threads-user-id--fields-id-username----}

Retrieve profile information about a user on Threads. See [Retrieve a Threads app-scoped user's profile information](https://developers.facebook.com/documentation/threads/threads-profiles#retrieve-a-threads-app-scoped-users-profile-information) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`.

| Name | Description |
| --- | --- |
| `threads-user-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads user identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `id` *(default)*, `username`, `name`, `threads_profile_picture_url`, `threads_biography`, `is_verified`, `recently_searched_keywords` |

## `GET /profile_lookup?username=...`

Look up a public profile and retrieve its basic profile information. See [Retrieve a Threads user's public profile information](https://developers.facebook.com/documentation/threads/threads-profiles#retrieve-a-threads-user-s-public-profile-information) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`.

| Name | Description |
| --- | --- |
| `username`<br><br>string | **Required.**  <br>Handle or unique username on Threads. Must be an exact match. |

## `GET /profile_posts?username=...`

Look up a public profile and retrieve its posts on Threads. See [Retrieve a list of a public profile's posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts#retrieve-a-list-of-a-public-profile-s-threads) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`, `since`, `until`, `limit`, `before`, and `after`.

| Name | Description |
| --- | --- |
| `username`<br><br>string | **Required.**  <br>Handle or unique username on Threads. Must be an exact match. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `id` *(default)*, `media_product_type`, `media_type`, `media_url`, `permalink`, `username`, `text`, `timestamp`, `shortcode`, `thumbnail_url`, `children`, `is_quote_post`, `alt_text`, `link_attachment_url`, `has_replies`, `reply_audience`, `quoted_post`, `reposted_post`, `gif_url`, `is_spoiler_media`, `text_entities` |

## `GET /{threads-user-id}/threads_publishing_limit`

Check the app user's current publishing rate limit usage. See [Rate limiting](https://developers.facebook.com/documentation/threads/overview#rate-limiting) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`.

| Name | Description |
| --- | --- |
| `threads-user-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads user identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `quota_usage` *(default)*, `config`, `reply_quota_usage`, `reply_config`, `delete_quota_usage`, `delete_config`, `location_search_quota_usage`, `location_search_config` |

## `GET /{threads-user-id}/replies`

Retrieve a paginated list of all Threads replies created by a user. See [Retrieve a list of a user's replies](https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/retrieve-replies#retrieve-a-list-of-a-users-replies) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`, `since`, `until`, `limit`, `before`, and `after`.

| Name | Description |
| --- | --- |
| `threads-user-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads user identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `id` *(default)*, `media_product_type`, `media_type`, `media_url`, `permalink`, `username`, `text`, `timestamp`, `shortcode`, `thumbnail_url`, `children`, `is_quote_post`, `has_replies`, `root_post`, `replied_to`, `is_reply`, `is_reply_owned_by_me`, `reply_audience`, `quoted_post`, `reposted_post`, `gif_url`, `is_verified`, `profile_picture_url` |

## `GET /{threads-user-id}/mentions`

Retrieve a paginated list of all Threads posts where a user is mentioned. See [Mentions](https://developers.facebook.com/documentation/threads/threads-mentions) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`, `since`, `until`, `limit`, `before`, and `after`.

| Name | Description |
| --- | --- |
| `threads-user-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads user identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the [fields](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts#fields) to be returned. If omitted, the default fields are returned. |

## `GET /{threads-user-id}/ghost_posts`

Retrieve a paginated list of all Threads ghost posts created by a user. See [Retrieve a list of an app-scoped user's ghost posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts#retrieve-a-list-of-an-app-scoped-user-s-ghost-posts) for more information.

### Parameters

This endpoint also uses these [common parameters](#common-parameters): `access_token`, `since`, `until`, `limit`, `before`, and `after`.

| Name | Description |
| --- | --- |
| `threads-user-id`<br><br>numeric string | **Required.**  <br>The path parameter of the Threads user identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the [fields](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts#fields) to be returned. If omitted, the default fields are returned. |