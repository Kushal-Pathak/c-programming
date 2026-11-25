# Design system — BCA C Programming

**Reference:** `unit02.html` (Elements of C). This document records its actual design values and the rules for extending the course. Reuse the reference stylesheet and markup rather than designing each unit from scratch. `index.html` uses the same visual system with a small directory-specific extension.

## 1. Principles

Academic, calm, minimal and readable. Prioritize lesson content, clear hierarchy, examples and feedback over decoration. White background, restrained blue accent, subtle neutral borders, no gradients, decorative illustrations, shadows (except mobile navigation), icon libraries or external fonts. Do not add dark mode or a new theme unless requested. Use color as reinforcement, never the only signal.

## 2. Design tokens

```css
:root {
  color-scheme: light;
  --bg: #fff;
  --surface: #f6f7f9;
  --text: #17212b;
  --muted: #526071;
  --line: #d6dce3;
  --accent: #214f83;
  --accent-dark: #173b65;
  --good: #17613c;
  --bad: #9c2d24;
  --radius: 8px;
  --sidebar: 285px;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 16px;
  line-height: 1.65;
}
```

| Role | Value |
|---|---|
| White page/card | `#fff` |
| Surface / table heading / code block | `#f6f7f9` |
| Primary text | `#17212b` |
| Secondary text | `#526071` |
| Borders | `#d6dce3` |
| Primary action/link | `#214f83` |
| Hover / strong active text | `#173b65` |
| Active sidebar background | `#eaf0f7` |
| Learning panel background | `#f8fafc` |
| Inline code background | `#f0f2f5` |
| Focus outline | `#588bcb` (3px, offset 3px) |
| Selected quiz option | `#edf3f9` / border `#98acc4` |
| Correct quiz option | `#eef7f1` / border `#86b29b` / text `#17613c` |
| Incorrect quiz option | `#fdf1ef` / border `#d9a29d` / text `#9c2d24` |

## 3. Typography

| Element | Reference specification |
|---|---|
| Body | Arial, Helvetica, sans-serif; 16px; line-height 1.65 |
| H1 | `clamp(1.85rem,4vw,2.5rem)`; line-height 1.3; letter-spacing −0.035em; margin-bottom 8px |
| H2 | 1.4rem; line-height 1.3; margin 32px 0 12px |
| H3 | 1.12rem; line-height 1.3; margin 24px 0 8px |
| Eyebrow | .81rem; bold; uppercase; letter-spacing .035em; muted |
| Sidebar links | .91rem; line-height 1.35 |
| Tables | .94rem; line-height 1.5; .88rem at ≤720px |
| Inline/code blocks | `ui-monospace,SFMono-Regular,Consolas,"Liberation Mono",monospace`; .9em; block line-height 1.5 |
| Footer | .85rem, muted |

Use bold only for essential terms, labels and results. Use one H1 per view, H2 for lesson sections, H3 for subtopics. Avoid justified text and headings used solely for visual size.

## 4. Layout, spacing and responsiveness

The desktop shell is centered, max-width 1500px, two-column grid `var(--sidebar) minmax(0,1fr)`. Main content uses `min-width:0`, padding `38px clamp(18px,5vw,70px) 64px`; `.page` and `.footer` max-width 840px, centered. Topbar is sticky at top, white, bottom border, minimum height 64px, padding 10px 24px. Sidebar is sticky below it, height `calc(100dvh - 64px)`, independently scrollable, border right, padding 20px 15px. Use native document scrolling for main content.

| Width | Layout |
|---|---|
| Above 900px | 285px sidebar, full desktop layout |
| 721–900px | 250px sidebar, main padding 28px 24px 50px, topbar padding 10px 16px |
| 720px and below | Single column; sticky 58px-min-height topbar; Menu opens left drawer width `min(320px,85vw)`; overlay below topbar; main padding 23px 16px 40px |
| Small screens | One-column `.field-grid`; panels padding 14px; table cells 8px; wrap action buttons and long text, scroll code/tables internally |

Spacing uses the reference's small set of values: 4–10px for compact groups, 12–16px for paragraphs/controls, 20–24px for panels and 32px for new major sections. Paragraph margin 0 0 12px; lists margin 8px 0 16px, left padding 24px; list items margin 5px 0. Main panels padding 20px, margin 22px 0. Borders 1px, main radius 8px; controls/code radius 6px, inline code 3px. Keep sizing consistent; use flexible widths rather than fixed content dimensions.

## 5. Component inventory

