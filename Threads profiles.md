# Threads profiles



The [Threads Profile API](https://developers.facebook.com/documentation/threads/reference/user#get---threads-user-id--fields-id-username----) and [Threads Profile Discovery API](https://developers.facebook.com/documentation/threads/reference/user#get-profile_lookupusername) provide two ways of retrieving Threads profile information depending on scope.

## Retrieve a Threads app-scoped user's profile information

Use the `GET /{threads-user-id}?fields=id,username,...` endpoint to return profile information about a Threads user.

### Permissions

Retrieving an app-scoped user's profile information requires an appropriate access token and permissions based on the endpoint you are calling. While you are testing, you can generate tokens and grant your app permissions by using the Graph API Explorer.

* `threads_basic` — Required for making any calls to all Threads API endpoints.

### Limitations

* You can only fetch the profile of the app-scoped user.

### Fields

| Name | Description |
| --- | --- |
| `id` | Threads user ID. This is returned by default. |
| `username` | Handle or unique username on Threads. |
| `name` | Display name of the user on Threads. |
| `threads_profile_picture_url` | URL of the user's profile picture on Threads. |
| `threads_biography` | Biography text on Threads profile. |
| `is_verified` | Whether the user is verified on Threads. |

### Example request

```bash
curl -s -X GET \
"https://graph.threads.com/v1.0/me?fields=id,username,name,threads_profile_picture_url,threads_biography,is_verified&access_token=<ACCESS_TOKEN>"
```

### Example response

```json
{
  "id": "1234567",
  "username": "threadsapitestuser",
  "name": "Threads API Test User",
  "threads_profile_picture_url": "https://scontent-sjc3-1.cdninstagram.com/link/to/profile/picture/on/threads/",
  "threads_biography": "This is my Threads bio.",
  "is_verified": false
}
```

## Retrieve a Threads user's public profile information {#retrieve-a-threads-user-s-public-profile-information}

Use the `GET /profile_lookup?username=...` endpoint to look up a public profile and retrieve their basic profile information.

### Permissions

The Threads Profile Discovery API requires an appropriate access token and permissions based on the endpoint you are calling. While you are testing, you can generate tokens and grant your app permissions by using the Graph API Explorer.

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_profile_discovery` — Required for making any calls to all Threads Profile Discovery API endpoints.

With [standard access](https://developers.facebook.com/documentation/development/graph-api/overview/access-levels), only some of the official Meta accounts can be looked up. These include @meta, @threads, @instagram, and @facebook.

### Limitations

* Only returns public profiles with at least 100 followers.
* A user can send a maximum of 1,000 requests within a rolling 24-hour period. Once a query is sent, it counts against this limit for 24 hours.

### Parameters

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads API user access token. |
| `username`<br><br>string | **Required.**  <br>Handle or unique username on Threads. Must be an exact match. |

### Fields

| Name | Description |
| --- | --- |
| `username`<br><br>string | Handle or unique username on Threads. |
| `name`<br><br>string | Display name of the user on Threads. |
| `profile_picture_url`<br><br>URL string | URL of the user's profile picture on Threads. |
| `biography`<br><br>string | Biography text on Threads profile. |
| `follower_count`<br><br>int | Total follower count of the user. |
| `likes_count`<br><br>int | Likes count of the user's posts in the past 7 days. |
| `quotes_count`<br><br>int | Quotes count of the user's posts in the past 7 days. |
| `reposts_count`<br><br>int | Reposts count of the user's posts in the past 7 days. |
| `views_count`<br><br>int | Views count of the user's posts in the past 7 days. |
| `is_verified`<br><br>Boolean | Whether the user is verified on Threads. |

### Example request

```bash
curl -i -X GET \
  "https://graph.threads.com/v1.0/profile_lookup?access_token=<ACCESS_TOKEN>&username=<THREADS_USERNAME>"
```

### Example response

```json
{
  "username": "meta",
  "name": "Meta",
  "profile_picture_url": "https://scontent-sjc3-1.cdninstagram.com/link/to/profile/picture/on/threads/",
  "biography": "Connect with what you love to make things happen. It's Your World.",
  "is_verified": true,
  "follower_count": 1234567,
  "likes_count": 1234567,
  "quotes_count": 1234567,
  "replies_count": 1234567,
  "reposts_count": 1234567,
  "views_count": 1234567
}
```