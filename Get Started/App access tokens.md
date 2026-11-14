# App access tokens



Use an app access token to make requests to the Threads API on behalf of an app rather than a user. Certain APIs require app access tokens instead of user access tokens, such as the [oEmbed API](https://developers.facebook.com/documentation/threads/tools-and-resources/embed-a-threads-post).

## Generating an app access token

To generate an app access token, you need:

* Your Threads app ID
* Your Threads app secret

### Example request

```bash
curl -X GET "https://graph.threads.com/oauth/access_token?client_id=<THREADS_APP_ID>&client_secret=<THREADS_APP_SECRET>&grant_type=client_credentials"
```

### Example response

```json
{
  "access_token": "TH|<THREADS_APP_ID>|<THREADS_APP_SECRET>",
  "token_type": "bearer"
}
```

This call returns an app access token that you can use in place of a user access token to make API calls as noted above.

**Note:** **Note:** Because this request uses your app secret, it must never be made in client-side code or in an app binary that could be decompiled. Never share your app secret with anyone. Make this API call only from server-side code.

## Alternate method

Another method to call the Threads API on behalf of an app does not require a generated app access token. You can pass your app ID and app secret as the `access_token` parameter when you make a call.

### Example request

```bash
curl -X GET "https://graph.threads.com/<API_ENDPOINT>?access_token=TH|<THREADS_APP_ID>|<THREADS_APP_SECRET>&..."
```

The choice to use a generated access token or this method depends on where you hide your app secret.