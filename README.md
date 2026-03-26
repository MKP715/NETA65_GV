# NETA 65 Grapevine / La Viña Committee Website

A single-page website for the Northeast Texas Area 65 Grapevine and La Viña Committee.
Everything lives in **one file** (`index.html`) — no special software needed.

---

## How This Website Works

The entire website is a single HTML file. All the content you'll ever need to update is stored in clearly labeled lists near the top of that file. You edit those lists, save the file, and the website updates automatically.

**You do NOT need to know how to code.** You just need to follow the patterns shown below — copy an existing entry, change the text, and save.

---

## What You Need

- **A text editor** — Notepad (Windows), TextEdit (Mac), or VS Code all work
- **Internet connection** — the site loads fonts and icons from the web
- **Google Drive** (optional) — for storing and sharing documents and photos

---

## Quick Start

1. Open `index.html` in your text editor
2. Find the section marked `CONFIGURATION — EDIT THESE ARRAYS TO UPDATE THE SITE`
3. Make your changes following the instructions below
4. Save the file
5. Double-click `index.html` to preview in your browser
6. When satisfied, push to GitHub (or ask someone who can)

---

## Google Drive Setup

All documents (PDFs) and photos can be stored in Google Drive. Here's how:

### Step 1 — Create Folders in Google Drive

Create a shared folder structure like this:

```
GV_NETA65 (shared folder)
├── reports/     ← monthly committee reports
├── notes/       ← meeting notes
├── slides/      ← meeting slide decks
├── flyers/      ← event flyer PDFs
└── photos/      ← booth and event photos
```

### Step 2 — Set Sharing Permissions

For each folder:
1. Right-click the folder in Google Drive
2. Click **Share**
3. Under "General access," change to **"Anyone with the link"**
4. Set permission to **"Viewer"**
5. Click **Copy link**

### Step 3 — Add Folder Links to the Website

Open `index.html` and find this section near the top:

```js
const GOOGLE_DRIVE = {
  reports: "",   // folder link for monthly reports
  notes:   "",   // folder link for meeting notes
  slides:  "",   // folder link for slide decks
  flyers:  "",   // folder link for event flyers
  photos:  "",   // folder link for booth photos
};
```

Paste your Google Drive folder links between the quotes. Example:

```js
const GOOGLE_DRIVE = {
  reports: "https://drive.google.com/drive/folders/ABC123?usp=sharing",
  notes:   "https://drive.google.com/drive/folders/DEF456?usp=sharing",
  slides:  "https://drive.google.com/drive/folders/GHI789?usp=sharing",
  flyers:  "https://drive.google.com/drive/folders/JKL012?usp=sharing",
  photos:  "https://drive.google.com/drive/folders/MNO345?usp=sharing",
};
```

When these are filled in, the Documents and Photos pages will show "View on Google Drive" buttons.

### Step 4 — Link Individual Files

For documents and photos, you can use either:
- **Local file paths** (the filename in the matching folder): `"report-2026-04.pdf"`
- **Google Drive direct links** (full URL): `"https://drive.google.com/file/d/FILEID/view?usp=sharing"`

To get a direct link for a file in Google Drive:
1. Right-click the file
2. Click **Share** > **Copy link**
3. Paste the full URL as the filename

The website automatically detects whether you're using a local file or a web link.

---

## How to Update Content

Open `index.html` in any text editor. Scroll down to the `<script>` section and look for:

```
CONFIGURATION — EDIT THESE ARRAYS TO UPDATE THE SITE
```

Everything you need to change is in this section. Below are step-by-step instructions for every common task.

**Important:** Always keep the commas, quotes, and curly braces exactly as shown. If something breaks, compare your edit to the examples below.

---

### Add an Announcement

Find `const ANNOUNCEMENTS = [` and add a new entry **at the top** (newest first):

```js
{
  date: "2026-05-01",
  title: "Your Announcement Title",
  body: "Your announcement text here."
},
```

> Announcements older than 90 days are automatically hidden.

---

### Add an Event

Find `const SPECIAL_EVENTS = [` and add:

```js
{
  date: "2026-06-15",
  title: "Event Name",
  location: "City, TX",
  description: "What the event is about.",
  flyerFile: "my-flyer.pdf"
},
```

- **flyerFile** can be a local filename (in the `flyers/` folder) or a full Google Drive link
- Use `""` (empty quotes) if there is no flyer
- Monthly committee meetings are generated automatically — you only add special events here

---

### Add a Monthly Report

