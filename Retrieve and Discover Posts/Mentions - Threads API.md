# Mentions - Threads API



Returns a list of public Threads media objects in which a Threads profile has been tagged by another Threads profile.

### Permissions

The Threads Mentions API requires an appropriate access token and permissions based on the node you are targeting. While you are testing, you can generate tokens and grant your app permissions by using the Graph API Explorer.

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_manage_mentions` — Required for making any calls to the mentions endpoint.

If your app has not been approved for advanced access for the `threads_manage_mentions` permission, the API returns only mentions made by a Threads tester on the app. After approval, the API returns other users' public posts.

### Limitations

* Threads media objects created by private users will not be returned.
* The `since` parameter's timestamp must be greater than or equal to `1688540400` and less than the `until` parameter, which must be less than or equal to the current timestamp and greater than the `since` parameter.

## Retrieve Threads mentions

### Fields

Use the `fields` parameter to specify [fields](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts#fields) you want included on any returned Threads media objects.

### Example request

```
curl -s -X GET \
  https://graph.threads.com/<THREADS_USER_ID>/mentions?fields=<LIST_OF_FIELDS>&access_token=<ACCESS_TOKEN>
```

### Example response

A successful API call returns a JSON-formatted object containing Threads media objects.

```
{
  "<FIELD>":"<VALUE>",
  ...
}
```