# TXM-SM — SM Signal Board

The Systems Management team's launcher page: every standing page we run, in one place,
published to GitHub Pages through GitHub Actions.

**Live site:** https://texas-mutual-proving-ground.github.io/TXM-SM/

## What's in here

| File | Purpose |
| --- | --- |
| `index.html` | The whole site — three signal pages, the team roster, and the deploy explainer. Catalog data lives in the `CATALOG` and `TEAM` constants at the top of the `<script>` block. |
| `.github/workflows/pages.yml` | Builds and deploys on every push to `main`. |
| `.nojekyll` | Tells Pages to serve the files as-is instead of running Jekyll. |

## One-time setup

1. Push these files to `main`.
2. **Settings → Pages → Build and deployment → Source** → select **GitHub Actions**.
3. Watch the run in the **Actions** tab. First deploy takes about a minute.

That's the whole lesson: Pages built from a workflow rather than from a branch. The
workflow uses the three official actions — `configure-pages`, `upload-pages-artifact`,
`deploy-pages` — and needs `pages: write` plus `id-token: write` permissions to do it.

## Adding your own page

Open `index.html`, find the `CATALOG` array near the bottom, and add an entry:

```js
{
  title: "Your Page Name",
  cadence: "Weekdays 08:00 CT",   // or "Standing" for a page that changes with the work
  url: "https://…",               // null if you haven't published it yet
  blurb: "One or two sentences on what it watches and what it tells you.",
  sources: ["Jira", "Outlook"],
  owner: "Your Name"              // must match a name in TEAM
}
```

Then claim a seat in the `TEAM` array below it:

```js
{ name: "Your Name", github: "your-handle", coverage: "What you cover" }
```

Commit to `main`. The page count in the roster is derived automatically from the catalog,
so it stays correct without anyone maintaining a number.

## Why this exists

Work shows up in email, Teams, meetings, and hallway conversations, and only some of it
ever becomes a Jira ticket. Each page here watches one of those channels and surfaces what
looks like work but has no ticket behind it. The board is the index so nobody has to
remember which URL is which.
