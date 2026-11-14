# Retrieve and discover posts



You can search for posts using the keyword search or retrieve posts and mentions related to a specific user.

## Pagination

Retrieving a user's posts and mentions supports cursor-based pagination, so the response includes `before` and `after` cursors if the response contains multiple pages of data. Unlike standard cursor-based pagination, however, the response does not include previous or next fields, so you have to use the `before` and `after` cursors to construct previous and next query strings manually to page through the returned data set.

### Example request

```bash
curl -s -X GET \
  "https://graph.threads.com/v1.0/<THREADS_USER_ID>/mentions?fields=id,username&access_token=<ACCESS_TOKEN>"
```

### Example response

```json
{
  "data": [
    {
      "id": "18038...",
      "username": "keldo..."
    },
    {
      "id": "17930...",
      "username": "ashla..."
    },
    {
      "id": "17931...",
      "username": "jaypo..."
    }
  ]
}
```

## Next steps

* [Retrieve posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts)
* [Mentions](https://developers.facebook.com/documentation/threads/threads-mentions)
* [Keyword search](https://developers.facebook.com/documentation/threads/keyword-search)