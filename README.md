# NETA 65 Grapevine / La Viña Committee Website

A bilingual (English/Spanish) single-page website for the Northeast Texas Area 65 Grapevine and La Viña Committee. Everything lives in **one file** (`index.html`) — no special software needed.

---

## Table of Contents

1. [How This Website Works](#how-this-website-works)
2. [What You Need](#what-you-need)
3. [Quick Start](#quick-start)
4. [Google Drive Setup](#google-drive-setup)
5. [How to Update Content](#how-to-update-content)
   - [Announcements](#add-an-announcement)
   - [Events](#add-an-event)
   - [Reports](#add-a-monthly-report)
   - [Meeting Notes](#add-meeting-notes)
   - [Meeting Slides](#add-meeting-slides)
   - [Booth Photos](#add-a-booth-photo)
   - [Meeting Info / Zoom](#update-meeting-info)
   - [Weekly Open Meeting Info](#update-weekly-open-meeting-info)
   - [Editorial Calendar](#update-editorial-calendar)
   - [Subscription Prices](#update-subscription-prices)
   - [YouTube Videos](#add-a-youtube-video)
   - [Podcast Episodes](#add-a-podcast-episode)
   - [Instagram Posts](#add-an-instagram-post)
   - [Timeline Milestones](#add-a-timeline-milestone)
   - [Resource Links](#add-a-resource-link)
   - [GVR/RLV Postcards & Flyers](#update-gvr--rlv-postcards--flyers)
6. [Language / Translation (EN ↔ ES)](#language--translation-en--es)
7. [File Naming Rules](#file-naming-rules)
8. [BASE_PATH Setting](#base_path-setting)
9. [Website Pages](#website-pages)
10. [What GVRs and RLVs Need to Know](#what-gvrs-and-rlvs-need-to-know)
11. [Monthly Checklist](#monthly-checklist)
12. [Quarterly Checklist](#quarterly-checklist)
13. [Annual Checklist](#annual-checklist)
14. [Deploy to GitHub Pages](#deploy-to-github-pages)
15. [Troubleshooting](#troubleshooting)
16. [Technical Details](#technical-details)

---

## How This Website Works

The entire website is a single HTML file. All the content you'll ever need to update is stored in clearly labeled configuration arrays near the top of the `<script>` section. You edit those arrays, save the file, and the website updates automatically.

**You do NOT need to know how to code.** You just need to follow the patterns shown below — copy an existing entry, change the text, and save.

### Key Features

- **Bilingual**: Full English/Spanish toggle — all page content, dates, buttons, and labels switch instantly
- **Auto-generated meetings**: Monthly committee meetings (3rd Wednesday) are calculated automatically
- **Countdown timer**: Live countdown to the next meeting on the home page
- **90-day announcements**: Old announcements automatically hide after 90 days
- **Random media picks**: Home page shows different podcast and YouTube selections each visit
- **PDF viewer**: Documents open in an inline viewer (no download required)
- **Calendar export**: Events can be added to any calendar app via .ics download
- **Share buttons**: Announcements and events can be shared via native share or clipboard

---

## What You Need

- **A text editor** — Notepad (Windows), TextEdit (Mac), or VS Code all work
- **Internet connection** — the site loads fonts and icons from the web
- **Google Drive** (optional) — for storing and sharing documents and photos
- **A web browser** — Chrome, Firefox, Edge, or Safari for testing

---

## Quick Start

1. Open `index.html` in your text editor
2. Find the section marked `CONFIGURATION — EDIT THESE ARRAYS TO UPDATE THE SITE` (around line 198)
3. Make your changes following the instructions below
4. Save the file
5. Double-click `index.html` to preview in your browser
6. When satisfied, push to GitHub (or ask someone who can)

> **Tip:** Use Ctrl+F (or Cmd+F on Mac) to search for the exact array name like `ANNOUNCEMENTS` or `SPECIAL_EVENTS`.

---

## Google Drive Setup

All documents (PDFs) and photos can be stored in Google Drive. This is the recommended approach so that multiple committee members can upload files without needing to edit code.

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

> **Important:** If sharing permissions expire or get changed, the documents will stop loading on the website. Check these at least once a year (see [Annual Checklist](#annual-checklist)).

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

You can include HTML links in the `body` field:
```js
body: "Visit <a href=\"https://example.com\" target=\"_blank\" rel=\"noopener\" class=\"text-brand-600 underline hover:text-brand-700\">this link</a> for details."
```

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
- Events have Share, Calendar (.ics), and View Flyer buttons in the detail modal

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

The newest entry automatically becomes the featured "Latest Meeting Notes" card on the Documents page.

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
- The gallery auto-cycles through all photos every 5 seconds
- Previous/next arrows and dot indicators are generated automatically

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
| `additionalNotes` | Extra note shown on the Meeting page |

> The next meeting date and countdown timer are calculated automatically — you do not need to update them. They always point to the next 3rd Wednesday.

---

### Update Weekly Open Meeting Info

Find `const WEEKLY_OPEN = {` and update:

```js
const WEEKLY_OPEN = { zoomId: "871 2036 8287", passcode: "238047", day: "Wednesdays", time: "11 AM Central" };
```

This info appears on the About page and in the Resources page under "GV Weekly Open Meeting."

---

### Update Editorial Calendar

Find `const EDITORIAL_CALENDAR = [` and replace with current topics from [aagrapevine.org/contribute](https://www.aagrapevine.org/contribute):

```js
{ issueMonth: "Month Year", topic: "Topic Name", deadline: "YYYY-MM-DD" },
```

- Leave `deadline: ""` for issues with no deadline (e.g., "Classic Grapevine")
- The Contribute page automatically highlights the next upcoming deadline
- Past deadlines are shown with a "Past" badge

---

### Update Subscription Prices

The Subscribe page has prices in the `renderSubscribe()` function. Search for `$36`, `$2.99`, `$69`, etc. and update when Grapevine announces price changes.

Current pricing: [aagrapevine.org/store/us-subscriptions](https://www.aagrapevine.org/store/us-subscriptions)

Phone numbers for subscriptions are also in `renderSubscribe()`:
- USA: (800) 631-6025
- International: +1 (570) 567-0437
- En Espanol: (800) 640-8781

---

### Add a YouTube Video

Find `const YOUTUBE_VIDEOS = [` and add:

```js
{ id: "VIDEO_ID", title: "Video Title" },
```

The `VIDEO_ID` is the part after `v=` in a YouTube URL.
Example: `youtube.com/watch?v=ABC123` → ID is `"ABC123"`

Videos are organized in sections:
- Original curated videos at the top
- Podcast episodes by season
- Personal stories
- La Vina (Spanish) videos
- Informational videos

Add new videos to the appropriate section.

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

The timeline appears on the About page with filtering by type and decade grouping.

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
| `"sites"` | Grapevine & La Vina |
| `"digital"` | Digital Tools & Apps |
| `"involve"` | Get Involved |
| `"gvr"` | GVR / RLV Tools |
| `"listen"` | Listen & Follow |
| `"aa"` | AA & NETA 65 |

Icon names from [icons.getbootstrap.com](https://icons.getbootstrap.com) — use the `bi-` prefix.

---

### Update GVR / RLV Postcards & Flyers

The GVR Corner page has four tabs of downloadable materials:
1. **GV Postcards** — English promotional postcards from aagrapevine.org
2. **LV Tarjetas Postales** — Spanish promotional postcards from aalavina.org
3. **GV Tools & Forms** — English catalogs, flyers, and forms
4. **LV Recursos & Formularios** — Spanish resources and forms

These are hardcoded links in the `renderGVR()` function. To update:
1. Search for `renderGVR` in the file
2. Find the tab section you want to update (look for `id="gvr-gvpc"`, `id="gvr-lvpc"`, `id="gvr-gvtool"`, or `id="gvr-lvtool"`)
3. Copy an existing link block and update the URL, title, and description
4. New postcards/flyers are published at [aagrapevine.org/gvr-resources](https://www.aagrapevine.org/gvr-resources) and [aalavina.org/recursos](https://www.aalavina.org/recursos)

---

## Language / Translation (EN ↔ ES)

The website is fully bilingual. Users click the **ES/EN** button in the header to switch languages.

### How Translation Works

- **Dynamic content** uses the `t("English text", "Spanish text")` helper function throughout all render functions
- **Dates** automatically format in the correct locale (English or Spanish)
- **Static HTML elements** (header, footer, modals) are updated by the `applyLang()` function
- **Navigation labels** are translated via the `NAV_ES` object
- **Language preference** is saved to the browser's localStorage, so it persists between visits

### What's Translated

- All page titles, headings, and descriptions
- All button labels (Share, Calendar, Copy, Close, etc.)
- Navigation menu items
- Countdown timer labels (Days, Hours, Min, Sec)
- Date formatting (months appear in Spanish when ES is active)
- Relative dates ("Today", "Tomorrow", "In X days")
- Footer text and copyright
- Modal buttons (event detail, PDF viewer)
- Toast messages (clipboard feedback)

### What Stays in English/Spanish

Some items intentionally remain in their original language:
- **Product names**: "AA Grapevine", "La Vina", book titles
- **PDF document titles**: Match the actual PDF filename/title
- **GVR postcard titles**: Match the official postcard names from aagrapevine.org
- **Resource link titles**: Many are proper names of websites or products
- **La Vina contribution section**: The submission instructions for La Vina are in Spanish since La Vina is a Spanish publication

### Adding New Translated Content

When adding new content to render functions, always use the `t()` helper:

```js
t("English text here", "Spanish text here")
```

For the `I18N` object (used by `applyLang()` for static HTML), add entries like:

```js
const I18N = {
  my_key: { en: "English", es: "Spanish" },
  ...
};
```

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

| Page | Menu Label (EN) | Menu Label (ES) | What's on it |
|------|----------------|-----------------|-------------|
| Home | Home | Inicio | Dashboard cards, announcements, media preview, countdown timer |
| Meeting | Meeting | Reunion | Schedule, Zoom details, chair contact, copy-to-clipboard |
| Events | Events | Eventos | Upcoming/past events, flyer links, calendar export, share |
| Subscribe | Subscribe | Suscribirse | GV & LV pricing, gift subscriptions, phone numbers |
| Contribute | Contribute | Contribuir | How to submit stories, editorial calendar with deadlines |
| About | About GV/LV | Acerca de GV/LV | History, timeline (40+ milestones), humor books, service structure |
| GVR Corner | GVR Corner | Rincon del RLV | GVR/RLV role, responsibilities, downloadable guides & postcards |
| Documents | Documents | Documentos | Reports, notes, slides with inline PDF viewer |
| Photos | Event Gallery | Galeria de Eventos | Auto-cycling photo gallery with captions |
| Listen & Watch | Listen & Watch | Escuchar y Ver | Podcast, YouTube, Instagram embeds |
| Resources | Resources | Recursos | Categorized links to external AA & Grapevine sites |

---

## What GVRs and RLVs Need to Know

This website is designed to be a **one-stop resource** for Grapevine Representatives (GVRs) and La Vina Representatives (RLVs). Here's what's available:

### For GVRs (English)

- **GVR Corner page**: Role description, responsibilities checklist, and ideas for promoting Grapevine at your homegroup
- **Downloadable guides**: GVR Handbook, GV Workbook, P-52 Pamphlet
- **Postcards & flyers**: 20+ printable promotional materials (Carry the Message, podcast, apps, books, etc.)
- **Registration link**: Register as a GVR at aagrapevine.org
- **Carry the Message**: Info on sponsoring gift subscriptions for facilities
- **Editorial calendar**: Current topics and deadlines for story submissions
- **Subscription info**: Current pricing for print, digital, and bundle options

### For RLVs (Spanish)

- **Rincon del RLV**: Same content as GVR Corner, fully translated
- **Manual del RLV**: Official RLV handbook from aalavina.org
- **Libro de Trabajo LV**: La Vina workbook
- **Tarjetas Postales**: Spanish-language promotional postcards
- **Registration link**: Register as an RLV at aalavina.org
- **Lleva el Mensaje**: Spanish version of the Carry the Message project

### For District Chairs

- **Meeting page**: Zoom info with one-click copy for sharing with district members
- **Events page**: All upcoming events with share buttons
- **Documents page**: Access to all committee reports, notes, and slides
- **Announcements**: Shareable announcements that can be forwarded to groups

### Key External Links Included

| Resource | URL | Purpose |
|----------|-----|---------|
| GVR Resources | aagrapevine.org/gvr-resources | Official GVR materials |
| RLV Recursos | aalavina.org/recursos | Official RLV materials |
| Submit a Story | aagrapevine.org/share | Story submission portal |
| Editorial Calendar | aagrapevine.org/contribute | Upcoming topics & deadlines |
| Carry the Message | aagrapevine.org/carry-the-message | Gift subscription program |
| GV Podcast | aagrapevine.org/grapevine-variety-hour | Free weekly podcast |
| GV Weekly Open Meeting | aagrapevine.org/grapevine-weekly-open | Live Zoom meeting info |
| Sobriety Calculator | aagrapevine.org/sobriety-calculator | Free sobriety date tool |
| GV App | aagrapevine.org/apps | Mobile app download |
| NETA 65 | neta65.org | Area website |
| GV/LV Committee | neta65.org/trusted-servants/grapevine-la-vina/ | Official committee page |

---

## Monthly Checklist

After each committee meeting, do these steps:

- [ ] Upload report PDF to Google Drive `reports/` folder (or local `reports/`)
- [ ] Upload meeting notes PDF to `notes/` folder
- [ ] Upload slides PDF to `slides/` folder
- [ ] Open `index.html` in your text editor
- [ ] Add new entry to `REPORTS` array (at the top)
- [ ] Add new entry to `MEETING_NOTES` array (at the top, include date and summary)
- [ ] Add new entry to `MEETING_SLIDES` array (at the top)
- [ ] Add any new announcements to `ANNOUNCEMENTS`
- [ ] Add any new special events to `SPECIAL_EVENTS`
- [ ] Add any new booth photos to `BOOTH_PHOTOS`
- [ ] Remove old announcements that are no longer relevant (though they auto-hide after 90 days)
- [ ] Save the file and test locally (double-click `index.html`)
- [ ] Test the Spanish version (click ES button) to make sure everything looks right
- [ ] Push to GitHub

---

## Quarterly Checklist

- [ ] Check that all Google Drive sharing permissions are still active
- [ ] Review upcoming events in `SPECIAL_EVENTS` — remove past events if desired
- [ ] Add any new YouTube videos or podcast episodes
- [ ] Check the GVR/RLV postcard links — aagrapevine.org occasionally updates these
- [ ] Verify the Zoom meeting link and passcode are still current
- [ ] Update the `WEEKLY_OPEN` info if the GV Weekly Open Meeting details change

---

## Annual Checklist

- [ ] Update `EDITORIAL_CALENDAR` from [aagrapevine.org/contribute](https://www.aagrapevine.org/contribute) — add the new year's topics
- [ ] Verify subscription prices and update `renderSubscribe()` if changed (check [aagrapevine.org/store/us-subscriptions](https://www.aagrapevine.org/store/us-subscriptions))
- [ ] Update phone numbers if they've changed
- [ ] Add new YouTube videos and podcast episodes
- [ ] Review `RESOURCES` links for broken URLs — click each one to verify
- [ ] Add new timeline milestones to `TIMELINE` if applicable
- [ ] Verify Google Drive sharing permissions are still active on all folders
- [ ] Check if aagrapevine.org has new postcards/flyers and update the GVR Corner tabs
- [ ] Review the `ANNOUNCEMENTS` array and clean out anything outdated
- [ ] Update the GV Workbook link if a newer version is published (check [aagrapevine.org/gvr-resources](https://www.aagrapevine.org/gvr-resources))
- [ ] Check for new GV/LV catalog PDFs and update links in both `RESOURCES` and `renderSubscribe()`

---

## Transition to a New Committee Chair

When the Grapevine/La Vina Committee Chair rotates:

1. **Update `MEETING_INFO`** — change `chair` and `chairEmail` fields
2. **Update Zoom info** — if the new chair uses a different Zoom account, update `zoomLink`, `meetingId`, and `passcode`
3. **Transfer Google Drive access** — share the Google Drive folders with the new chair and grant Editor permissions
4. **Transfer GitHub access** — add the new chair as a collaborator on the GitHub repository (Settings > Collaborators)
5. **Walk them through this README** — especially the [Quick Start](#quick-start) and [Monthly Checklist](#monthly-checklist)

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
5. Enable **Enforce HTTPS** in the Pages settings

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Website is blank | Check for missing commas or quotes in the config section. Open browser console (F12) for errors. |
| Document link doesn't work | Make sure the filename matches exactly (case-sensitive) or the Google Drive link is correct. |
| Photos don't show | Check the filename in `BOOTH_PHOTOS` matches the actual file. Google Drive links must be direct sharing links. |
| Google Drive buttons not showing | Make sure the folder URL is pasted between the quotes in `GOOGLE_DRIVE`. |
| Changes not showing on live site | Clear your browser cache (Ctrl+Shift+R) or wait a few minutes for GitHub Pages to update. |
| Spanish translation missing | Make sure the text uses `t("English","Spanish")` wrapper. See [Language section](#language--translation-en--es). |
| Countdown shows "coming soon" | The meeting date may have passed. The countdown auto-advances to the next 3rd Wednesday. |
| PDF viewer shows blank | Some Google Drive PDFs require the file to be publicly shared. Check sharing permissions. |
| Events not showing | Check that the `date` field is in `YYYY-MM-DD` format. Future events show under "Upcoming." |
| YouTube video thumbnail broken | Verify the video ID is correct. Private or deleted videos won't show thumbnails. |
| Instagram embeds not loading | Instagram embeds may be blocked by ad blockers. This is normal. |
| Sidebar menu shows wrong language | Click the ES/EN toggle button — the sidebar rebuilds when language changes. |

### How to Debug

1. Open `index.html` in your browser
2. Press **F12** to open Developer Tools
3. Click the **Console** tab
4. Look for red error messages — they usually point to the exact line with the problem
5. Common errors:
   - `Unexpected token` — missing comma or quote
   - `Unexpected end of input` — missing closing brace `}` or bracket `]`
   - `is not defined` — typo in a variable name

---

## Technical Details

- **Single HTML file** — all CSS, JS, and content in one file (~235KB)
- **No build tools** — no npm, no bundler, no server needed
- **CDN dependencies:** Tailwind CSS, Bootstrap Icons, Google Fonts (Inter)
- **SPA routing** via `hashchange` — browser back/forward works, bookmarkable URLs
- **Responsive** from mobile (320px) to ultra-wide (2560px+)
- **Accessibility:** skip-to-content link, keyboard navigation, ARIA labels, focus management
- **Bilingual:** Full EN/ES toggle with localStorage persistence
- **Offline-capable structure:** Content renders from local data arrays, only external dependencies are CDN CSS/fonts and embedded media (YouTube, Spotify, Instagram)

### Configuration Arrays Reference

| Array/Object | Location | Purpose |
|-------------|----------|---------|
| `BASE_PATH` | Line ~200 | URL prefix for local file paths |
| `GOOGLE_DRIVE` | Line ~207 | Google Drive folder sharing links |
| `NAV_SECTIONS` | Line ~214 | Navigation menu items and icons |
| `ANNOUNCEMENTS` | Line ~227 | Time-sensitive announcements (auto-expire 90 days) |
| `MEETING_INFO` | Line ~233 | Committee meeting Zoom details |
| `WEEKLY_OPEN` | Line ~241 | GV Weekly Open Meeting Zoom details |
| `SPECIAL_EVENTS` | Line ~258 | Non-recurring events (assemblies, workshops, etc.) |
| `REPORTS` | Line ~266 | Monthly committee report PDFs |
| `MEETING_NOTES` | Line ~276 | Monthly meeting notes with summaries |
| `MEETING_SLIDES` | Line ~282 | Monthly meeting slide decks |
| `BOOTH_PHOTOS` | Line ~288 | Event and booth photo gallery |
| `RESOURCES` | Line ~296 | Categorized external links |
| `EDITORIAL_CALENDAR` | Line ~335 | GV submission topics and deadlines |
| `TIMELINE` | Line ~363 | Historical milestones for About page |
| `YOUTUBE_VIDEOS` | Line ~406 | YouTube video IDs and titles |
| `SPOTIFY_EPISODES` | Line ~539 | Spotify episode IDs and titles |
| `INSTAGRAM_POSTS` | Line ~558 | Instagram post shortcodes |
| `I18N` | Line ~1342 | Static HTML translation strings |
| `NAV_ES` | Line ~598 | Spanish navigation labels |
