# Share posts to Instagram Stories



You can enable cross-sharing of a Threads post as a Story on your linked Instagram account by including the `crossreshare_to_ig` parameter when you create content using any of the Threads [publishing](https://developers.facebook.com/documentation/threads/create-posts) endpoints.

## Limitations

* The user must have a linked Instagram account. If no linked account exists, the cross-share fails but the Threads post is still published.
* Cross-sharing creates an Instagram Story, which expires after 24 hours per standard Instagram Story behavior.
* The cross-shared Story is created through the standard Instagram Story flow, so it respects the user's existing Instagram account privacy settings and Story audience controls.

## Permissions

Sharing Threads posts to Instagram Stories requires an appropriate [access token](https://developers.facebook.com/documentation/threads/get-started/get-access-tokens-and-permissions) and permissions. While you are testing, you can generate tokens and grant your app permissions by using the [Graph API Explorer](https://developers.facebook.com/documentation/threads/get-started#graph-api-explorer).

The following permissions are required:

* `threads_basic` — Required for making calls to all Threads API endpoints.
* `threads_content_publish` — Required for Threads publishing endpoints only.
* `threads_share_to_instagram` — Required for cross-sharing the Threads post to the user's linked Instagram account as a Story.

If your app has not been approved for advanced access for the `threads_content_publish` permission, you can only post on behalf of [Threads testers](https://developers.facebook.com/documentation/threads/get-started#threads-testers) on your app. After your app is published and approved, you can post on behalf of any Threads user who grants your app the permission.

## Create a cross-shared post

To cross-share a Threads post to Instagram Stories, include either the `crossreshare_to_ig` or `crossreshare_to_ig_dark_mode` parameter set to `true` when creating a Threads media container. You can use these parameters with any supported media type (text, image, video, or carousel).

### Parameters

| Name | Description |
| --- | --- |
| `crossreshare_to_ig`<br><br>Boolean | Cross-shares a Threads post to a linked Instagram account as a Story when set to `true`.<br><br>**Values:** `true`, `false` (*default*) |
| `crossreshare_to_ig_dark_mode`<br><br>Boolean | Cross-shares a Threads post to a linked Instagram account as a Story in dark mode when set to `true`.<br><br>**Values:** `true`, `false` (*default*) |

### Response fields

When you enable cross-sharing, the publish response includes the `crossreshare_to_ig_status` field:

| Name | Description |
| --- | --- |
| `id`<br><br>string | The ID of the published Threads media. |
| `crossreshare_to_ig_status`<br><br>string | The status of the cross-share to Instagram Stories.<br>**Values:** `SUCCESS`, `FAILED` |

**Note:** The Threads post is published even if the cross-share to Instagram fails. Check the `crossreshare_to_ig_status` field to confirm whether the Story was created successfully.

### Example request

```bash
curl -X POST \
  -d "media_type=text" \
  -d "text=<POST_TEXT>" \
  -d "crossreshare_to_ig=true" | "crossreshare_to_ig_dark_mode=true" \
  -d "access_token=<ACCESS_TOKEN>"
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads"
```

### Example response

```json
{
  "id": "<MEDIA_CONTAINER_ID>",
  "crossreshare_to_ig_status": "SUCCESS" | "FAILED"
}
```