| Component / class | Use |
|---|---|
| `.skip`, `.topbar`, `.brand`, `.spacer`, `.menu-button` | Accessible skip link, sticky course header, menu |
| `.shell`, `.sidebar`, `.mobile-backdrop`, `main`, `.page` | Shared responsive page structure |
| `.nav-no`, `.nav-check`, `[aria-current=page]` | Numbered nav, completion check and active page |
| `.progressbox`, `progress`, `.stats`, `.stat` | Learning progress and concise numeric overview |
| `.eyebrow`, `.muted`, `.lesson-heading` | Unit/lesson metadata, heading divider |
| `.objectives` | Neutral bordered learning objectives |
| `.lesson-text` | Main instructional content, H2 with top border/padding |
| `pre > code.language-c`, `pre > code.language-text` | C source and output; use escaped plain text |
| `.code-wrap`, `.code-copy` | Copy button above code; reference JS adds these to C code |
| `.table-scroll`, `table`, `th`, `td` | Accessible scroll region; two-column comparisons, left aligned; first column 42% |
| `.notice` | Small explanatory note with 3px blue left border |
| `.learning-panel`, `.field-grid`, `.result`, `.chips`, `.chip`, `.memory`, `.memory-model` | Interactive demos, input pairs, result display, token and memory examples |
| `.actions`, `.button`, `.secondary` | Primary/secondary actions, wrapping button row |
| `.practice-section`, `details.practice`, `.practice-answer` | Expandable worked answers and exam marking guides |
| `.quiz-section`, `.quiz`, `.option`, `.feedback`, `.quiz-result` | Scored formative questions and results |
| `.complete-panel`, `.check-line` | Self-reported lesson completion |
| `.lesson-navigation` | Previous/next unit lesson navigation |
| `.overview-list`, `.overview-item`, `.overview-status` | Ordered lesson or unit directory |
| `.footer`, `.noscript` | Quiet footer and no-JS explanation |

Primary controls: blue background and white text, 1px accent border, radius 6px, 9px 15px padding, weight 600, line-height 1.4, min-height 44px. Secondary controls: white background, accent text, neutral border. Hover primary uses darker accent; secondary uses neutral surface. Disabled buttons use reduced opacity and `not-allowed`. Use explicit `type="button"` unless submitting a form. Native input/select min-height 44px; labels visible; radio/checkbox 18px with larger clickable label. Existing copy/menu compact controls are exceptions; prefer ≥44px touch targets in new work when they fit.

Tables: collapsed borders, 9px 12px cell padding, surface header, vertical-align top. Wrap wide tables in `.table-scroll` with `tabindex="0"`, `role="region"` and an informative `aria-label`; never force page-wide overflow. Code blocks: surface background, border, 14px 16px padding, horizontal scrolling, whitespace preserved, tab-size 4. Keep copy buttons limited to C code rather than output.

## 6. Unit page structure

Use the following as a structural guide, not a complete application. Copy real components and behavior from the reference.

```html
<a class="skip" href="#main">Skip to learning content</a>
<header class="topbar">…</header>
<div class="shell">
  <aside class="sidebar" id="sidebar">
    <div class="progressbox">…</div>
    <nav aria-label="Table of contents">
      <h2>Table of contents</h2>
      <a href="index.html">All units</a>
      <a data-nav="overview" href="#overview">Unit overview</a>
      <!-- lesson links and final review -->
    </nav>
  </aside>
  <main id="main" tabindex="-1">
    <section class="page" id="overview">…</section>
    <article class="lesson page" id="lesson-slug" aria-labelledby="heading-lesson-slug">
      <header class="lesson-heading">
        <p class="eyebrow">Lesson 1 of N · Syllabus X.Y</p>
        <h1 id="heading-lesson-slug">Topic title</h1>
        <p class="muted">Unit X · Unit title</p>
      </header>
      <section class="objectives">…</section>
      <div class="lesson-text">…</div>
      <section class="learning-panel" aria-label="Interactive demonstration">…</section>
      <section class="practice-section">…</section>
      <section class="quiz-section">…</section>
      <div class="complete-panel">…</div>
      <nav class="lesson-navigation" aria-label="Lesson navigation">…</nav>
    </article>
    <section class="page" id="final-review">…</section>
    <footer class="footer">…</footer>
  </main>
</div>
```

Use stable, descriptive hash slugs. JS shows one `.page` at a time, sets active nav state and updates the page title. Without JS, all unit content stays visible and anchor links still work. Keep the mobile backdrop in the DOM, link it to menu dismissal and preserve keyboard accessibility.

### Homepage directory

`index.html` uses the same shell, tokens, navigation and `.overview-list` row layout. Available units are real links (`href="unit02.html"`); unavailable entries are plain text rows with “Coming soon”, no href or tab stop. The homepage adds `.directory-nav-item` and `.unit-unavailable` for static rows; reuse these if needed. No guessed syllabus names: use numerical placeholders until the teacher supplies actual titles. The header brand links to `index.html`, while unit overview links remain hash-based. Update both sidebar and directory when a unit is enabled.

## 7. Interaction, printing and quality

Use native controls with labels and meaningful status announcements (`aria-live="polite"` or `role="status"`). Quiz feedback must say correct/incorrect and explain why; do not rely on red/green. Use the scoring and localStorage contracts in `AGENTS.md`. Keep demos responsive and validate input; no arbitrary code execution. Mobile navigation supports open/close, backdrop, Escape and focus return. Keep reduced-motion preference respected.

Reference print mode: A4, 16mm margins, black text, 11pt body, 22pt H1, 15pt H2; hide navigation, interactive controls, quizzes and footer. Prevent code blocks and tables from splitting where practical. Print the currently selected lesson (or overview); with JS disabled, content remains readable. The HTML is not subject to the PDF notes' one-page-per-topic limit.

Test 320, 390, 720, 721, 768, 900, 901 and 1440 CSS px as appropriate; check real interactions rather than screenshots only. Preserve existing behavior, typography and layout when introducing new units. Reference CSS is the authoritative implementation; change shared design only deliberately, and keep this file and every affected page in sync.
