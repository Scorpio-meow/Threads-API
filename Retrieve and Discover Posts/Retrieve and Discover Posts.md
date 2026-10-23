# Retrieve and Discover Posts



You can search for posts using the keyword search or retrieve posts and mentions related to a specific user.

## Pagination

Retrieving a user's posts and mentions supports cursor-based pagination so the response will include `before` and `after` cursors if the response contains multiple pages of data. Unlike standard cursor-based pagination, however, the response will not include previous or next fields, so you will have to use the `before` and `after` cursors to construct previous and next query strings manually in order to page through the returned data set.

### Example request

```
curl -s -X GET \
  https://graph.threads.com/17841405822304914/mentions?fields=id,username&access_token=EAADd...
```

### Example response

```
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

* [Retrieve Posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts)
* [Mentions](https://developers.facebook.com/documentation/threads/threads-mentions)
* [Keyword Search](https://developers.facebook.com/documentation/threads/keyword-search)