# Debug



Retrieve various data about an access token. See [Debug Access Token](https://developers.facebook.com/documentation/threads/troubleshooting/debug-access-token) for more information.

## `GET /debug_token`

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**<br>An [app access token](https://developers.facebook.com/documentation/threads/get-started/app-access-tokens), or a Threads Graph API user access token of a Threads tester. |
| `input_token`<br><br>string | **Required.**<br>The access token to inspect. |

**Note:** The `access_token` and `input_token` can be associated with different users but must be associated with the same app. If the `input_token` was issued by a different app, the call fails with the following error message: `The App_id in the input_token did not match the Viewing App`.

### Fields

| Name | Description |
| --- | --- |
| `data`<br><br>object | Data wrapper around the result. |
| `type`<br><br>string | Whether the access token is an app or user access token. |
| `application`<br><br>string | Name of the application this access token is for. |
| `data_access_expires_at`<br><br>Unixtime | Timestamp when the app's access to user data expires. |
| `expires_at`<br><br>Unixtime | Timestamp when this access token expires. |
| `is_valid`<br><br>Boolean | Whether the access token is still valid. |
| `issued_at`<br><br>Unixtime | Timestamp when this access token was issued. |
| `scopes`<br><br>string[] | List of permissions that the user has granted for the app in this access token. |
| `user_id`<br><br>string | The ID of the user this access token is for. |