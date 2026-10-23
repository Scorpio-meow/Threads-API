# Long-lived access tokens - Threads API



By default, Threads user access tokens are short-lived and are valid for one hour. However, short-lived tokens can be exchanged for long-lived tokens.

Long-lived tokens are valid for 60 days and can be refreshed as long as they are at least 24 hours old but have not expired, and the app user has granted your app the `threads_basic` permission. Refreshed tokens are valid for 60 days from the date at which they are refreshed. Tokens that have not been refreshed in 60 days will expire and can no longer be refreshed.

Long-lived access tokens for private Threads profiles can now be refreshed. In addition, permissions granted to apps by app users with private profiles are now valid for 90 days.

### Limitations

* Expired short-lived tokens cannot be exchanged for long-lived tokens. If the user's token has expired, get a new one before exchanging it for a long-lived token.
* Requests for long-lived tokens include your app secret so should only be made in server-side code, never in client-side code or in an app binary that could be decompiled. Do not share your app secret with anyone, expose it in code, send it to a client, or store it in a device.

## Get a Long-Lived Token

Use the `GET /access_token` endpoint to exchange a short-lived Threads user access token for a long-lived token. Once you have a long-lived token, you can use it in server-side requests or send it to the client for use there.

Your request must be made server-side and include:

* A valid (unexpired) short-lived Threads user access token.
* Your Threads app secret (**App Dashboard** > **App settings** > **Basic** > **Threads App secret**).

### Parameters

Include the following query string parameters to augment the request.

| Name | Description |
| --- | --- |
| `client_secret`<br><br>string | **Required.**  <br>Your Threads app's secret, displayed in the **App Dashboard** > **App settings** > **Basic** > **Threads App secret** field. |
| `grant_type`<br><br>string | **Required.**  <br>Set this to `th_exchange_token`. |
| `access_token`<br><br>string | **Required.**  <br>The valid (unexpired) short-lived Threads user access token that you want to exchange for a long-lived token. |

### Sample Request

```
curl -i -X GET "https://graph.threads.com/access_token
  ?grant_type=th_exchange_token
  &client_secret=<THREADS_APP_SECRET>
  &access_token=<SHORT_LIVED_ACCESS_TOKEN>"
```

### Sample Response

```
{
  "access_token": "<LONG_LIVED_USER_ACCESS_TOKEN>",
  "token_type": "bearer",
  "expires_in": 5183944  // number of seconds until token expires
}
```

## Refresh a Long-Lived Token

Use the `GET /refresh_access_token` endpoint to refresh unexpired long-lived Threads user access tokens. Refreshing a long-lived token makes it valid for 60 days again. Long-lived tokens that have not been refreshed in 60 days will expire.

Your request must include:

* A valid (unexpired) long-lived Threads user access token.

### Parameters

| Name | Description |
| --- | --- |
| `grant_type`<br><br>string | **Required.**  <br>Set this to `th_refresh_token`. |
| `access_token`<br><br>string | **Required.**  <br>The valid (unexpired) long-lived Threads user access token that you want to refresh. |

### Sample Request

```
curl -i -X GET "https://graph.threads.com/refresh_access_token
  ?grant_type=th_refresh_token
  &access_token=<LONG_LIVED_ACCESS_TOKEN>"
```

### Sample Response

```
{
  "access_token": "<LONG_LIVED_USER_ACCESS_TOKEN>",
  "token_type": "bearer",
  "expires_in": 5183944 // number of seconds until token expires
}
```