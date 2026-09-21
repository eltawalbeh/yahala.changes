# Change 003 — Payment Method Logos

## Main change

Replace the homepage Payment Methods text labels with the supplied SVG logos and add `Moyasar` as the seventh payment method

## Replace

```text
src/app/pages/HomePage.tsx
```

The replacement keeps the existing section title, Arabic/English behavior, responsive wrapping, and card styling. Each logo is rendered at a consistent `120 × 40px` area with `object-contain`

## Add

```text
public/payment-methods/visa.svg
public/payment-methods/mastercard.svg
public/payment-methods/mada.svg
public/payment-methods/apple-pay.svg
public/payment-methods/stc-pay.svg
public/payment-methods/bank-transfer.svg
public/payment-methods/moyasar.svg
src/app/lib/paymentMethods.test.mjs
```

## Payment order

```text
Visa
Mastercard
Mada
Apple Pay
STC Pay
Bank Transfer
Moyasar / ميسر
```

## Asset contract

All supplied SVGs were checked and use:

```text
viewBox="0 0 240 80"
```

The website renders each asset consistently inside:

```text
width: 120px
height: 40px
object-fit: contain
```

The card minimum width is `168px` to prevent logo crowding

## Accessibility

Each logo receives a language-aware `alt` value:

```text
Arabic: فيزا، ماستركارد، مدى، Apple Pay، STC Pay، تحويل بنكي، ميسر
English: Visa, Mastercard, Mada, Apple Pay, STC Pay, Bank Transfer, Moyasar
```

## Verification

```text
Focused payment contract: 3 total tests passed with the existing hero contract
All 7 SVG assets present
All 7 SVG viewBoxes: 240 × 80
Production build: passed
Git diff --check: passed
```

## Figma Make handoff

1. Replace `src/app/pages/HomePage.tsx`
2. Add the seven SVG files under `public/payment-methods/`
3. Optionally add `src/app/lib/paymentMethods.test.mjs`
4. Run `Deploy`
5. Run `Publish`
6. Verify the homepage Payment Methods section in Arabic and English
