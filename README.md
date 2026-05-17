# filter-test-ublock

Custom [uBlock Origin](https://github.com/gorhill/uBlock) filter lists that strip
algorithmic and promoted clutter from **LinkedIn** and **Instagram**, so the feed
shows the people you actually follow.

## What it does

**`linkedin.txt`**
- Redacts Promoted / Suggested / "Recommended for you" posts and LinkedIn
  Learning course cards (painted black in place, not removed — see below)
- Hides the right-rail banner ad, the "Add to your feed" widget, and the
  "Try Premium" upsell

**`instagram.txt`**
- Redacts "Suggested" posts and "Sponsored" ads
- Hides the Reels nav tab
- Hides the Explore page's algorithmic grid (the search box still works)

### Why "redact" instead of "remove"?

Feed injections are painted **solid black in place** rather than deleted.
Removing a post mid-scroll collapses the layout and fights the site's own
infinite-scroll code, causing scroll-jank. Painting the post black keeps its
size — so the page doesn't jump — and leaves a visible record of how much of
your feed is algorithmic.

## Setup

You need [uBlock Origin](https://ublockorigin.com/) installed.

1. Open the uBlock Origin dashboard → **Filter lists** tab
2. Scroll to the bottom → **Import…**
3. Paste one or both of these URLs:

   ```
   https://raw.githubusercontent.com/andratwiro/filter-test-ublock/main/linkedin.txt
   https://raw.githubusercontent.com/andratwiro/filter-test-ublock/main/instagram.txt
   ```

4. Click **Apply changes**

To pull updates immediately: **Purge all caches** → **Update now** in the same tab.

## How it works

Both lists anchor on **stable hooks** — `data-testid`, `aria-label`, `role`,
visible text — never on the obfuscated CSS class names that LinkedIn and
Instagram rotate on every release. Every rule is commented with what it
targets and why.

## Caveats

- LinkedIn and (especially) Instagram change their markup often. Rules will
  break over time and need re-tuning.
- These lists can't tell "post from someone you follow" from "post from a
  stranger" — that's server-side information. They only target **labelled**
  algorithmic content. For unlabelled clutter, use Instagram's native
  "Following" feed toggle.

## License

[CC0 1.0 Universal](LICENSE) — public domain. Do whatever you want with it.
