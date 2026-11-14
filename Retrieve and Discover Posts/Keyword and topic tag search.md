# Keyword and topic tag search



Search for public Threads media with specific keywords or by topic tag.

## Limitations

* A user can send a maximum of 2,200 queries within a rolling 24-hour period. Once a query is sent, it counts against this limit for 24 hours.
* This limit applies to a user across apps and is not differentiated for different apps. If multiple apps send requests for the same user, those queries apply to the same limit for that user.
* Subsequent queries against the same keyword within this timeframe also count against this limit.
* Queries which return no results do not count against this limit for the user. If no results are returned, consider refining or shortening your query.
* The API returns an empty array for any requests that include keywords that Threads has deemed sensitive or offensive.

## Permissions

The Threads Keyword Search API requires an appropriate access token and permissions. While you are testing, you can generate tokens and grant your app permissions by using the Graph API Explorer.

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_keyword_search` — Required for making `GET` calls to the keyword search endpoint.

If your app has not been approved for the `threads_keyword_search` permission, the search is performed only on posts owned by the authenticated user. After approval, public posts are searchable.

## Keyword search

To search for public Threads media by keyword, send a `GET` request to the `/keyword_search` endpoint with a keyword to be queried.

### Parameters

| Name | Description |
| --- | --- |
| `q`<br><br>string | **Required.**  <br>The keyword(s) to be queried. |
| `search_type`<br><br>string | **Optional.**  <br>Specifies the search behavior.<br><br>**Values:**<br><br>* `TOP` *(default)* — Returns the most popular search results.<br>* `RECENT` — Returns the most recent search results. |
| `search_mode`<br><br>string | **Optional.**  <br>Specifies the search mode.<br><br>**Values:**<br><br>* `KEYWORD` *(default)* — The query is treated as a keyword.<br>* `TAG` — The query is treated as a topic tag. |
| `media_type`<br><br>string | **Optional.**  <br>Specifies the type of media to search for. Only the media type values listed below are supported.<br><br>**Values:**<br><br>* `TEXT` — The query searches for text posts.<br>* `IMAGE` — The query searches for image posts.<br>* `VIDEO` — The query searches for video posts. |
| `since`<br><br>datetime | **Optional.**  <br>The start date for retrieval, as a Unix timestamp (such as `1767225600`) or a date (such as `2026-01-01`). Must be on or after `1688540400` and before `until`. |
| `until`<br><br>datetime | **Optional.**  <br>The end date for retrieval, as a Unix timestamp (such as `1767225600`) or a date (such as `2026-01-01`). Must be after `since` and no later than the current time. |
| `limit`<br><br>int | **Optional.**  <br>The maximum number of media objects or records to return. The default is `25` and the maximum is `100`. Only non-negative numbers are allowed. |
| `author_username`<br><br>string | **Optional.**  <br>Filters search results to include only posts created by the specified username or profile. The username must be an exact match without the `@` symbol. |

See the [Media](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts) documentation for a list of available fields.

**Note:** The `owner` field is excluded and is not returned.

### Example request

```bash
curl -s -G \
  --data-urlencode "q=<KEYWORD>" \
  -d "search_type=TOP" \
  -d "fields=id,text,media_type,permalink,timestamp,username,has_replies,is_quote_post,is_reply" \
  -d "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/keyword_search"
```

### Example response

```json
{
  "data": [
    {
      "id": "1234567890",
      "text": "first thread",
      "media_type": "TEXT_POST",
      "permalink": "https://www.threads.com/@<USER>/post/abcdefg",
      "timestamp": "2023-10-17T05:42:03+0000",
      "username": "<USER>",
      "has_replies": false,
      "is_quote_post": false,
      "is_reply": false
    }
  ]
}
```

## Topic tag search

To search for public Threads media by topic tag, send a `GET` request to the `/keyword_search` endpoint with a topic to be queried. To perform a topic tag search, you need to use the `search_mode` parameter and set the value to `TAG`.

### Example request

```bash
curl -s -G \
  --data-urlencode "q=<TAG>" \
  -d "search_mode=TAG" \
  -d "search_type=TOP" \
  -d "fields=id,text,media_type,permalink,timestamp,username,has_replies,is_quote_post,is_reply" \
  -d "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/keyword_search"
```

### Example response

```json
{
  "data": [
    {
      "id": "1234567890",
      "text": "second thread",
      "media_type": "TEXT_POST",
      "permalink": "https://www.threads.com/@<USER>/post/abcdefg",
      "timestamp": "2023-10-17T05:42:03+0000",
      "username": "<USER>",
      "has_replies": false,
      "is_quote_post": false,
      "is_reply": false
    }
  ]
}
```

## Search by media type

To search for public Threads posts by media type, send a `GET` request to the `/keyword_search` endpoint with the `media_type` parameter. Searches can be done for text, image, and video media types. If the `media_type` parameter is not sent, all media types are returned in the response.

### Example request

```bash
curl -s -G \
  --data-urlencode "q=<KEYWORD>" \
  -d "media_type=IMAGE" \
  -d "fields=id,text,media_type,permalink,timestamp,username" \
  -d "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/keyword_search"
```

### Example response

```json
{
  "data": [
    {
      "id": "1234567890",
      "text": "third thread",
      "media_type": "IMAGE",
      "permalink": "https://www.threads.com/@<USER>/post/abcdefg",
      "timestamp": "2023-10-17T05:42:03+0000",
      "username": "<USER>"
    }
  ]
}
```

## Interacting with public Threads posts {#interacting-with-public-threads}

You can interact with public Threads media that you have recently searched for. These actions include [replying](https://developers.facebook.com/documentation/threads/reply-management), [quoting](https://developers.facebook.com/documentation/threads/posts/quote-posts), and [reposting](https://developers.facebook.com/documentation/threads/posts/reposts).

**Note:** Additional permissions might be required, as listed in those pages.

## Recently searched keywords

You can retrieve a list of recently searched keywords for the currently authenticated user by sending a `GET` request to the `/me` endpoint and requesting the `recently_searched_keywords` field.

### Example request

```bash
curl -s -G \
  -d "fields=recently_searched_keywords" \
  -d "access_token=<ACCESS_TOKEN>" \
"https://graph.threads.com/v1.0/me"
```

### Example response

```json
{
  "id": "1234567890",
  "recently_searched_keywords": [
    {
      "query": "some keyword",
      "timestamp": 1735707600
    },
    {
      "query": "some other keyword",
      "timestamp": 1735707600
    }
  ]
}
```