---

title: Newsletter
published: true
---

# Newsletter

PlatformKit includes a newsletter system for building an email subscriber list and sending broadcast messages — powered by Supabase Edge Functions.

## How it works

1. **Signup form** — a section on your site where visitors enter their email.
2. **Double opt-in** — a confirmation email is sent; the subscriber clicks a link to verify.
3. **Subscriber management** — view and manage your list in the CMS admin panel.
4. **Broadcasts** — compose and schedule email campaigns from the CMS.

## Setup

The newsletter requires a running [Supabase](/docs/deployment/supabase) instance (local or hosted). The following edge functions handle the workflow:

| Function                 | Endpoint                      | Purpose                         |
| ------------------------ | ----------------------------- | ------------------------------- |
| `newsletter-signup`      | `POST /newsletter-signup`     | Public subscribe endpoint       |
| `newsletter-confirm`     | `GET /newsletter-confirm`     | Email confirmation link handler |
| `newsletter-admin`       | Various                       | Manage subscribers & broadcasts |
| `newsletter-send`        | Internal                      | Batch send scheduled broadcasts |
| `newsletter-cron`        | Internal                      | Scheduled job runner            |
| `newsletter-unsubscribe` | `GET /newsletter-unsubscribe` | Unsubscribe link handler        |
| `newsletter-view`        | `GET /newsletter-view/:id`    | Public archive view             |

## Enabling the newsletter tab

In your theme or override config, ensure the newsletter section is enabled. In the CMS, toggle the **Newsletter** tab to visible and configure the label and icon.

## Composing a broadcast

1. Open the CMS and navigate to the **Newsletter** section.
2. Click **Compose** to open the editor drawer.
3. Write your message (supports rich text).
4. Set a send date or send immediately.
5. Click **Send** — the broadcast is queued and delivered in batches.

## Confirmation flow

When a visitor subscribes:

1. They enter their email on the signup form.
2. A confirmation email is sent with a verification link.
3. The link routes to `/confirmed` on your site, which shows:
   - ✅ **Success** — subscription confirmed
   - ⏰ **Expired** — link has expired, please re-subscribe
   - ❌ **Error** — something went wrong

## Archive

Past newsletters can be viewed at `/newsletter/:id`, giving subscribers a web-based archive of all sent emails.
