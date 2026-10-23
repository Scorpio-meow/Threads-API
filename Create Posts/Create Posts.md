# Create Posts



You can use the Threads API to publish image, video, text, or carousel posts as well as quote and repost other posts.

## Permissions

Posting to Threads requires an appropriate access token and permissions based on the node you are targeting. While you are testing, you can generate tokens and grant your app permissions by using the Graph API Explorer.

- `threads_basic` — Required for making any calls to all Threads API endpoints.
- `threads_content_publish` — Required for Threads publishing endpoints only.

If your app has not been approved for advanced access for the `threads_content_publish` permission, you can only post on behalf of [Threads testers](https://developers.facebook.com/documentation/threads/get-started#threads-testers) on your app. After your app is published and approved, you can post on behalf of any Threads user who grants your app the permission.

## Fediverse

For Threads users who have [enabled sharing to the fediverse](https://help.instagram.com/760878905943039), eligible posts made to Threads via the Threads API will also be shared to the fediverse starting August 28, 2024.

## Next steps

* [Threads Posts](https://developers.facebook.com/documentation/threads/posts)
* [Reposts](https://developers.facebook.com/documentation/threads/posts/reposts)
* [Quote Posts](https://developers.facebook.com/documentation/threads/posts/quote-posts)
* [Spoilers](https://developers.facebook.com/documentation/threads/create-posts/spoilers)
* [Text Attachments](https://developers.facebook.com/documentation/threads/create-posts/text-attachments)
* [Geo-Gated Content](https://developers.facebook.com/documentation/threads/posts/geo-gating)
* [Accessibility](https://developers.facebook.com/documentation/threads/posts/accessibility)