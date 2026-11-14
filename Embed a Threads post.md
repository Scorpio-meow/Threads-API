# Embed a Threads post



You can use the Threads oEmbed endpoint to retrieve the embed HTML code snippet and essential metadata for a public Threads post or profile, allowing you to display a rich preview on an external website or application. Post embeds mirror how text, image, video, and carousel posts appear on Threads. For profiles, the embed includes the user's name, profile picture, bio, follower count, and a **Follow** button.

## Common use cases

* Embed a creator's post or profile in a blog or website.
* Render a post or profile in a content management system.

## Limitations

* The Threads oEmbed endpoint is only intended to be used for embedding Threads content in websites and apps. It is not to be used for any other purpose. Using metadata and post or profile content (or their derivations) from the endpoint for any purpose other than providing a front-end view of the post or profile is strictly prohibited. This prohibition encompasses consuming, manipulating, extracting, or persisting the metadata and content, including but not limited to, deriving information about posts or profiles from the metadata for analytics purposes.
* Posts on private, inactive, and age-restricted accounts as well as geo-gated posts are not supported.
* Profiles of private, inactive, and age-restricted accounts are not supported. Profiles of users who have turned off embeds for their account are also not supported.

## Rate limits

* You can make up to 1,000 requests every hour.

## Get the embed HTML code

You can fetch the embed HTML code programmatically through the API. For posts, you can also get it from [threads.com](https://threads.com) by clicking the three dots in the top-right corner of a post and selecting **Get embed code**, or by selecting **Embed code** from the post's share menu. In the embed dialog, choose **Light**, **Dark**, or **Auto** to preview the embed, then click **Copy** to copy the embed code for the selected mode.

To get the embed HTML code using the API, send a request to the `/oembed` endpoint:

```
GET /oembed?url=<THREADS_URL>
```

* `THREADS_URL` — The URL of the Threads post or profile that you want to embed. See [URL formats](#url-formats) for the accepted formats.

Upon success, the API responds with a JSON object containing the embed HTML code and additional metadata. The embed HTML code is in the returned `html` field.

Refer to the [Threads oEmbed Reference](https://developers.facebook.com/documentation/threads/reference/oembed) for a list of query string parameters you can include to augment the request.

### Choose the embed theme

Include the optional `theme` parameter to choose `light`, `dark`, or `auto` mode. If you omit `theme`, the embed uses light mode. Auto mode follows the viewer's preferred appearance settings.

For example, add `theme=dark` to render a post embed in dark mode:

```bash
curl -s -X GET "https://graph.threads.com/v1.0/oembed?url=https://www.threads.com/@meta/post/DDzbnVKx57R&theme=dark"
```

### Example requests

Embed a post:

```bash
curl -s -X GET "https://graph.threads.com/v1.0/oembed?url=https://www.threads.com/@meta/post/DDzbnVKx57R"
```

Embed a profile:

```bash
curl -s -X GET "https://graph.threads.com/v1.0/oembed?url=https://www.threads.com/@meta"
```

### Example response

Default fields that are returned:

```json
{
  "type": "rich",
  "version": "1.0",
  "html": "<blockquote class=\"text-post-media\" data-text-post-permalink=...",
  "provider_name": "Threads",
  "provider_url": "https://www.threads.com/",
  "width": 658
}
```

Post and profile embeds return the same fields.

### URL formats

The `url` query string parameter accepts the following URL formats for posts:

```
https://www.threads.com/@{username}/post/{media-shortcode}/
```

```
https://www.threads.com/t/{media-shortcode}/
```

To embed a profile, use the following URL format:

```
https://www.threads.com/@{username}/
```

### Embed JS

The embed HTML contains a reference to the Threads embed.js JavaScript library. When the library loads, it scans the page for the embed HTML and generates the fully rendered post or profile.

```html
<script async src="https://www.threads.com/embed.js"></script>
```

### Embed size

The embedded post or profile is responsive and adapts to the size of its container. This means that the height varies depending on the container width and the length of the content. You can set the maximum width by including the `maxwidth` query string parameter in your request.

**Note:** The `maxwidth` must be between 320 and 658 pixels.