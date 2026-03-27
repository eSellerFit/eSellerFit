# Marketplace Fit Calculator

A sophisticated assessment tool that evaluates which platform (Amazon, Shopify, or Etsy) best fits your e-commerce business across three critical dimensions: Customer Fit, Operational Fit, and Financial Fit.

## Overview

The Marketplace Fit Calculator uses the **3-Layer Framework**:

1. **Customer Fit** — Does your ideal buyer exist and actively shop on this platform?
2. **Operational Fit** — Can you operationally support your product on this platform?
3. **Financial Fit** — Can your margins support the platform's fees and advertising costs?

Each platform (Amazon, Shopify, Etsy) is weighted differently because different platforms prioritize these layers:
- **Amazon**: 30% Customer Fit, 40% Operational Fit, 30% Financial Fit
- **Shopify**: 45% Customer Fit, 20% Operational Fit, 35% Financial Fit
- **Etsy**: 50% Customer Fit, 20% Operational Fit, 30% Financial Fit

## Structure

```
marketplace-fit/
├── marketplace-fit.html              # Main entry point (welcome + assessment + results)
├── README.md                          # This file
└── assets/
    ├── css/
    │   └── shared-ui.css              # Shared design system (all calculators)
    └── js/
        ├── config.js                  # Configuration (endpoints, GA4 ID, booking URL)
        ├── calculator-shell.js        # Shared utilities (form binding, validation, progress)
        ├── marketplace-fit-data.js    # Questions, platforms, weights (PROTECTED IP)
        ├── marketplace-fit-engine.js  # Scoring logic & insights (PROTECTED IP)
        └── marketplace-fit-render.js  # Results presentation (dark theme, original design)
```

## Files Explained

### marketplace-fit.html
- Entry point with welcome screen, assessment flow, and results container
- Includes universal consent checkbox (all 3 legal documents)
- Universal footer (5 legal documents: Terms, Privacy, Disclaimer, Client Agreement, Refund Policy)
- Initializes calculator and binds event handlers

### assets/js/config.js
Shared configuration across all calculators. Set:
```javascript
window.ESF_CONFIG = {
  appsScriptUrl: 'https://script.google.com/macros/d/.../useTrigger', // Lead capture endpoint
  bookingUrl: 'https://calendly.com/gio_chakhidze/new-meeting',
  ga4Id: 'G-XYYCWXC1RV'
};
```

### assets/js/calculator-shell.js
Reusable framework providing:
- `bindStartGate()` — Form validation for welcome screen
- `showOnly()` — Screen navigation
- `renderQuestions()` — Dynamic question rendering
- `bindProgress()` — Progress bar tracking
- `allQuestionsAnswered()` — Validation check
- `collectAnswers()` — Extract form data
- `submitLead()` — POST data to Google Apps Script

### assets/js/marketplace-fit-data.js
**PROTECTED IP** — Contains:
- All 12 questions (4 per layer) with exact wording
- 3 layers: Customer Fit (Q1-4), Operational Fit (Q5-8), Financial Fit (Q9-12)
- Platform metadata: Amazon, Shopify, Etsy
- Platform weights: [CF%, OF%, FF%] per platform
- Layer colors and labels

### assets/js/marketplace-fit-engine.js
**PROTECTED IP** — Contains:
- `calculate()` — Computes layer scores and platform scores
- `calculatePlatformScores()` — Applies platform weights
- `getLayerInsight()` — Contextual interpretation for each layer
- `getPlatformExplanation()` — Platform-specific guidance

### assets/js/marketplace-fit-render.js
**UI Layer** — Contains:
- `renderResults()` — Builds the results HTML (dark theme, original design)
- `getPlatformWhy()` — Platform-specific explanation copy

## Design System

