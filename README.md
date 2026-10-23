# Threads API 文件（Markdown 整理版）

> Meta 官方 [Threads API 文件](https://developers.facebook.com/documentation/threads/) 的 Markdown 副本，共 49 頁，保留官方的章節結構，方便在編輯器、Git、AI 工具與 RAG 中搜尋與引用。

- **最後同步**：2026-10-23（官方 Changelog 最新一筆：2026-08-18）
- **性質**：非官方整理，文件內容的權利屬於 Meta；實際行為請以官方網站為準。

## 快速開始

1. 先讀 [Threads API](./Threads%20API.md)（總目錄）與 [Threads API overview](./Threads%20API%20overview.md)（速率限制、圖片與影片規格）。
2. 依序讀 `Get Started/`：[Create an app for the Threads API](./Get%20Started/Create%20an%20app%20for%20the%20Threads%20API.md) → [Get Access Tokens](./Get%20Started/Get%20Access%20Tokens.md) → [Long-lived access tokens - Threads API](./Get%20Started/Long-lived%20access%20tokens%20-%20Threads%20API.md)。
3. 之後依需求查下方的「常見任務速查」。

## 常見任務速查

| 我想… | 看這份 |
| --- | --- |
| 建立 Meta app | [Create an app for the Threads API](./Get%20Started/Create%20an%20app%20for%20the%20Threads%20API.md) |
| 取得或延長 access token | [Get Access Tokens](./Get%20Started/Get%20Access%20Tokens.md)、[Long-lived access tokens - Threads API](./Get%20Started/Long-lived%20access%20tokens%20-%20Threads%20API.md)、[App Access Tokens](./Get%20Started/App%20Access%20Tokens.md) |
| 發文（單則、輪播） | [Threads Posts](./Create%20Posts/Threads%20Posts.md) |
| 回覆貼文、管理回覆 | [Create Replies](./Create%20Posts/Create%20Replies.md)、[Reply management - Threads API](./Retrieve%20and%20Manage%20Replies/Reply%20management%20-%20Threads%20API.md) |
| 讀取貼文與回覆 | [Retrieve User Posts](./Retrieve%20and%20Discover%20Posts/Retrieve%20User%20Posts.md)、[Retrieve Media Replies and Conversations](./Retrieve%20and%20Manage%20Replies/Retrieve%20Media%20Replies%20and%20Conversations.md) |
| 搜尋關鍵字或主題標籤 | [Keyword and Topic Tag Search](./Retrieve%20and%20Discover%20Posts/Keyword%20and%20Topic%20Tag%20Search.md) |
| 查看成效數據 | [Threads Insights API](./Threads%20Insights%20API.md) |
| 接收即時通知 | [Webhooks for Threads](./Webhooks%20for%20Threads.md) |
| 嵌入貼文或做分享連結 | [Embed a Threads Post](./Embed%20a%20Threads%20Post.md)、[Web Intents](./Web%20Intents.md) |
| 速率限制與媒體規格 | [Threads API overview](./Threads%20API%20overview.md) |
| 排查錯誤、檢查 token | [Threads API Troubleshooting](./Threads%20API%20Troubleshooting/Threads%20API%20Troubleshooting.md)、[Debug Access Token](./Threads%20API%20Troubleshooting/Debug%20Access%20Token.md) |
| 了解最近改了什麼 | [Threads Changelog](./Threads%20Changelog.md) |

## 目錄結構

| 資料夾 | 頁數 | 內容 |
| --- | --- | --- |
| 根目錄 | 9 | 總目錄、概覽、個人檔案、成效、Webhooks、oEmbed、Web Intents、刪除貼文、Changelog |
| [`Get Started/`](./Get%20Started) | 5 | 建立 Meta app、取得短效／長效 user token、app access token |
| [`Create Posts/`](./Create%20Posts) | 13 | 發文：單則與輪播、回覆、轉發、引用、幽靈貼文、投票、劇透、文字附件、分享到 IG 限時動態、地點標記、地理限制、無障礙 |
| [`Retrieve and Discover Posts/`](./Retrieve%20and%20Discover%20Posts) | 4 | 讀取使用者貼文、被標記（Mentions）、關鍵字與主題標籤搜尋 |
| [`Retrieve and Manage Replies/`](./Retrieve%20and%20Manage%20Replies) | 4 | 讀取回覆與對話串、隱藏回覆、控制誰能回覆、回覆審核 |
| [`Threads API Reference/`](./Threads%20API%20Reference) | 10 | 各端點與參數的參考頁（Publishing、Media Retrieval、User、Insights 等） |
| [`Threads API Troubleshooting/`](./Threads%20API%20Troubleshooting) | 2 | 疑難排解與 access token 除錯 |
| [`Tools and Resources/`](./Tools%20and%20Resources) | 2 | Postman Collection 等工具 |

## 完整索引

每一列都附官方原頁網址，方便對照。

### 根目錄

| 頁面 | 官方網址 |
| --- | --- |
| [Threads API](./Threads%20API.md) | [https://developers.facebook.com/documentation/threads](https://developers.facebook.com/documentation/threads) |
| [Threads API overview](./Threads%20API%20overview.md) | [https://developers.facebook.com/documentation/threads/overview](https://developers.facebook.com/documentation/threads/overview) |
| [Delete Posts](./Delete%20Posts.md) | [https://developers.facebook.com/documentation/threads/posts/delete-posts](https://developers.facebook.com/documentation/threads/posts/delete-posts) |
| [Threads Profiles](./Threads%20Profiles.md) | [https://developers.facebook.com/documentation/threads/threads-profiles](https://developers.facebook.com/documentation/threads/threads-profiles) |
| [Threads Insights API](./Threads%20Insights%20API.md) | [https://developers.facebook.com/documentation/threads/insights](https://developers.facebook.com/documentation/threads/insights) |
| [Webhooks for Threads](./Webhooks%20for%20Threads.md) | [https://developers.facebook.com/documentation/threads/webhooks](https://developers.facebook.com/documentation/threads/webhooks) |
| [Embed a Threads Post](./Embed%20a%20Threads%20Post.md) | [https://developers.facebook.com/documentation/threads/tools-and-resources/embed-a-threads-post](https://developers.facebook.com/documentation/threads/tools-and-resources/embed-a-threads-post) |
| [Web Intents](./Web%20Intents.md) | [https://developers.facebook.com/documentation/threads/threads-web-intents](https://developers.facebook.com/documentation/threads/threads-web-intents) |
| [Threads Changelog](./Threads%20Changelog.md) | [https://developers.facebook.com/documentation/threads/changelog](https://developers.facebook.com/documentation/threads/changelog) |

### Get Started

| 頁面 | 官方網址 |
| --- | --- |
| [Get started with the Threads API](./Get%20Started/Get%20started%20with%20the%20Threads%20API.md) | [https://developers.facebook.com/documentation/threads/get-started](https://developers.facebook.com/documentation/threads/get-started) |
| [Create an app for the Threads API](./Get%20Started/Create%20an%20app%20for%20the%20Threads%20API.md) | [https://developers.facebook.com/documentation/threads/get-started/create-an-app](https://developers.facebook.com/documentation/threads/get-started/create-an-app) |
| [Get Access Tokens](./Get%20Started/Get%20Access%20Tokens.md) | [https://developers.facebook.com/documentation/threads/get-started/get-access-tokens-and-permissions](https://developers.facebook.com/documentation/threads/get-started/get-access-tokens-and-permissions) |
| [Long-lived access tokens - Threads API](./Get%20Started/Long-lived%20access%20tokens%20-%20Threads%20API.md) | [https://developers.facebook.com/documentation/threads/get-started/long-lived-tokens](https://developers.facebook.com/documentation/threads/get-started/long-lived-tokens) |
| [App Access Tokens](./Get%20Started/App%20Access%20Tokens.md) | [https://developers.facebook.com/documentation/threads/get-started/app-access-tokens](https://developers.facebook.com/documentation/threads/get-started/app-access-tokens) |

### Create Posts

| 頁面 | 官方網址 |
| --- | --- |
| [Create Posts](./Create%20Posts/Create%20Posts.md) | [https://developers.facebook.com/documentation/threads/create-posts](https://developers.facebook.com/documentation/threads/create-posts) |
| [Threads Posts](./Create%20Posts/Threads%20Posts.md) | [https://developers.facebook.com/documentation/threads/posts](https://developers.facebook.com/documentation/threads/posts) |
| [Create Replies](./Create%20Posts/Create%20Replies.md) | [https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/create-replies](https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/create-replies) |
| [Reposts](./Create%20Posts/Reposts.md) | [https://developers.facebook.com/documentation/threads/posts/reposts](https://developers.facebook.com/documentation/threads/posts/reposts) |
| [Quote Posts](./Create%20Posts/Quote%20Posts.md) | [https://developers.facebook.com/documentation/threads/posts/quote-posts](https://developers.facebook.com/documentation/threads/posts/quote-posts) |
| [Ghost posts](./Create%20Posts/Ghost%20posts.md) | [https://developers.facebook.com/documentation/threads/create-posts/ghost-posts](https://developers.facebook.com/documentation/threads/create-posts/ghost-posts) |
| [Polls - Threads API](./Create%20Posts/Polls%20-%20Threads%20API.md) | [https://developers.facebook.com/documentation/threads/create-posts/polls](https://developers.facebook.com/documentation/threads/create-posts/polls) |
| [Spoilers](./Create%20Posts/Spoilers.md) | [https://developers.facebook.com/documentation/threads/create-posts/spoilers](https://developers.facebook.com/documentation/threads/create-posts/spoilers) |
| [Text Attachments](./Create%20Posts/Text%20Attachments.md) | [https://developers.facebook.com/documentation/threads/create-posts/text-attachments](https://developers.facebook.com/documentation/threads/create-posts/text-attachments) |
| [Share posts to Instagram Stories](./Create%20Posts/Share%20posts%20to%20Instagram%20Stories.md) | [https://developers.facebook.com/documentation/threads/create-posts/share-to-ig-stories](https://developers.facebook.com/documentation/threads/create-posts/share-to-ig-stories) |
| [Location tagging](./Create%20Posts/Location%20tagging.md) | [https://developers.facebook.com/documentation/threads/create-posts/location-tagging](https://developers.facebook.com/documentation/threads/create-posts/location-tagging) |
| [Geo-Gated Content](./Create%20Posts/Geo-Gated%20Content.md) | [https://developers.facebook.com/documentation/threads/posts/geo-gating](https://developers.facebook.com/documentation/threads/posts/geo-gating) |
| [Accessibility - Threads API](./Create%20Posts/Accessibility%20-%20Threads%20API.md) | [https://developers.facebook.com/documentation/threads/posts/accessibility](https://developers.facebook.com/documentation/threads/posts/accessibility) |

### Retrieve and Discover Posts

| 頁面 | 官方網址 |
| --- | --- |
| [Retrieve and Discover Posts](./Retrieve%20and%20Discover%20Posts/Retrieve%20and%20Discover%20Posts.md) | [https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts) |
| [Retrieve User Posts](./Retrieve%20and%20Discover%20Posts/Retrieve%20User%20Posts.md) | [https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts](https://developers.facebook.com/documentation/threads/retrieve-and-discover-posts/retrieve-posts) |
| [Mentions - Threads API](./Retrieve%20and%20Discover%20Posts/Mentions%20-%20Threads%20API.md) | [https://developers.facebook.com/documentation/threads/threads-mentions](https://developers.facebook.com/documentation/threads/threads-mentions) |
| [Keyword and Topic Tag Search](./Retrieve%20and%20Discover%20Posts/Keyword%20and%20Topic%20Tag%20Search.md) | [https://developers.facebook.com/documentation/threads/keyword-search](https://developers.facebook.com/documentation/threads/keyword-search) |

### Retrieve and Manage Replies

| 頁面 | 官方網址 |
| --- | --- |
| [Retrieve and Manage Replies](./Retrieve%20and%20Manage%20Replies/Retrieve%20and%20Manage%20Replies.md) | [https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies](https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies) |
| [Retrieve User Replies](./Retrieve%20and%20Manage%20Replies/Retrieve%20User%20Replies.md) | [https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/retrieve-replies](https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/retrieve-replies) |
| [Retrieve Media Replies and Conversations](./Retrieve%20and%20Manage%20Replies/Retrieve%20Media%20Replies%20and%20Conversations.md) | [https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/replies-and-conversations](https://developers.facebook.com/documentation/threads/retrieve-and-manage-replies/replies-and-conversations) |
| [Reply management - Threads API](./Retrieve%20and%20Manage%20Replies/Reply%20management%20-%20Threads%20API.md) | [https://developers.facebook.com/documentation/threads/reply-management](https://developers.facebook.com/documentation/threads/reply-management) |

### Threads API Reference

| 頁面 | 官方網址 |
| --- | --- |
| [Threads API Reference](./Threads%20API%20Reference/Threads%20API%20Reference.md) | [https://developers.facebook.com/documentation/threads/reference](https://developers.facebook.com/documentation/threads/reference) |
| [Publish with the Threads API](./Threads%20API%20Reference/Publish%20with%20the%20Threads%20API.md) | [https://developers.facebook.com/documentation/threads/reference/publishing](https://developers.facebook.com/documentation/threads/reference/publishing) |
| [Media Retrieval](./Threads%20API%20Reference/Media%20Retrieval.md) | [https://developers.facebook.com/documentation/threads/reference/media-retrieval](https://developers.facebook.com/documentation/threads/reference/media-retrieval) |
| [Reply management (reference) - Threads API](./Threads%20API%20Reference/Reply%20management%20%28reference%29%20-%20Threads%20API.md) | [https://developers.facebook.com/documentation/threads/reference/reply-management](https://developers.facebook.com/documentation/threads/reference/reply-management) |
| [User](./Threads%20API%20Reference/User.md) | [https://developers.facebook.com/documentation/threads/reference/user](https://developers.facebook.com/documentation/threads/reference/user) |
| [Locations](./Threads%20API%20Reference/Locations.md) | [https://developers.facebook.com/documentation/threads/reference/locations](https://developers.facebook.com/documentation/threads/reference/locations) |
| [Location Search](./Threads%20API%20Reference/Location%20Search.md) | [https://developers.facebook.com/documentation/threads/reference/location-search](https://developers.facebook.com/documentation/threads/reference/location-search) |
| [Threads API insights](./Threads%20API%20Reference/Threads%20API%20insights.md) | [https://developers.facebook.com/documentation/threads/reference/insights](https://developers.facebook.com/documentation/threads/reference/insights) |
| [oEmbed](./Threads%20API%20Reference/oEmbed.md) | [https://developers.facebook.com/documentation/threads/reference/oembed](https://developers.facebook.com/documentation/threads/reference/oembed) |
| [Debug](./Threads%20API%20Reference/Debug.md) | [https://developers.facebook.com/documentation/threads/reference/debug](https://developers.facebook.com/documentation/threads/reference/debug) |

### Threads API Troubleshooting

| 頁面 | 官方網址 |
| --- | --- |
| [Threads API Troubleshooting](./Threads%20API%20Troubleshooting/Threads%20API%20Troubleshooting.md) | [https://developers.facebook.com/documentation/threads/troubleshooting](https://developers.facebook.com/documentation/threads/troubleshooting) |
| [Debug Access Token](./Threads%20API%20Troubleshooting/Debug%20Access%20Token.md) | [https://developers.facebook.com/documentation/threads/troubleshooting/debug-access-token](https://developers.facebook.com/documentation/threads/troubleshooting/debug-access-token) |

### Tools and Resources

| 頁面 | 官方網址 |
| --- | --- |
| [Tools and Resources](./Tools%20and%20Resources/Tools%20and%20Resources.md) | [https://developers.facebook.com/documentation/threads/tools-and-resources](https://developers.facebook.com/documentation/threads/tools-and-resources) |
| [Threads API Postman Collection](./Tools%20and%20Resources/Threads%20API%20Postman%20Collection.md) | [https://developers.facebook.com/documentation/threads/tools-and-resources/postman-collection](https://developers.facebook.com/documentation/threads/tools-and-resources/postman-collection) |

## 命名與格式

- **檔名等於該頁的官方標題**（頁面的 H1，含大小寫），例如 `Polls - Threads API.md`、`Ghost posts.md`。官方改標題時，檔名也跟著改。
- 內容與官方 Markdown 相同，只做兩件事：還原 HTML 實體（例如 `&lt;` 還原為 `<`），以及移除每頁結尾的「Full documentation index」提示行。
- 檔案使用 LF 換行。在 Windows 上，Git 依 `core.autocrlf` 設定自動轉換。

## 如何更新

官方站把每一頁都以原始 Markdown 提供：在頁面網址後加 `.md` 即可取得，頁面清單則在 `llms.txt`。

```bash
# 頁面清單（目前為 49 頁）
curl -sL https://developers.facebook.com/documentation/threads/llms.txt

# 單頁原始 Markdown，例如 Changelog
curl -sL https://developers.facebook.com/documentation/threads/changelog.md
```

1. 先看 [Threads Changelog](./Threads%20Changelog.md) 與 `llms.txt`，判斷有沒有新增、移除或改名的頁面。
2. 逐頁下載 `.md`，依上一節的規則處理後，與本 repo 的檔案比對，只更新有差異的檔案。
3. 標題有變動的頁面，檔名一併改成新標題。
4. 同步後更新本文件開頭的「最後同步」日期，並確認頁數與 `llms.txt` 一致。

## 聲明

- 本 repo 為個人整理的非官方副本，與 Meta 無關，也未獲其背書。
- 文件內容的著作權與相關權利屬於 Meta；本 repo 尚未另行附上授權條款。
- 官方文件會持續更新，副本可能落後，正式開發前請對照官方網站。
