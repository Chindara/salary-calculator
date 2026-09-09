# Sri Lanka Salary Calculator

Static, single-file calculator for Sri Lankan **Advance Personal Income Tax (APIT)**, the
**EPF employee deduction (8%)** and monthly **take-home salary**.

No build step, no dependencies — `index.html` is the whole app. The only external request is
the Outfit webfont from Google Fonts.

Two-column layout (inputs and headline results on the left, slab table and breakdown on the
right), collapsing to one column below 1000px. Light and dark themes follow the OS setting and
can be toggled in the header; the choice is remembered in `localStorage`.

## Inputs

| Field | Meaning |
| --- | --- |
| Monthly basic salary | EPF-applicable earnings |
| Cash allowances | Allowances paid in cash |
| Other taxable income | Non-cash benefits (vehicle, housing, fuel) or other taxable employment income |
| Deduct EPF (8%) | Toggle the employee contribution |
| Apply EPF on allowances too | Include allowances in the EPF base |
| Other income is paid in cash | Add other income to take-home instead of treating it as a non-cash benefit |

## APIT slabs (effective 01 April 2025)

Monthly figures are the annual thresholds divided by 12.

| Monthly income | Rate |
| --- | --- |
| First Rs. 150,000.00 | 0% |
| Next Rs. 83,333.33 | 6% |
| Next Rs. 41,666.67 | 18% |
| Next Rs. 41,666.67 | 24% |
| Next Rs. 41,666.67 | 30% |
| Balance | 36% |

To change the rates, edit the `BANDS` array near the top of the `<script>` block in
[index.html](index.html) — thresholds are **annual** amounts.

## How the numbers are derived

- **APIT base** = basic salary + cash allowances + other taxable income. The 8% EPF
  contribution is *not* deductible for APIT, so tax is charged on the gross figure.
- **EPF employee 8%** is applied to the basic salary (plus allowances if the option is ticked).
- **Take-home** = gross cash income − APIT − EPF. Non-cash benefits are taxed but never
  received in cash, so they are excluded unless marked as cash.
- Employer EPF (12%) and ETF (3%) are displayed for information only; they are not deducted
  from the employee's pay.

## Run locally

Open `index.html` in a browser, or serve it:

```sh
npx serve .
```

## Deploy to Netlify

Connect the repository and accept the defaults — `netlify.toml` sets the publish directory to
the repository root with no build command. Or drag the folder onto the Netlify dashboard.

## Disclaimer

Indicative figures only. Confirm your liability with the Inland Revenue Department or your
payroll department.
