# Threads poll attachments



You can use the Threads API to create posts with polls.

## Permissions

Publishing posts with polls requires the following permissions:

* `threads_basic` — Required for making any calls to all Threads API endpoints.
* `threads_content_publish` — Required for Threads publishing endpoints only.

If your app has not been approved for advanced access for the `threads_content_publish` permission, you can only post on behalf of [Threads testers](https://developers.facebook.com/documentation/threads/get-started#threads-testers) on your app. After your app is published and approved, you can post on behalf of any Threads user who grants your app the permission.

## Limitations

* You can attach polls only to text-only posts.

## Create a post with a poll

You can attach a poll when making a request to the `POST /threads` endpoint to create a media object. Include the following parameter in your request:

* `poll_attachment` — A JSON object containing the options for the poll.

The `poll_attachment` object must be of the form:

```json
{
  "option_a": "first option",
  "option_b": "second option",
  "option_c": "third option", // Optional
  "option_d": "fourth option" // Optional
}
```

The `poll_attachment` object must contain at least 2 options and no more than 4 options. Each option must be between 1 and 25 characters long.

### Example request

```bash
curl -i -X POST \
"https://graph.threads.com/v1.0/<THREADS_USER_ID>/threads?media_type=TEXT&text=MyText&access_token=<ACCESS_TOKEN>" \
-d poll_attachment='{"option_a":"first option", "option_b":"second option"}'
```

### Example response

```json
{
  "id": "1234567" // Threads Media Container ID
}
```

The request above creates a Threads media container. After you [publish](https://developers.facebook.com/documentation/threads/posts#step-2-publish-the-threads-media-container) it, the post contains a poll attachment with the provided options.

## Media retrieval

Make a request to the `GET /threads` or `GET /{threads-media-id}` endpoint to retrieve media objects. Make sure to include the following field with your API request:

* `poll_attachment` — The poll attachment for the post.

### Example request

```bash
curl -i -G \
"https://graph.threads.com/v1.0/<THREADS_MEDIA_ID>?access_token=<ACCESS_TOKEN>" \
-d "fields=id,poll_attachment{option_a,option_b,option_c,option_d,option_a_votes_percentage,option_b_votes_percentage,option_c_votes_percentage,option_d_votes_percentage,total_votes,expiration_timestamp}"
```

### Example response

```json
{
  "id": "1234567", // Threads Media ID
  "poll_attachment": {
    "option_a": "first option",
    "option_b": "second option",
    "option_c": "third option",
    "option_d": "fourth option",
    "option_a_votes_percentage": 0.10, // Percentage of votes for first option
    "option_b_votes_percentage": 0.20,
    "option_c_votes_percentage": 0.15,
    "option_d_votes_percentage": 0.55,
    "total_votes": 100,
    "expiration_timestamp": "2025-01-01T23:00:00+0000" // Time when the poll expires
  }
}
```

**Note:** The API returns the fields for option C and option D only when they are available for the poll being retrieved.