# Media Retrieval



You can retrieve Threads media objects by individual ID or by searching on a keyword. See [Retrieve Threads Media Objects](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts) and [Keyword Search](https://developers.facebook.com/documentation/threads/keyword-search) for more information on each method.

## `GET /{threads-media-id}`
Retrieve a Threads media object. See [Retrieve a Single Threads Media Object](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts#retrieve-a-single-threads-media-object) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `threads-media-id`<br><br>string | **Required.**  <br>The path parameter of the Threads media identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields that the API returns.  <br>**Values:** `id` *(default)*, `media_product_type`, `media_type`, `media_url`, `permalink`, `owner`, `username`, `text`, `timestamp`, `shortcode`, `thumbnail_url`, `children`, `is_quote_post`, `alt_text`, `link_attachment_url`, `has_replies`, `is_reply`, `is_reply_owned_by_me`, `root_post`, `replied_to`, `hide_status`, `reply_audience`, `quoted_post`, `reposted_post`, `gif_url`, `poll_attachment`, `topic_tag`, `is_spoiler_media`, `text_entities`, `text_attachment`, `location_id` |

## `GET /keyword_search`

Search for public Threads media with specific keywords or topic tags. See [Keyword Search](https://developers.facebook.com/documentation/threads/keyword-search) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `q`<br><br>string | **Required.**  <br>The keyword(s) to be queried. |
| `search_type`<br><br>string | **Optional.**  <br>Specifies the search behavior.<br><br>**Values:**<br><br>* `TOP` (*default*) — To get the most popular search results.<br>* `RECENT` — To get the most recent search results. |
| `search_mode`<br><br>string | **Optional.**  <br>Specifies the search mode.<br><br>**Values:**<br><br>* `KEYWORD` (*default*) — The query is treated as a keyword.<br>* `TAG` — The query will be treated as a topic tag. |
| `media_type`<br><br>string | **Optional.**  <br>Specifies the type of media to search for. Only the media type values listed below are supported.<br><br>**Values:**<br><br>* `TEXT` — The query searches for text posts.<br>* `IMAGE` — The query will search for image posts.<br>* `VIDEO` — The query will search for video posts. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `id` *(default)*, `media_product_type`, `media_type`, `media_url`, `permalink`, `username`, `text`, `timestamp`, `shortcode`, `thumbnail_url`, `children`, `is_quote_post`, `alt_text`, `link_attachment_url`, `has_replies`, `is_reply`, `root_post`, `replied_to`, `reply_audience`, `quoted_post`, `reposted_post`, `gif_url`, `poll_attachment`, `topic_tag` |
| `since` | **Optional.**  <br>Query string parameter representing the start date for retrieval (must be a Unix timestamp or a date/time representation parsable by `strtotime();`). The timestamp must be greater than or equal to `1688540400` and less than the `until` parameter. |
| `until` | **Optional.**  <br>Query string parameter representing the end date for retrieval (must be a Unix timestamp or a date/time representation parsable by `strtotime();`). The timestamp must be less than or equal to the current timestamp and greater than the `since` parameter. |
| `limit` | **Optional.**  <br>Query string parameter representing the maximum number of media objects or records requested to return. The default is **25** and the maximum is **100** (only non-negative numbers are allowed). |
| `author_username` | **Optional.**  <br>Filters search results to include only posts created by the specified username or profile. The username must be an exact match without the `@` symbol. |