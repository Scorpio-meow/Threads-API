# Webhooks for Threads



Webhooks for Threads allow you to receive real-time notifications for the subscribed topics and fields.

## Receive live webhook notifications

To receive live webhook notifications, the following conditions must be satisfied:

- Your app must have Threads webhooks added as a sub-use case and appropriate fields subscribed to in the App Dashboard.

- For non-tech providers, the apps must be in [Live mode](https://developers.facebook.com/documentation/development/build-and-test/app-modes).

- For tech providers, the apps must have permissions with an [advanced access level](https://developers.facebook.com/documentation/development/graph-api/overview/access-levels). You can request advanced access for permissions as shown here:

If the app permissions do not have advanced access, the app does not receive webhook notifications.

- The app user must have granted your app appropriate permissions (that is, `threads_basic`, `threads_read_replies` for reply webhooks).

- The business connected to the app must be verified.

- To receive real-time [reply](#real-time-reply-notifications) and [mention](#real-time-mention-notifications) notifications, the owner of the media object upon which the webhook event occurs must not have set their account to private.

- To receive real-time [delete](#real-time-delete-notifications) and [publish](#real-time-publish-notifications) notifications, the owner of the media object upon which the webhook event occurs must be a public account or private account that authenticated to the app.

### Limitations

* Apps do not receive webhook notifications if the media where the reply or mention appears was created by a private account.
* Your app must have successfully completed App Review ([advanced access](https://developers.facebook.com/documentation/development/graph-api/overview/access-levels)) to receive webhook notifications for all of the fields.

### Step 0: [Optional] Use the sample app to test your integration

Download the [webhooks sample app](https://github.com/fbsamples/graph-api-webhooks-samples/) to test your integration.

### Step 1: Add the webhooks sub-use case to the main Threads API use case

Under **Use Cases** > **Customize** > **Settings**, add the **Get real-time notifications with Threads Webhooks** sub-use case.

### Step 2: Create an endpoint and configure Threads webhooks

[Create an endpoint](https://developers.facebook.com/docs/graph-api/webhooks/getting-started) that accepts and processes webhooks. To add the configuration:

1. Select the desired topic, and click **Subscribe to this object**.
2. Set the callback URL and token.

The token here is passed to your server defined in the callback URL to allow verification that the call originates from Meta servers.

#### Webhook topics

##### Moderate topic fields

| Name | Description |
| --- | --- |
| `replies` | [Replies](https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/replies-and-conversations#a-threads-replies) on a [Threads post](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts) owned by the authenticated user.  <br>**Required permission(s):** [`threads_basic`](https://developers.facebook.com/documentation/development/permissions#threads_basic), [`threads_read_replies`](https://developers.facebook.com/documentation/development/permissions#threads_read_replies) |
| `delete` | Threads posts that were [deleted](https://developers.facebook.com/documentation/threads/posts/delete-posts) by the authenticated user.  <br>**Required permissions:** [`threads_basic`](https://developers.facebook.com/documentation/development/permissions#threads_basic), [`threads_delete`](https://developers.facebook.com/documentation/development/permissions#threads_delete) |

##### Interaction topic fields

| Name | Description |
| --- | --- |
| `mentions` | [Mentions](https://developers.facebook.com/documentation/threads/threads-mentions) on a public [Threads post](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts) tagging the authenticated user.  <br>**Required permission(s):** [`threads_basic`](https://developers.facebook.com/documentation/development/permissions#threads_basic), [`threads_manage_mentions`](https://developers.facebook.com/documentation/development/permissions#threads_manage_mentions)  <br>**Optional permission(s):** [`threads_read_replies`](https://developers.facebook.com/documentation/development/permissions#threads_read_replies) — required for the `has_replies`, `is_reply`, `replied_to`, and `root_post` fields. Without this permission, these fields are removed from the webhook response. |
| `publish` | Threads posts that were [published](https://developers.facebook.com/documentation/threads/posts) by the authenticated user (including replies to the user's or others' posts).  <br>**Required permissions:** `threads_basic` |

## Notification formats

### Fields

| Name | Description |
| --- | --- |
| `app_id` | The Threads app ID displayed in **App Dashboard** > **App settings** > **Basic** > **Threads App ID**. |
| `topic` | Name of the webhook topic.  <br>Threads supports moderate and interaction topics. |
| `target_id` | The media's ID for a `replies` or `delete` webhook, or the mentioned Threads user's app-scoped user ID for a `mentions` webhook. |
| `time` | Time when the real-time notification is sent. |
| `subscription_id` | The subscription ID for the user in the webhook. |
| `id` | The media's ID. |
| `deleted_at` | Time when the post was deleted in ISO 8601 format. |
| `timestamp` | Time when the post was published in ISO 8601 format. |

### Real-time reply notifications

If you subscribe to the `replies` field, your endpoint receives a webhook notification containing the reply object.

#### Example replies payload {#sample-replies-payload}

```json
{
  "app_id": "123456",
  "topic": "moderate",
  "target_id": "78901",
  "time": 1723226877,
  "subscription_id": "234567",
  "has_uid_field": false,
  "values": {
    "value": {
      "id": "8901234",
      "username": "test_username",
      "text": "Reply",
      "media_type": "TEXT_POST",
      "permalink": "https:\/\/www.threads.com\/@test_username\/post\/Pp",
      "replied_to": {
        "id": "567890"
      },
      "root_post": {
        "id": "123456",
        "owner_id": "123456",
        "username": "test_username_2"
      },
      "shortcode": "Pp",
      "timestamp": "2024-08-07T10:33:16+0000"
    },
    "field": "replies"
  }
}
```

**Note:** Additional fields not listed in this sample response that are returned when applicable include `is_verified` and `profile_picture_url`.

### Real-time mention notifications

If you subscribe to the `mentions` field, Threads will send your endpoint a webhook notification containing the media object in which the user is mentioned.

#### Example mentions payload {#sample-mentions-payload}

```json
{
  "app_id": "123456",
  "topic": "interaction",
  "target_id": "78901",
  "time": 1723226877,
  "subscription_id": "234567",
  "has_uid_field": false,
  "values": {
    "value": {
      "id": "8901234",
      "alt_text": "test alt text",
      "gif_url": "https://media2.giphy.com/media/v1.Y2lkPTA1NzQyMTNjd2R0MXcybjZ6bDNyam9qaXJsN3RicnVncnFsanJ2dGk3eDJiejRmbyZlcD12MV9naWZzX2dpZklkJmN0PWc/3o85xEFRBYvAnamJnG/200.gif",
      "has_replies": true,
      "is_quote_post": false,
      "is_reply": false,
      "media_product_type": "THREADS",
      "media_type": "TEXT_POST",
      "permalink": "https:\/\/www.threads.com\/@test_username\/post\/Pp",
      "shortcode": "Pp",
      "text": "Reply",
      "timestamp": "2024-08-07T10:33:16+0000",
      "username": "test_username"
    },
    "field": "mentions"
  }
}
```

**Note:** Additional fields not listed in this sample response that are returned when applicable include `media_url`, `poll_attachment`, `quoted_post`, `replied_to`, `reposted_post`, `root_post`, `is_verified`, `profile_picture_url`, and `thumbnail_url`.

### Real-time delete notifications

If you subscribe to the `delete` field, Threads will send your endpoint a webhook notification containing the media object when it is deleted.

#### Example delete payload {#sample-delete-payload}

```json
{
  "app_id": "123456",
  "topic": "moderate",
  "target_id": "78901",
  "time": 1723226877,
  "subscription_id": "234567",
  "has_uid_field": false,
  "values": {
    "value": {
      "id": "8901234",
      "owner": {
        "owner_id": "78901"
      },
      "deleted_at": "2024-08-07T10:33:16+0000",
      "timestamp": "2024-08-07T10:33:16+0000",
      "username": "test_username"
    },
    "field": "delete"
  }
}
```

### Real-time publish notifications

If you subscribe to the `publish` field, Threads will send your endpoint a webhook notification containing the media object when it is published (including replies to the user's or others' posts).

#### Example publish payload {#sample-publish-payload}

```json
{
  "app_id": "123456",
  "topic": "interaction",
  "target_id": "78901",
  "time": 1723226877,
  "subscription_id": "234567",
  "has_uid_field": false,
  "values": {
    "value": {
      "id": "8901234",
      "media_type": "TEXT_POST",
      "permalink": "https:\/\/www.threads.com\/@test_username\/post\/Pp",
      "timestamp": "2024-08-07T10:33:16+0000",
      "username": "test_username"
    },
    "field": "publish"
  }
}
```