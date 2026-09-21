# Change 002 — Fix Occasion Hero Video Delivery

## Main change

Fix the published occasion Hero video, which was returning `HTTP 403 Forbidden` when loaded from the same-site path `/events/*`

The event Hero now uses the same files already committed in `eltawalbeh/YaHalaWebsite`, served through `jsDelivr` with the exact source commit pinned:

```text
https://cdn.jsdelivr.net/gh/eltawalbeh/YaHalaWebsite@e5b0138517204b2061a23c62941db585afb9a0ef/public/events/saudind-hero.mp4
https://cdn.jsdelivr.net/gh/eltawalbeh/YaHalaWebsite@e5b0138517204b2061a23c62941db585afb9a0ef/public/events/saudind-hero.webm
```

## Root cause verified

```text
Source repo files: present
Home event Hero: rendered
Same-site MP4 request: HTTP 403 Forbidden
Same-site WebM request: HTTP 403 Forbidden
jsDelivr MP4 request: HTTP 206, video/mp4
jsDelivr WebM request: HTTP 206, video/webm
```

## Replace

```text
src/app/components/EventHero.tsx
```

## Optional test update

If the existing focused contract is included in the source transfer, replace it with:

```text
src/app/lib/heroConfig.test.mjs
```

## Why this fix is safe

- No change to `HomePage` routing or event date logic
- No change to the existing `VideoHero`
- No change to `Navbar`
- The media remains in the GitHub source repository
- The CDN URL is pinned to commit `e5b0138`, not `main`
- Both MP4 and WebM remain available
- The CTA and event copy are unchanged

## Verification

```text
Focused hero contract: 2 passed
Production build: passed
Git diff --check: passed
CDN MP4: HTTP 206, video/mp4
CDN WebM: HTTP 206, video/webm
```

## Figma Make handoff

1. Replace `src/app/components/EventHero.tsx`
2. Optionally replace `src/app/lib/heroConfig.test.mjs`
3. Run `Deploy`
4. Run `Publish`
5. Recheck `https://yahala.co/` and confirm the video request is no longer same-site `/events/*`
