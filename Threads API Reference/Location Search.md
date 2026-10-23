# Location Search



The Threads location search endpoint allows you to search for locations which can then be tagged in Threads posts. See [Location Tagging](https://developers.facebook.com/documentation/threads/create-posts/location-tagging) for more information.

## `GET /location_search`

Search for locations by query or by coordinates.

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**  <br>Threads Graph API user access token. |
| `query`<br><br>string | **Optional.**  <br>The query string to search for. |
| `latitude`<br><br>float | **Optional.**  <br>The latitude coordinate to search for. This must be used with `longitude`. |
| `longitude`<br><br>float | **Optional.**  <br>The longitude coordinate to search for. This must be used with `latitude`. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.  <br>**Values:** `id` *(default)*, `name`, `address`, `city`, `country`, `latitude`, `longitude`, `postal_code` |