# Task type: landing-page
Deliverable: copy doc + working page (HTML/CSS or the project's framework).
Default complexity: C2.

| Parameter | Required | Default | Infer from |
|---|---|---|---|
| Product / main character | yes | — | message, entity |
| Page goal (signup, download, waitlist, buy) | yes | — | message, entity defaults |
| Audience | yes | entity audience | entity |
| Sections | no | hero, problem, features (3), social proof, FAQ, CTA | — |
| Tech stack / where it lives | yes | existing project stack, else single HTML file | CLAUDE.md, repo |
| Brand (colors, fonts, logo) | yes | entity brand | brand.md |
| Language | no | entity default | entity |
| SEO keyword | no | none | entity |

Acceptance criteria (base):
1. Value proposition understandable in 5 seconds (headline + subhead).
2. One primary CTA, repeated at top and bottom.
3. Responsive at 375 px and 1440 px; WCAG AA contrast.
4. Uses brand tokens; no lorem ipsum left.
5. Title + meta description set.

Ask first (if unknown): page goal, tech stack, sections beyond default.
