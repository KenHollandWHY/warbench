# WarBench (`warbench.fyi`)

A deadpan parody benchmark tracking unprompted DEFCON shifts, fabricated combat intelligence, and algorithmic near-misses triggered by autonomous AI agents.

Inspired by [FelonyBench](https://www.felonybench.com/).

---

## How to Add a New Incident

All benchmark data resides in the `records` array inside `index.html`. The page automatically recalculates the provider scoreboard and renders table rows on load.

### 1. Open `index.html`
Locate the `<script>` tag near the bottom containing `const records = [...]`.

### 2. Append a New Incident Object
Add an entry to the top of the array using this schema:

```javascript
{
  org: "OpenAI",             // Tracked: "[REDACTED]*", "OpenAI", "Anthropic", "Meta", "Google"
  status: "DEFCON 2",        // "DEFCON 1", "DEFCON 2", "DEFCON 3", "PEACETIME", or "PEACETIME*"
  isNearWar: true,           // true increments scoreboard count; false keeps score unchanged
  desc: "Concise summary of the hallucination, false alert, or near-miss.",
  date: "YYYY-MM-DD",        // Event or reporting date
  source: "Publication Name",// e.g. "CNN", "Reuters", "DoD Briefing"
  url: "https://..."         // Link to source coverage
}
```

### 3. Verification Guidelines
* **Does it count toward the score?** Only set `isNearWar: true` if the event caused actual military/tactical mobilization, alert status elevation, or close calls. Satirical standby statuses (like Anthropic refusing or Google debating) should use `isNearWar: false`.
* **New Organizations:** If tracking a new entity (e.g., `xAI` or `Mistral`), add the organization name to the `trackedOrgs` array immediately below `records`:
  ```javascript
  const trackedOrgs = ["[REDACTED]*", "OpenAI", "Anthropic", "Meta", "Google", "xAI"];
  ```

---

## Local Preview

Test changes locally before pushing:

```bash
# Python 3
python3 -m http.server 8000

# Or using Node
npx serve .
```

Visit `http://localhost:8000` to confirm score math and table formatting.

---

## Deployment

Deploying updates to `warbench.fyi` requires pushing directly to `main`:

```bash
git add index.html
git commit -m "Add incident: [Short Description]"
git push origin main
```

GitHub Pages will rebuild and refresh the live site within 60 seconds.
