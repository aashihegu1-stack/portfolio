---
layout: post
title: Semantic HTML with OCS Typography Grammar
description: Semantic HTML defines meaning and structure. OCS Typography Grammar expresses the OCS style without hardcoding CSS.
categories: [SASS, Typography]
permalink: /sass/typography
---

## Done by Aashi

This page is live at the valid typography route:

https://aashihegu1-stack.opencodingsociety.com/sass/typography

## Typography assignment

Use semantic HTML to structure content clearly and let the global OCS SASS typography system handle the visual styling.

### Core rules

- Use `h1` / `h2` / `h3` for headings
- Use `p` for paragraph text
- Use `ul` / `ol` and `li` for lists
- Use `strong` and `em` for emphasis
- Pair semantic tags with OCS utility classes such as `ocs_card`, `ocs_section-title`, and `ocs_text`

### Example

```html
<section class="ocs_card">
  <h2 class="ocs_section-title">Cat Care 101</h2>
  <p class="ocs_lead">Follow these basics to keep your pet happy.</p>
  <ol>
    <li>Give fresh water daily.</li>
    <li>Provide cozy resting spots.</li>
    <li>Play with them each day.</li>
  </ol>
</section>
```

This makes the page accessible, readable, and consistent with the OCS design system.
