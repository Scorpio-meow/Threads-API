# oEmbed



The Threads oEmbed endpoint allows you to embed a public Threads post or profile in external websites and apps. See [Embed a Threads post](https://developers.facebook.com/documentation/threads/tools-and-resources/embed-a-threads-post) for more information.

## `GET /oembed?url=...`

Retrieve the embed HTML code snippet and metadata of a post or profile.

### Parameters

| Name | Description |
| --- | --- |
| `url`<br><br>URL string | **Required.**  <br>Permanent link to the post or profile on Threads.<br><br>**Accepted formats:**<br><br>* `https://www.threads.com/@{username}/post/{media-shortcode}`<br>* `https://www.threads.com/t/{media-shortcode}`<br>* `https://www.threads.com/@{username}`<br><br>**Examples:**<br><br>* https://www.threads.com/@meta/post/DDzbnVKx57R<br>* https://www.threads.com/t/DDzbnVKx57R<br>* https://www.threads.com/@meta |
| `maxwidth`<br><br>int | **Optional.**  <br>Maximum width of returned media. Must be between 320 and 658 pixels.  <br>**Note:** The `maxheight` parameter is not supported because the embed code is responsive and its height varies depending on its width. |
| `theme`<br><br>string | **Optional.**  <br>Display mode for the embed. Accepted values:<br><br>* `light`: Always use light mode. This is the default if you omit `theme`.<br>* `dark`: Always use dark mode.<br>* `auto`: Automatically use light or dark mode based on the viewer's preferred appearance settings. |

### Fields

| Name | Description |
| --- | --- |
| `html`<br><br>string | The HTML used to display the post or profile. |
| `provider_name`<br><br>string | Name of the provider (Threads). |
| `provider_url`<br><br>URL string | URL of the provider ([https://www.threads.com/](https://www.threads.com/)). |
| `type`<br><br>string | The oEmbed resource type. See [https://oembed.com/](https://oembed.com/). |
| `version`<br><br>string | Always `1.0`. See [https://oembed.com/](https://oembed.com/). |
| `width`<br><br>int | The width in pixels required to display the HTML. |