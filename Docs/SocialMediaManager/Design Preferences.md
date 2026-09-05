---
type: preferences
status: user-approved-direction
updated: 2026-09-05
---
# Design Preferences

Primary reference: [Ronas IT Fintech](https://dribbble.com/shots/25742426-Fintech-Web-App-Design), for its clean and easy-to-use feeling. Stripe dashboard is a general quality reference; Metricool is the social analytics reference. Supporting references: [CRM](https://dribbble.com/shots/25742359-CRM-Dashboard-App-Design), [Isora](https://dribbble.com/shots/24564783-UI-UX-Web-Design-for-Isora-Web-App-SaaS-Platform), [Ronas IT portfolio](https://dribbble.com/ronasit).

Pages/descriptions were retrieved; actual shot artwork was not visually inspected this session. Inspect it before claiming fidelity. Exact palette, typography and tokens are not approved.

## Accepted preferences

Balance information density, limited scrolling and reduced data anxiety. A few high-value visuals should lead into details with one click or hover. Prioritize decisions over showing every metric.

## Implementation interpretation

Use progressive disclosure: overview answers the main question, click opens persistent detail preserving account/date context; hover offers a preview. Keyboard and touch provide equivalent access. Essential information is never hover-only. Restore focus after overlays close.

Proposed direction: neutral surfaces, readable typography, restrained accents, consistent spacing and shared Tailwind/shadcn tokens. Color communicates meaning alongside labels. These are provisional choices until a working page is reviewed.

Limited scrolling is a usability goal, not a fixed-height mandate. Preserve zoom/reflow, readable text and touch targets. Smaller viewports may scroll naturally. Avoid unnecessary nested scrolling.

Include empty/loading/error/stale/partial-success/permission-denied states. Make freshness and reconnection needs clear without excessive alerts. Unavailable differs from zero.

First reference implementation: Connections & Scan Health with account connections, freshness, scan action and expandable run detail. Label fixtures. Refine with Corey before calling it approved. Data collection still leads the roadmap.
