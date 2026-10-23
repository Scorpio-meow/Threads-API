# Delete Posts



You can use the Threads API to delete your own posts.

## Deleting

You can delete a Threads post that was created by the authenticated user by making a request to the `DELETE /{threads-media-id}` endpoint with the post's media object ID. Make sure to include the `access_token` parameter with your API request.

### Permissions

The Threads Delete API requires an appropriate access token and permissions based on the node you are targeting. While you are testing, you can easily generate tokens and grant your app permissions by using the Graph API Explorer.

- `threads_basic` — Required for making any calls to all Threads API endpoints.
- `threads_delete` — Required for making any delete calls.

### Limitations

* The Delete endpoint has a rate limit of 100 deletes per day per account.

### Example Request

```html
curl -i -X DELETE \
  "https://graph.threads.com/v1.0/<THREADS_MEDIA_ID>?access_token=<ACCESS_TOKEN>"
```

### Example Response

```html
{
  "success": true,
  "deleted_id": "1234567",
}
```

The request above deletes a Threads post and returns a response indicating whether the action was successful or not, along with the deleted post's ID.