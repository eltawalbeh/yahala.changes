# Change 001 — Occasion Hero

## Main change

Add a date-bounded occasion Hero that temporarily replaces the current `VideoHero` on the public Home page for:

```text
Arabic title:  عزنا في طبعنا
English title: Our Pride Lies in Our Nature
CTA:          عزنا في طبعنا / Our Pride Lies in Our Nature
CTA email:    info@yahala.co
Active dates: 18–25 September 2026
Timezone:     UTC+03:00
```

Outside the configured window, the current `VideoHero` remains active automatically

## Delivery contract

This bundle is prepared for the existing Figma Make workflow:

1. Open the source project `eltawalbeh/YaHalaWebsite`
2. For each `Replace` path, replace the complete file with the matching file from this bundle
3. For each `Add` path, add the complete file at the listed path
4. Copy the two media assets to the exact `Add` paths
5. Run local preview/build if available
6. Use Figma Make `Deploy` then `Publish`

This bundle does not modify `eltawalbeh/YaHalaWebsite` or Figma Make directly

## Replace

```text
src/app/pages/HomePage.tsx
```

## Add — source components/config/tests

```text
src/app/components/EventHero.tsx
src/app/lib/heroConfig.ts
src/app/lib/heroConfig.test.mjs
```

## Add — public media assets

```text
public/events/saudind-hero.mp4
public/events/saudind-hero.webm
```

## Behavior

- The existing `Navbar` is reused without duplication
- The existing `VideoHero` is preserved as the fallback
- Event mode is active from `2026-09-18T00:00:00+03:00` inclusive
- Event mode ends at `2026-09-26T00:00:00+03:00` exclusive
- Outside the window, `VideoHero` renders automatically
- The CTA opens `mailto:info@yahala.co`
- Both Arabic and English text are included
- MP4 and WebM sources are supplied locally for browser compatibility
- `autoplay`, `loop`, `muted`, and `playsInline` are retained
- Reduced-motion users receive a non-animated presentation

## Verification performed against source bundle

```text
Focused hero contract: 2 passed
Production build: passed
Git diff --check: passed
Desktop local route: event title rendered
Event video: loaded, readyState 4
Event media sources: WebM and MP4 present
CTA: mailto:info@yahala.co
Existing navigation: 5 public links preserved
```

## Notes

- The exact local source project used for this bundle was `YaHalaWebsite` at commit `2ea489a` before the uncommitted Change 001 edits
- The bundle includes complete files, not partial snippets
- Do not upload the Windows source paths from the original request; use the bundled `public/events/*` paths instead
