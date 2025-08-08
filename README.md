# wordpress-rest-api-post-guide
Comprehensive guide for creating posts in WordPress via the REST API, including all parameters, detailed descriptions, and examples for developers.


# WordPress REST API – Required Parameters for Creating a Post

| Parameter | Type | Description | Example |
|-----------|------|-------------|---------|
| `title` | string | The title of the post. This is displayed as the main heading of the post. | `"My First API Post"` |
| `content` | string | The main body of the post. Can include HTML or plain text. | `"<p>This is the post body content</p>"` |
| `status` | string | The publication status of the post. Common values: `"publish"`, `"draft"`, `"pending"`. | `"publish"` |
| `date` | string (ISO8601) | The date and time to publish the post, in ISO8601 format. If not set, current date/time is used. | `"2025-08-08T14:30:00"` |
| `slug` | string | The URL-friendly version of the post title. If not set, it is auto-generated from the title. | `"my-first-api-post"` |


# WordPress REST API – Create Post Parameters Guide

This document explains all parameters you can send to the `POST /wp/v2/posts` endpoint when creating a post via the WordPress REST API, with examples for each.

---

## Basic Post Fields

| Parameter | Type | Required? | Description | Example |
|-----------|------|-----------|-------------|---------|
| title | string / object | Yes | The title of the post. Can be plain text or an object with `raw` & `rendered` fields. | `"title": "My First API Post"` |
| content | string / object | Yes | Main body content of the post. Can include HTML. | `"content": "<p>This is my content.</p>"` |
| excerpt | string / object | No | Short summary of the post. Useful for previews. | `"excerpt": "This is a short preview."` |
| status | string | No | Post status: `publish`, `draft`, `pending`, `private`, `future`. | `"status": "publish"` |
| slug | string | No | URL-friendly post name. If omitted, generated from title. | `"slug": "my-first-api-post"` |

---

## Date and Time Fields

| Parameter | Type | Required? | Description | Example |
|-----------|------|-----------|-------------|---------|
| date | string (ISO 8601) | No | Publish date in site’s timezone. | `"date": "2025-08-08T15:30:00"` |
| date_gmt | string (ISO 8601) | No | Publish date in GMT. | `"date_gmt": "2025-08-08T10:00:00"` |
| modified | string (ISO 8601) | No | Last modified date. | `"modified": "2025-08-09T12:00:00"` |
| modified_gmt | string (ISO 8601) | No | Last modified date in GMT. | `"modified_gmt": "2025-08-09T06:30:00"` |

---

## Taxonomy and Relationships

| Parameter | Type | Required? | Description | Example |
|-----------|------|-----------|-------------|---------|
| categories | array<int> | No | Array of category IDs. | `"categories": [1, 3]` |
| tags | array<int> | No | Array of tag IDs. | `"tags": [5, 8]` |
| author | integer | No | ID of the post’s author. | `"author": 2` |

---

## Media and Appearance

| Parameter | Type | Required? | Description | Example |
|-----------|------|-----------|-------------|---------|
| featured_media | integer | No | ID of the featured image. | `"featured_media": 123` |
| template | string | No | Theme template to use. | `"template": "custom-template.php"` |
| format | string | No | Post format: `standard`, `aside`, `gallery`, `image`, `link`, `quote`, `status`, `video`, `audio`, `chat`. | `"format": "video"` |
| sticky | boolean | No | Whether to stick the post to the top. | `"sticky": true` |

---

## Discussion Settings

| Parameter | Type | Required? | Description | Example |
|-----------|------|-----------|-------------|---------|
| comment_status | string | No | `open` or `closed` for comments. | `"comment_status": "open"` |
| ping_status | string | No | `open` or `closed` for pingbacks. | `"ping_status": "closed"` |

---

## Security and Visibility

| Parameter | Type | Required? | Description | Example |
|-----------|------|-----------|-------------|---------|
| password | string | No | Password to protect the post. | `"password": "mypassword123"` |
| private | boolean | No | Whether post visibility is private. | `"private": true` |

---

## Custom Data

| Parameter | Type | Required? | Description | Example |
|-----------|------|-----------|-------------|---------|
| meta | object | No | Custom meta fields as key-value pairs. | `"meta": { "_seo_title": "SEO Title Example" }` |
| menu_order | integer | No | Custom sort order for hierarchical post types (like pages). | `"menu_order": 5` |

---

## System Fields (Auto-handled by WordPress)

| Parameter | Type | Required? | Description | Example |
|-----------|------|-----------|-------------|---------|
| guid | string | No | Unique ID for the post. Auto-generated. | `"guid": "https://example.com/?p=101"` |
| permalink_template | string | No | Template for permalink structure. | `"permalink_template": "/%year%/%postname%/"` |
| generated_slug | string | No | Auto-generated slug if `slug` is empty. | `"generated_slug": "auto-generated-slug"` |

---

## Example Request (Full JSON)

```json
{
  "title": "My First API Post",
  "content": "<p>Hello from the REST API!</p>",
  "excerpt": "This is a short preview.",
  "status": "publish",
  "slug": "my-first-api-post",
  "date": "2025-08-08T15:30:00",
  "categories": [2],
  "tags": [5, 8],
  "author": 1,
  "featured_media": 123,
  "comment_status": "open",
  "ping_status": "closed",
  "sticky": false,
  "format": "standard",
  "password": "",
  "meta": { "_custom_key": "Custom Value" },
  "menu_order": 0
}
```
---

## Example Request (cURL)

```curl -X POST https://example.com/wp-json/wp/v2/posts \
-u username:application_password \
-H "Content-Type: application/json" \
-d '{
  "title": "My First API Post",
  "content": "<p>Hello from the REST API!</p>",
  "status": "publish",
  "categories": [2],
  "tags": [5, 8],
  "featured_media": 123
}'
```