Find `const REPORTS = [` and add **at the top**:

```js
{ month: "April 2026", filename: "report-2026-04.pdf" },
```

- **filename** can be a local file or a Google Drive link

---

### Add Meeting Notes

Find `const MEETING_NOTES = [` and add **at the top**:

```js
{
  month: "April 2026",
  date: "2026-04-15",
  filename: "notes-2026-04.pdf",
  summary: "Brief summary of what was discussed."
},
```

The newest entry automatically becomes the featured "Latest Meeting Notes" card.

---

### Add Meeting Slides

Find `const MEETING_SLIDES = [` and add **at the top**:

```js
{ month: "April 2026", filename: "slides-2026-04.pdf" },
```

---

### Add a Booth Photo

Find `const BOOTH_PHOTOS = [` and add:

```js
{ filename: "my-photo.jpg", caption: "Description — Event Name, City TX" },
```

- **filename** can be a local file (in `photos/`) or a Google Drive link
- The gallery auto-cycles through all photos

---

### Update Meeting Info

Find `const MEETING_INFO = {` and change any of these fields:

| Field | What it controls |
|-------|-----------------|
| `schedule` | Text like "3rd Wednesday of Every Month" |
| `time` | Text like "7:00 PM – 8:00 PM (Central)" |
| `zoomLink` | The full Zoom join URL |
| `meetingId` | Zoom Meeting ID |
| `passcode` | Zoom passcode |
| `chair` | Chair's title or name |
| `chairEmail` | Chair's email address |

> The next meeting date is calculated automatically — you do not need to update it.

---

### Update Editorial Calendar

