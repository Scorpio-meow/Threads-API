# oEmbed



You can retrieve the embed HTML code and associated metadata of public Threads posts.

## `GET /oembed?url=...`

Retrieve the embed HTML of a public Threads post. See [Embed a Threads Post](https://developers.facebook.com/documentation/threads/tools-and-resources/embed-a-threads-post) for more information.

### Parameters

| Name | Description |
| --- | --- |
| `url`<br><br>string | **Required.**  <br>Permanent link to the post on Threads.<br><br>**Accepted formats:**<br><br>* `https://www.threads.com/@{username}/post/{media-shortcode}`<br>* `https://www.threads.com/t/{media-shortcode}`<br><br>**Examples:**<br><br>* https://www.threads.com/@meta/post/DDzbnVKx57R<br>* https://www.threads.com/t/DDzbnVKx57R |
| `maxwidth`<br><br>int64 | **Optional.**  <br>Maximum width of returned media. Must be between 320 and 658. **Note:** The `maxheight` parameter is not supported because the embed code is responsive and its height varies depending on its width. |

### Fields

| Name | Description |
| --- | --- |
| `html`<br><br>string | The HTML used to display the post. |
| `provider_name`<br><br>string | Name of the provider (Threads). |
| `provider_url`<br><br>string | URL of the provider ([https://www.threads.com/](https://www.threads.com/)). |
| `type`<br><br>string | The oEmbed resource type. See [https://oembed.com/](https://oembed.com/). |
| `version`<br><br>string | Always 1.0. See [https://oembed.com/](https://oembed.com/). |
| `width`<br><br>int32 | The width in pixels required to display the HTML. |