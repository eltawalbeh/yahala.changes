# Change 004 — Fix Payment SVG Delivery URLs

## Main change

Fix the homepage payment logo URLs. The existing same-site paths return `HTTP 403 Forbidden` on the published site even though the SVG files exist in `YaHalaWebsite/public/payment-methods/`

The replacement uses `jsDelivr` URLs pinned to the exact GitHub commit that contains the seven SVG assets

## Root cause verified

```text
GitHub source assets: present
HomePage references: /payment-methods/*.svg
Published site response: HTTP 403 Forbidden
Pinned jsDelivr response: HTTP 200, image/svg+xml
```

## Replace

```text
src/app/pages/HomePage.tsx
```

No new SVG files are required for this correction. They already exist in the source repository and were included in `Change 003`

## Correct URL pattern

```text
https://cdn.jsdelivr.net/gh/eltawalbeh/YaHalaWebsite@2e7e08380b1c40d4cbafe34a2f7911e457129cbb/public/payment-methods/{name}.svg
```

The commit is pinned rather than using `main`, so the assets cannot silently change underneath the published page

## Covered assets

```text
visa.svg
mastercard.svg
mada.svg
apple-pay.svg
stc-pay.svg
bank-transfer.svg
moyasar.svg
```

## Verification

```text
All 7 CDN URLs: HTTP 200
All 7 content types: image/svg+xml
Browser fetch: 7/7 loaded
Production build: passed
Git diff --check: passed
```

## Figma Make handoff

1. Replace `src/app/pages/HomePage.tsx` with the file in this bundle
2. Do not delete the existing `public/payment-methods/*.svg` files
3. Run `Deploy`
4. Run `Publish`
5. Recheck the homepage Payment Methods section
6. Confirm browser requests use `cdn.jsdelivr.net`, not `/payment-methods/*.svg`
