# Screenshot Replacement Guide

Three screenshot placeholders have been added to the Featured Projects section
of `README.md`. Each placeholder is a self-contained SVG that renders cleanly
on GitHub with a "screenshot pending" label and replacement instructions.

## Placeholder locations

| Project | Placeholder file | README location |
|---|---|---|
| IT Support Automation | `assets/screenshots/it-support-automation.svg` | Line 89 |
| Network & Infrastructure Configuration | `assets/screenshots/network-infrastructure-config.svg` | Line 101 |
| Internal Operations Tooling | `assets/screenshots/internal-ops-tooling.svg` | Line 113 |

## How to replace a placeholder

1. Capture a screenshot of the actual work described in the project card.
2. Save it as a PNG or JPEG in `assets/screenshots/` with the suggested filename.
3. Edit `README.md` and replace the placeholder `<img src="..." />` block.

### Example replacement

**Before** (placeholder):

```markdown
<div align="center">
  <img
    src="./assets/screenshots/it-support-automation.svg"
    alt="IT Support Automation — Screenshot placeholder"
    width="90%"
  />
</div>
```

**After** (real screenshot):

```markdown
<div align="center">
  <img
    src="./assets/screenshots/it-support-automation.png"
    alt="IT Support Automation — Terminal output showing user provisioning script"
    width="90%"
  />
</div>
```

## What to capture in each screenshot

### 1. IT Support Automation

**What:** A terminal window showing the script in action.

**Suggested content:**
- A dry-run output of the user provisioning script listing actions it would take
- An asset tracking log file showing entries being added with timestamps
- A ticket triage summary table printed to stdout

**Format:** PNG, 1600×900 px or larger, dark terminal theme matching the banner
colour scheme (dark background, cyan/purple accents).

**Example terminal command to capture:**

```bash
# If the script supports dry-run mode:
./provision-user.sh --dry-run jdoe@example.com

# Or run a log viewer showing recent entries:
tail -n 20 /var/log/asset-tracker.log
```

### 2. Network & Infrastructure Configuration

**What:** A visual representation of network architecture, firewall rules, or a
rendered runbook page.

**Suggested content:**
- A network topology diagram created with draw.io, Lucidchart, or Excalidraw
  showing VLANs, routers, and firewalls with labels
- A firewall rule table from pfSense, iptables, or a CSP console showing policy
  applied to production subnets
- A rendered Markdown runbook page from GitBook, MkDocs, or a static site
  generator showing a step-by-step procedure

**Format:** PNG, 1600×900 px or larger. If using a diagram tool, export at 2x
resolution for crisp rendering on Retina displays.

**Example captures:**

- **Diagram:** Export from draw.io as PNG with transparent background disabled
  and background colour set to `#0d1117` to match the dark theme.
- **Firewall rules:** Screenshot the web UI table or use a CLI tool like
  `iptables-save` piped through a formatter and captured in a terminal.
- **Runbook:** Open the rendered page in a browser, zoom to 100%, and capture
  the full content area (crop browser chrome).

### 3. Internal Operations Tooling

**What:** A UI screenshot of a dashboard, inventory table, or status page.

**Suggested content:**
- A dashboard showing key metrics (uptime, ticket queue depth, server status)
  with charts or tables
- An inventory page listing hardware assets with columns for serial number,
  location, assigned user, and warranty expiry
- A status page showing service health indicators with green/yellow/red pills
  or icons

**Format:** PNG, 1600×900 px or larger. Capture at 100% browser zoom or use a
screenshot tool that scales to actual pixels (not "Retina 2x" mode).

**How to capture:**

1. Open the tool in a browser or Electron app.
2. Zoom to 100% (Ctrl+0 or Cmd+0).
3. Use a full-page screenshot tool (browser DevTools → Cmd+Shift+P → "Capture
   full size screenshot" in Chrome/Edge, or a third-party tool like Shottr).
4. Crop to the viewport area — exclude browser tabs, address bar, and OS chrome.
5. If the tool has a light/dark mode toggle, use dark mode to match the banner.

## Screenshot best practices

- **Resolution:** Minimum 1600×900 px. GitHub scales images down if they exceed
  the container width, so higher resolution ensures crisp rendering on large
  monitors and Retina displays.
- **Colour scheme:** Dark backgrounds with cyan/purple accents match the banner.
  Avoid light-mode screenshots unless the tool has no dark mode option.
- **Content:** Show real data if possible, or realistic placeholder data. Avoid
  "lorem ipsum" filler — use `user-001`, `server-web-01`, `10.0.1.0/24`.
- **Sensitive data:** Redact IP addresses, hostnames, usernames, and any
  identifying information before committing. Use a rectangular overlay or blur
  tool, not a semi-transparent bar (those can be reversed).
- **File size:** Aim for under 500 KB per image. Use PNG for UI screenshots
  (lossless, good for text) and JPEG at 85% quality for diagrams or photos.
  Run `pngcrush` or `optipng` to reduce file size without quality loss.

## After replacing placeholders

Once all three placeholders are replaced with real screenshots, delete the three
`.svg` placeholder files from `assets/screenshots/` — they are no longer needed.

This file (`SCREENSHOTS.md`) can remain in the repository as reference, or be
deleted once the README is complete.
