# Springfield Faith Assembly — Website

> **Live site:** [faithagspringfield.netlify.app](https://faithagspringfield.netlify.app)
> **Admin panel:** [faithagspringfield.netlify.app/admin.html](https://faithagspringfield.netlify.app/admin.html)

A modern, fully static church website for Springfield Faith Assembly (Springfield, Missouri) built with plain HTML, CSS, and JavaScript. Deployed on Netlify, managed via GitHub. No WordPress, no backend — everything is fast, free, and staff-editable through a built-in admin panel.

---

## Repository Structure

```
faithagspringfield/
├── index.html          # Main public website
├── admin.html          # Password-protected staff admin panel
├── events.json         # Upcoming events data
├── announcements.json  # Top-of-page announcement banner
├── sermons.json        # Latest sermon info (YouTube embed + details)
├── hero-bg.jpg         # (optional) Hero background photo — upload to enable
├── logo 2.png          # Primary site logo
├── logo.png / logo.svg # Alternate logo formats
└── README.md           # This file
```

---

## Website Sections

| Section | Description |
|---|---|
| **Hero** | Full-bleed header with logo, tagline, CTA buttons, and service-times strip |
| **About** | Church welcome text and values |
| **Services** | Sunday 10:30 AM and Wednesday 7:00 PM service cards |
| **Plan Your Visit** | Address, times, dress code, kids info, and Google Maps embed |
| **Ministries** | Six ministry cards (Children, Youth, Worship, Outreach, Small Groups, Women's) |
| **Events** | Dynamically loaded from `events.json` |
| **Sermons** | YouTube embed + details loaded from `sermons.json` |
| **Give** | Online giving call-to-action (update the link to your giving platform) |
| **Contact** | Address, phone, email, social links, and a contact form |
| **Footer** | Four-column footer with Quick Links, Get Involved, Contact, and social icons |

---

## Admin Panel

Navigate to `/admin.html` and log in with the admin password.

### Tabs

| Tab | What You Can Do |
|---|---|
| **Events** | Add, edit, delete upcoming events. Changes are saved locally until published. |
| **Announcement** | Toggle the top banner on/off and edit its message text. Supports basic HTML links. |
| **Sermons** | Update the featured sermon — title, series, speaker, date, YouTube video ID, description. |
| **Change Password** | Generate a new SHA-256 hash for the admin password. |

### Publishing Changes to the Live Site

The admin panel publishes directly to GitHub via the GitHub API, which triggers an automatic Netlify redeploy (~30–60 seconds).

1. Click **"Save & Publish All"** in the green bar at the top of the admin panel.
2. If prompted, enter your GitHub Personal Access Token (it saves to your browser automatically after the first time).
3. Wait about 30–60 seconds and refresh the live site.

All three JSON files (`events.json`, `announcements.json`, `sermons.json`) are published in a single click.

### Default Admin Password

```
faithag2026
```

> **To change it:** Go to the **Change Password** tab, enter your new password, copy the generated hash, then edit `admin.html` on GitHub and replace the `STORED_HASH` value near the top of the `<script>` block.

---

## GitHub Personal Access Token (Required for Publishing)

The admin panel needs a GitHub token to push JSON updates. You only need to set this up once per device/browser.

1. Go to [github.com/settings/tokens?type=beta](https://github.com/settings/tokens?type=beta)
2. Click **"Generate new token"**
3. Set the token name (e.g. *SFA Admin Panel*)
4. Set **Repository access** → Only select repositories → **faithagspringfield**
5. Under **Permissions → Repository permissions**, set:
   - **Contents** → Read and write
   - **Metadata** → Read-only (auto-selected)
6. Click **Generate token** and copy it
7. Paste it into the green **GitHub Token** field in the admin panel — it saves automatically

---

## JSON File Formats

### events.json
```json
[
  {
    "id": 1,
    "title": "Sunday Morning Worship",
    "date": "2026-04-12",
    "time": "10:30 AM",
    "category": "Worship",
    "description": "Join us for uplifting worship and biblical teaching."
  }
]
```
**Valid categories:** `Worship`, `Bible Study`, `Outreach`, `Special`, `Youth`, `Prayer`, `Children`

Events more than 7 days in the past are automatically hidden from the public site.

---

### announcements.json
```json
{
  "active": true,
  "text": "Join us this Sunday for Easter Service at 10:30 AM!"
}
```
Set `"active": false` to hide the banner. The `text` field supports basic HTML (e.g. `<a href="#events">See Events</a>`).

---

### sermons.json
```json
[
  {
    "id": 1,
    "title": "Walking in Faith",
    "series": "Faith That Works",
    "speaker": "Pastor",
    "date": "2026-04-06",
    "youtubeId": "dQw4w9WgXcQ",
    "description": "An encouraging message on walking by faith."
  }
]
```
The `youtubeId` is the part after `?v=` in a YouTube URL. Leave it blank to show a placeholder.

---

## Adding a Hero Background Photo

Upload an image named `hero-bg.jpg` to the repository root. The hero section will automatically display it with a dark overlay. Recommended size: 1920×1080px or larger, landscape orientation.

---

## Updating the Give Button

In `index.html`, find the Give section and replace the `href` in the Give Now button with your church's giving platform URL (Tithe.ly, Planning Center Giving, PayPal, etc.):

```html
<a href="https://YOUR-GIVING-LINK-HERE" target="_blank" class="btn btn-primary">
    <i class="fa-solid fa-heart"></i> Give Now
</a>
```

---

## Deployment

The site is hosted on [Netlify](https://netlify.com) with automatic deploys from the `main` branch of this repository. Any commit to `main` — including those made by the admin panel — triggers a new deploy automatically within 30–60 seconds.

---

## Tech Stack

| Layer | Technology |
|---|---|
| HTML/CSS/JS | Vanilla — no frameworks |
| Fonts | Google Fonts (Cormorant Garamond, Inter, Outfit) |
| Icons | Font Awesome 6 |
| Hosting | Netlify (free tier) |
| Source control | GitHub |
| CMS layer | GitHub Contents API + custom admin panel |
| Password security | SHA-256 via Web Crypto API (no plaintext passwords) |

---

*Last updated April 2026 — Springfield Faith Assembly, Springfield, Missouri*
