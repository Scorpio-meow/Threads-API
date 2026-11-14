# Get access tokens



This guide explains how to use the Authorization Window to get permissions from Threads users for short-lived Threads user access tokens.

## Step 1: Get authorization

The Authorization Window allows app users to grant your app permissions and short-lived Threads user access tokens. After a user logs in and chooses which data to allow your app to access, Threads will redirect the user to your app and include an authorization code, which you can then exchange for a short-lived access token.

To begin the process, get the Authorization Window and present it to the user:

```
https://threads.com/oauth/authorize
  ?client_id=<THREADS_APP_ID>
  &redirect_uri=<REDIRECT_URI>
  &scope=<SCOPE>
  &response_type=code
  &state=<STATE> // Optional
```

If accessing the Authorization Window from an Android mobile system, make sure to open the URL in the native webview or browser and not the native app.

An example of how you can achieve this with JavaScript:

```javascript
window.open(url, '_system');`
```

### Parameters

**Note:** All parameters except `state` are required.

| Name | Description |
| --- | --- |
| `client_id`<br><br>numeric string | **Required.**  <br>Your Threads app ID displayed in **App Dashboard** > **App settings** > **Basic** > **Threads App ID**.  <br>**Example:** `990602627938098` |
| `redirect_uri`<br><br>string | **Required.**  <br>The URI that Threads will redirect users to after they allow or deny permission requests. Make sure this exactly matches one of the base URIs in your list of [valid OAuth URIs](https://developers.facebook.com/documentation/development/create-an-app/threads-use-case#settings). Keep in mind that the App Dashboard might have added a trailing slash to your URIs, so we recommend that you verify by checking the list.  <br>**Example:** https://socialsizzle.herokuapp.com/auth/ |
| `response_type`<br><br>string | **Required.**  <br>Set this value to `code`. |
| `scope`<br><br>comma-separated or space-separated list | **Required.**  <br>A comma-separated list, or URL-encoded space-separated list, of permissions to request from the app user.  <br>**Note:** `threads_basic` is required.  <br>**Values:** `threads_basic`, `threads_content_publish`, `threads_read_replies`, `threads_manage_replies`, `threads_manage_insights` |
| `state`<br><br>string | An optional value indicating a server-specific state. For example, you can use this to protect against CSRF issues. Threads will include this parameter and value when redirecting the user back to you.  <br>**Example:** `1` |

### Example Authorization Window URL {#sample-authorization-window-url}

```
https://threads.com/oauth/authorize
  ?client_id=<THREADS_APP_ID>
  &redirect_uri=https://socialsizzle.herokuapp.com/auth/
  &scope=threads_basic,threads_content_publish
  &response_type=code
```

### Successful authorization

If authorization is successful, Threads will redirect the user to your `redirect_uri` and pass an authorization code through the `code` query string parameter. Capture the code so your app can exchange it for a short-lived Threads user access token.

Authorization codes are valid for 1 hour and can only be used once.

#### Example successful authorization redirect {#sample-successful-authentication-redirect}

```
https://socialsizzle.herokuapp.com/auth/?code=AQBx-hBsH3...#_
```

**Note:** `#_` is appended to the end of the redirect URI, but it is not part of the code itself, so strip it out.

### Canceled authorization

If the user cancels the authorization flow, Threads will redirect the user to your `redirect_uri` and append the following error parameters.

**Note:** It is your responsibility to fail gracefully in these situations and display an appropriate message to your users.

| Error parameter | Description |
| --- | --- |
| `error` | `access_denied` |
| `error_reason` | `user_denied` |
| `error_description` | `The+user+denied+your+request` |

#### Example canceled authorization redirect {#sample-canceled-authorization-redirect}

```
https://socialsizzle.herokuapp.com/auth/?error=access_denied
  &error_reason=user_denied
  &error_description=The+user+denied+your+request
```

## Step 2: Exchange the code for a token

Once you receive a code, exchange it for a short-lived access token by sending a `POST` request to the following endpoint:

```
POST https://graph.threads.com/oauth/access_token
```

### Parameters

Include the following parameters in your `POST` request body.

| Name | Description |
| --- | --- |
| `client_id`<br><br>numeric string | **Required.**  <br>Your Threads app ID displayed in **App Dashboard** > **App settings** > **Basic** > **Threads App ID**.  <br>**Example:** `990602627938098` |
| `client_secret`<br><br>string | **Required.**  <br>Your Threads app secret displayed in **App Dashboard** > **App settings** > **Basic** > **Threads App secret**.  <br>**Example:** `a1b2C3D4` |
| `code`<br><br>string | **Required.**  <br>The authorization code that Threads passed in the `code` parameter when redirecting the user to your `redirect_uri`.  <br>**Example:** `AQBx-hBsH3...` |
| `grant_type`<br><br>string | **Required.**  <br>Set this value to `authorization_code`. |
| `redirect_uri`<br><br>string | **Required.**  <br>The `redirect_uri` value you used in the Authorization Window request. It must match exactly, or the request is rejected.  <br>**Example:** https://socialsizzle.herokuapp.com/auth/ |

### Example request {#sample-request}

```bash
curl -X POST \
  https://graph.threads.com/oauth/access_token \
  -F client_id=<THREADS_APP_ID> \
  -F client_secret=<THREADS_APP_SECRET> \
  -F grant_type=authorization_code \
  -F redirect_uri=https://socialsizzle.herokuapp.com/auth/ \
  -F code=<AUTHORIZATION_CODE>
```

### Example success response {#sample-success-response}

If successful, the API returns a JSON payload containing the app user's short-lived access token, the token type, and user ID.

```json
{
  "access_token": "THQVJ...",
  "token_type": "bearer",
  "user_id": 17841405793187218
}
```

Capture the `access_token` value. This is the user's short-lived Threads user access token, which your app can use to access Threads API endpoints.

### Example rejected response {#sample-rejected-response}

If the request is malformed in some way, the API returns an error.

```json
{
  "error_type": "OAuthException",
  "code": 400,
  "error_message": "Matching code was not found or was already used"
}
```