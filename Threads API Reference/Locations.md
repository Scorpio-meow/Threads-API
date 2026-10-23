# Locations



You can retrieve Threads location objects by individual ID. See [Location Tagging](https://developers.facebook.com/documentation/threads/create-posts/location-tagging) for more information.

## `GET /{location-id}`

Retrieve a location by its ID.

| Name | Description |
| --- | --- |
| `access_token`<br><br>string | **Required.**<br>Threads Graph API user access token. |
| `location-id`<br><br>string | **Required.**<br>The path parameter of the Threads location identifier. |
| `fields`<br><br>string | **Optional.**  <br>A comma-separated list of the fields to be returned.<br>**Values:** `id` *(default)*, `name`, `address`, `city`, `country`, `latitude`, `longitude`, `postal_code` |