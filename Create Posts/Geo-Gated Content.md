# Geo-Gated Content



You can use the Threads API to create geo-gated content restricted to one or more specific countries. Content marked in this way will only be shown to Threads profiles in those countries.

## Permissions

Publishing geo-gated content requires the following permissions:

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_content_publish` — Required for Threads publishing endpoints only.

If your app has not been approved for advanced access for the `threads_content_publish` permission, you can only post on behalf of [Threads testers](https://developers.facebook.com/documentation/threads/get-started#threads-testers) on your app. After your app is published and approved, you can post on behalf of any Threads user who grants your app the permission.

### Limitations

Only users with access to this feature on threads.com can use this feature via Threads API.

## User Eligibility

A user's eligibility for the geo-gating feature can be retrieved when making a request to the `GET /me` or `GET /{threads-user-id}` endpoints to [retrieve profile information](https://developers.facebook.com/documentation/threads/threads-profiles#retrieve-a-threads-user-s-profile-information). To retrieve this value, include the following parameter with your API request:

* `is_eligible_for_geo_gating` - A boolean value which represents whether a user is eligible for the geo-gating feature.

### Example Request

```
curl -s -X GET \
  "https://graph.threads.com/v1.0/me?fields=id,is_eligible_for_geo_gating&access_token=<ACCESS_TOKEN>"
```

### Example Response

```
{
   "id": "12312312312123",
   "is_eligible_for_geo_gating": true
}
```

This means that this user has access to the geo-gating feature.

## Publish Geo-Gated Content

Geo-gating can be used when making a request to the `POST /threads` endpoint to [create a media object](https://developers.facebook.com/documentation/threads/posts#step-1--create-a-threads-media-container). To use geo-gating, include the following parameter with your API request:

* `allowlisted_country_codes` - A string list of valid [ISO 3166-1 alpha-2 country codes](https://www.iso.org/obp/ui/#search) that represents the countries where this media should be shown. If this parameter is passed in, the media will not be shown to Threads profiles in countries outside of this list.

### Example Request

```
curl -i -X POST \
  "https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads?media_type=IMAGE&image_url=https://www.example.com/images/bronz-fonz.jpg&text=#BronzFonz&allowlisted_country_codes=US,CA&access_token=<ACCESS_TOKEN>"
```

This request would create a Threads post container that, once published, is only visible in the United States and Canada.

**Note:** The creator of a Threads post is always able to see their content, regardless of geo-gating settings.

## Media Retrieval

Allowlisted country codes for geo-gating can be retrieved when making a request to the `GET /threads` or `GET /{threads_media_id}` endpoint to [retrieve media object(s)](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts). To retrieve the geo-gating allowlist, include the following parameter with your API request:

* `allowlisted_country_codes` - A string list of valid [ISO 3166-1 alpha-2 country codes](https://www.iso.org/obp/ui/#search) that represents the countries where this media is shown.

### Example Request

```
curl -s -X GET \
  "https://graph.threads.com/v1.0/me/threads?fields=id,allowlisted_country_codes&limit=1&access_token=<ACCESS_TOKEN>"
```

### Example Response

```
{
   "id": "12312312312123",
   "allowlisted_country_codes": [
      "US"
   ]
}
```

This means this media is only shown to users in the United States.

## Error Codes

| Error | Description |
| --- | --- |
| `ErrorCode::THREADS_API__FEATURE_NOT_AVAILABLE` | This user does not have access to this Threads API feature. |
| `ErrorCode::THREADS_API__GEO_GATING_INVALID_COUNTRY_CODES` | Some of the specified country code(s) are not supported for geo-gating. |