- **Primary Color**: Teal (#0f6e56)
- **Background**: Light cream (#f5f2eb)
- **Dark Results Theme**: Dark slate (#1a1a22)
- **Layer Colors**:
  - Customer Fit: Blue (#3a72b0)
  - Operational Fit: Orange (#b8620a)
  - Financial Fit: Green (#2a6a3a)
- **Platforms**: Amazon (#FF9900), Shopify (#96BE3D), Etsy (#F1641E)

## Typography

- **Headings**: Playfair Display (serif)
- **Body**: Syne (sans-serif)
- **Labels/Code**: JetBrains Mono (monospace)

## Features

### Welcome Screen
- Bright, welcoming design
- Layer preview cards (Customer Fit, Operational Fit, Financial Fit)
- Email capture
- Product category input
- Universal consent checkbox (3 legal documents)
- Universal footer (5 legal documents)

### Assessment Screen
- 12 questions (one per section, 3 options each)
- Progress bar showing completion
- Question animation
- Form validation before submission

### Results Screen
- Platform cards (3-column grid, top pick highlighted)
- Score bars with color coding
- Platform-specific explanation
- Layer breakdown with insights
- Top Pick weight analysis
- CTA to Entry Strategy booking
- Advisory notice
- Universal footer (5 legal documents)

## Integration Points

### Google Apps Script Endpoint
Posts lead data to Google Apps Script for Notion database capture:
```javascript
{
  calculator: 'marketplace-fit',
  category: 'user input',
  email: 'user@email.com',
  answers: { mf_1: '8.5', mf_2: '5', ... },
  result: {
    layerScores: { cf: 6.5, of: 5.2, ff: 7.1 },
    platformScores: { amazon: 6.8, shopify: 7.2, etsy: 6.4 },
    topPlatform: 'shopify'
  }
}
```

### Calendly Booking
CTA button links to: `https://calendly.com/gio_chakhidze/new-meeting`

### Google Analytics
Tracks events:
- `assessment_started` — User begins questionnaire
- `assessment_completed` — User completes and sees results

## Legal Documents Required

The calculator references these legal pages (create at `/legal/`):
- `/legal/terms.html` — Terms of Service
- `/legal/privacy.html` — Privacy Policy
- `/legal/disclaimer.html` — Disclaimer
- `/legal/client-agreement.html` — Client Agreement
- `/legal/refund-policy.html` — Refund Policy

## Methodology Preservation

The following are **PROTECTED** and should never be changed without explicit approval:
- ✅ All question wording
- ✅ Question order
- ✅ Layer groupings (CF: Q1-4, OF: Q5-8, FF: Q9-12)
- ✅ Answer values (2, 5, 8.5)
- ✅ Platform weights
- ✅ Scoring logic
- ✅ Interpretation text

## Allowed Customizations

You may freely modify:
- Colors and styling (render.js)
- Layout and spacing
- Typography
- Button labels
- Result presentation format (as long as data is correct)

## Deployment

1. Upload all files to GitHub repository: `github.com/eSellerFit/eSellerFit/marketplace-fit/`
2. Update `/shared-ui.css`, `/config.js`, `/calculator-shell.js` from latest versions
3. Verify paths in `marketplace-fit.html`:
   - `./assets/css/shared-ui.css`
   - `./assets/js/config.js`
   - `./assets/js/calculator-shell.js`
   - `./assets/js/marketplace-fit-data.js`
   - `./assets/js/marketplace-fit-engine.js`
   - `./assets/js/marketplace-fit-render.js`
4. Test at: `https://esellerfit.com/marketplace-fit/marketplace-fit.html`

## Troubleshooting

### Questions not loading
- Check browser console for errors
- Verify `marketplace-fit-data.js` is loaded
- Confirm `calculator-shell.js` `renderQuestions()` is called

### Results not showing
- Verify all 12 questions answered
- Check `marketplace-fit-engine.js` `calculate()` output
- Confirm `marketplace-fit-render.js` `renderResults()` receives data

### Leads not capturing
- Verify Google Apps Script URL in `config.js`
- Check network tab for POST request
- Confirm endpoint is set to `/useTrigger` (not `/exec`)

## Next Steps

- [ ] Set `ESF_CONFIG.appsScriptUrl` in `config.js`
- [ ] Upload legal pages to `/legal/` directory
- [ ] Add GA4 tag to all HTML files
- [ ] Test lead capture with Notion integration
- [ ] Deploy to GitHub + verify at esellerfit.com URL