Find `const EDITORIAL_CALENDAR = [` and replace with current topics from [aagrapevine.org/contribute](https://www.aagrapevine.org/contribute):

```js
{ issueMonth: "Month Year", topic: "Topic Name", deadline: "YYYY-MM-DD" },
```

---

### Update Subscription Prices

The Subscribe page has prices in the `renderSubscribe()` function. Search for `$36`, `$2.99`, `$69`, etc. and update when Grapevine announces price changes.

Current pricing: [aagrapevine.org/store/us-subscriptions](https://www.aagrapevine.org/store/us-subscriptions)

---

### Add a YouTube Video

Find `const YOUTUBE_VIDEOS = [` and add:

```js
{ id: "VIDEO_ID", title: "Video Title" },
```

The `VIDEO_ID` is the part after `v=` in a YouTube URL.
Example: `youtube.com/watch?v=ABC123` → ID is `"ABC123"`

---

### Add a Podcast Episode

Find `const SPOTIFY_EPISODES = [` and add:

```js
{ id: "EPISODE_ID", title: "Episode Title" },
```

Find episode IDs at the [AA Grapevine Spotify page](https://open.spotify.com/show/714djcL57SFf0Nzf40CL8Q) — the ID is in the URL after `/episode/`.

---

### Add an Instagram Post

Find `const INSTAGRAM_POSTS = [` and add the post shortcode:

```js
"POST_SHORTCODE",
```

The shortcode is the part after `/p/` in an Instagram URL.
Example: `instagram.com/p/ABC123/` → shortcode is `"ABC123"`

---

### Add a Timeline Milestone

Find `const TIMELINE = [` and add in chronological position:

```js
{
  year: "2026",
  title: "Milestone Title",
  desc: "Description of what happened.",
  type: "grapevine"
},
```

**type** must be one of: `"grapevine"`, `"lavina"`, or `"both"`

---

### Add a Resource Link

Find `const RESOURCES = [` and add:

```js
{
  title: "Resource Name",
  url: "https://example.com",
  icon: "bi-globe",
  description: "Short description.",
  cat: "sites"
},
```

**cat values** (determines which section the link appears in):

| Value | Section |
|-------|---------|
| `"sites"` | Grapevine & La Viña |
| `"digital"` | Digital Tools & Apps |
| `"involve"` | Get Involved |
| `"gvr"` | GVR / RLV Tools |
| `"listen"` | Listen & Follow |
| `"aa"` | AA & NETA 65 |

Icon names from [icons.getbootstrap.com](https://icons.getbootstrap.com) — use the `bi-` prefix.

---

## File Naming Rules

If storing files locally (not on Google Drive):

| Folder | Pattern | Example |
|--------|---------|---------|
| `reports/` | `report-YYYY-MM.pdf` | `report-2026-04.pdf` |
| `notes/` | `notes-YYYY-MM.pdf` | `notes-2026-04.pdf` |
| `slides/` | `slides-YYYY-MM.pdf` | `slides-2026-04.pdf` |
| `flyers/` | `descriptive-name.pdf` | `spring-assembly-2026.pdf` |
| `photos/` | `descriptive-name.jpg` | `booth-spring-2026.jpg` |

Rules: lowercase, hyphens instead of spaces, no special characters.

---

## BASE_PATH Setting

Find `const BASE_PATH = "";` near the top of the script.

| Scenario | Value |
|----------|-------|
| Testing locally (double-click file) | `""` |
| GitHub Pages (repo URL) | `"/GV_NETA65"` |
| Custom domain (grapevine.neta65.org) | `""` |

---

## Website Pages

| Page | Menu Label | What's on it |
|------|-----------|-------------|
| Home | Home | Dashboard cards, announcements, media preview, countdown |
| Meeting | Meeting | Schedule, Zoom details, chair contact |
| Events | Events | Upcoming/past events with flyer links |
| Subscribe | Subscribe | GV & LV pricing, gift subscriptions |
| Contribute | Contribute | How to submit stories, editorial calendar |
| About | About GV/LV | History, timeline, service structure |
| GVR Corner | GVR Corner | GVR role, responsibilities, downloadable guides |
| Documents | Documents | Reports, notes, slides with download links |
| Photos | Event Gallery | Auto-cycling photo gallery with captions |
| Listen & Watch | Listen & Watch | Podcast, YouTube, Instagram embeds |
| Resources | Resources | Categorized links to external sites |

---

## Monthly Checklist

After each committee meeting, do these steps:

- [ ] Upload report PDF to Google Drive `reports/` folder (or local `reports/`)
- [ ] Upload meeting notes PDF to `notes/` folder
- [ ] Upload slides PDF to `slides/` folder
- [ ] Open `index.html` in your text editor
- [ ] Add new entry to `REPORTS` array (at the top)
- [ ] Add new entry to `MEETING_NOTES` array (at the top)
- [ ] Add new entry to `MEETING_SLIDES` array (at the top)
- [ ] Add any new announcements to `ANNOUNCEMENTS`
- [ ] Add any new special events to `SPECIAL_EVENTS`
- [ ] Add any new booth photos to `BOOTH_PHOTOS`
- [ ] Save the file and test locally (double-click `index.html`)
- [ ] Push to GitHub

---

## Annual Checklist

- [ ] Update `EDITORIAL_CALENDAR` from [aagrapevine.org/contribute](https://www.aagrapevine.org/contribute)
- [ ] Verify subscription prices and update `renderSubscribe()` if changed
- [ ] Add new YouTube videos and podcast episodes
- [ ] Review `RESOURCES` links for broken URLs
- [ ] Add new timeline milestones to `TIMELINE`
- [ ] Verify Google Drive sharing permissions are still active

---

## Deploy to GitHub Pages

1. Create a GitHub repository (e.g., `GV_NETA65`)
2. Push all files to the `main` branch
3. Go to **Settings > Pages > Source**: Deploy from branch > `main` > `/ (root)`
4. Site goes live at `https://yourusername.github.io/GV_NETA65/`

### Custom Domain (grapevine.neta65.org)

1. In repo **Settings > Pages > Custom domain**: enter `grapevine.neta65.org`
2. Add a **CNAME** DNS record: `grapevine` → `yourusername.github.io`
3. GitHub auto-creates a `CNAME` file
4. Set `BASE_PATH = ""` in index.html

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Website is blank | Check for missing commas or quotes in the config section. Open browser console (F12) for errors. |
| Document link doesn't work | Make sure the filename matches exactly (case-sensitive) or the Google Drive link is correct |
| Photos don't show | Check the filename in `BOOTH_PHOTOS` matches the actual file. Google Drive links must be direct sharing links. |
| Google Drive buttons not showing | Make sure the folder URL is pasted between the quotes in `GOOGLE_DRIVE` |
| Changes not showing on live site | Clear your browser cache (Ctrl+Shift+R) or wait a few minutes for GitHub Pages to update |

---

## Technical Details

- **Single HTML file** — all CSS, JS, and content in one file
- **No build tools** — no npm, no bundler, no server needed
- **CDN dependencies:** Tailwind CSS, Bootstrap Icons, Google Fonts (Inter)
- **SPA routing** via `history.pushState` + `hashchange` — browser back/forward works
- **Responsive** from mobile (320px) to ultra-wide (2560px+)
- **Accessibility:** skip-to-content link, keyboard navigation, ARIA labels
