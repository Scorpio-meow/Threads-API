# Debug Access Token



The `/debug_token` endpoint returns metadata about a given access token. This includes data such as the user for which the token was issued, whether the token is still valid, when it expires, and what permissions the app has for the given user.

To call this endpoint, provide either an [app access token](https://developers.facebook.com/documentation/threads/get-started/app-access-tokens) or a user access token from a [Threads tester](https://developers.facebook.com/documentation/threads/get-started#threads-testers) as the `access_token` parameter. In either case, the access token must be associated with the same app that is linked to the `input_token` being inspected. An app can only inspect tokens that belong to itself.

## Retrieve an Access Token's Data

### Example Request

```bash
curl -i -X GET \
  "https://graph.threads.com/v1.0/debug_token?access_token=<APP_OR_THREADS_TESTER_ACCESS_TOKEN>&input_token=<ACCESS_TOKEN_TO_BE_INSPECTED>"
```

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**<br>An [app access token](https://developers.facebook.com/documentation/threads/get-started/app-access-tokens), or a Threads Graph API user access token of a Threads tester. |
| `input_token`<br><br>string | **Required.**<br>The access token to be inspected (does not need to be a Threads tester but must be associated with the same app as the `access_token` parameter). |

**Note:** The `access_token` and `input_token` can be associated with different users but must be associated with the same app. If the `input_token` was issued by a different app, the call fails with the following error message: `The App_id in the input_token did not match the Viewing App`.

### Threads App Access Token Format

A Threads app access token follows the following format: `TH|<APP_ID>|<APP_SECRET>`. See [App Access Tokens](https://developers.facebook.com/documentation/threads/get-started/app-access-tokens) for details on how to generate one.

### Example Response

```json
{
  "data": {
    "type": "USER",
    "application": "Threads API Test App",
    "data_access_expires_at": 1754846089,
    "expires_at": 1752254132,
    "is_valid": true,
    "issued_at": 1747070132,
    "scopes": [
      "threads_basic",
      "threads_content_publish",
      "threads_manage_replies",
      "threads_manage_insights",
      "threads_read_replies",
      "threads_manage_mentions",
      "threads_keyword_search",
      "threads_location_tagging"
    ],
    "user_id": "1234567890123456"
  }
}
```

### Fields

| Name | Description |
| --- | --- |
| `data`<br><br>object | Data wrapper around the result. |
| `type`<br><br>string | Whether the access token is an app access token or user access token. |
| `application`<br><br>string | Name of the application this access token is for. |
| `data_access_expires_at`<br><br>Unixtime | Timestamp when the app's access to user data expires. |
| `expires_at`<br><br>Unixtime | Timestamp when this access token expires. |
| `is_valid`<br><br>Boolean | Whether the access token is still valid or not. |
| `issued_at`<br><br>Unixtime | Timestamp when this access token was issued. |
| `scopes`<br><br>string[] | List of permissions that the user has granted for the app in this access token. |
| `user_id`<br><br>string | The ID of the user this access token is for. |