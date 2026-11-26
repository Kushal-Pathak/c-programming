# AGENTS.md — BCA C Programming learning website

## 1. Purpose and scope

Maintain a free, beginner-friendly, examination-oriented learning resource for first-semester BCA students studying Computer Programming in C. Teach in simple English suitable for non-native speakers while retaining academically correct technical terms. Aim for comprehensive understanding and full-mark preparation, not guaranteed marks or expertise.

Read this file and `DESIGN_SYSTEM.md` before changing any page. Inspect `unit02.html` as the canonical implementation for lesson layout, components, CSS, navigation and interactive behavior. The existing content is the reference, not a reason to copy inaccuracies or unrelated Unit 2 material into new units.

## 2. Repository structure

```text
/
  AGENTS.md
  DESIGN_SYSTEM.md
  index.html       # course homepage / unit directory
  unit01.html      # Problem Solving with Computer
  unit02.html      # Elements of C — active reference unit
  ...
  unit11.html      # future unit (not created yet)
```

Use lowercase, zero-padded filenames (`unit01.html` through `unit11.html`). Keep paths relative so GitHub Pages works both at a domain root and at a repository subpath. Do not create empty placeholder HTML pages. The homepage must list all eleven units, in numerical order, but only link to completed, verified files. Unavailable entries are non-interactive text with a clear “Coming soon” label, not broken links or disabled anchors. Units 01 and 02 are currently enabled. Titles, hours and content for the other units have not been supplied; do not invent them.

## 3. Workflow for a new unit or update

1. Read the teacher's supplied syllabus and approved teaching order. Preserve original syllabus numbering even when teaching order changes. If the required syllabus is missing, request it rather than guessing its contents.
2. Plan the lesson order based on prerequisites. Preserve existing approved order unless explicitly asked to change it.
3. Copy the structural and visual patterns from `unit02.html`. Use a separate file per unit; do not add a framework, build step or dependency.
4. Write the lesson content and interactive exercises. Independently verify C examples, outputs and all quiz answers.
5. Add a unit overview, lesson navigation, unit-specific local progress, a final review and written examination marking guides.
6. Test the unit using the checklist below. Only after the unit is complete, enable its entry on `index.html` and update the available-unit count and navigation.
7. Report what changed, assumptions, tests run and any limitations. Do not claim tests that were not performed.

When editing an existing unit, preserve stable IDs, storage keys, working features and approved material unless the requested change requires otherwise. Keep edits focused; avoid reformatting unrelated pages.

## 4. Academic content contract

Each unit starts with an overview: unit title, supplied syllabus hours (if known), lesson list, question count, how to study, progress and a Start learning link. Each topic follows this order:

1. Lesson heading: topic name, original syllabus reference, learning order, and planned class time if supplied or explicitly identified as a suggestion.
2. Learning objectives (usually 3–5 specific outcomes).
3. Short, complete definition with important technical terms emphasized.
4. Detailed but simple explanations, types, rules, syntax and meaningful examples. Define new terms before relying on them. Use two-column tables for all comparisons and bullets for lists of rules.
5. Worked C examples with exact output and short explanations. Include complete compilable programs where helpful; identify code fragments and their assumed context. Avoid excessive code comments and overly obvious examples.
6. Common misconceptions and mistakes, with corrections and reasons.
7. Exam preparation: essential concepts, question patterns and a short summary where useful.
8. Interactive demonstration for a meaningful concept (simulation or clearly described activity).
9. Practice questions with expandable worked answers; encourage attempting before revealing.
10. Scored topic quiz, lesson completion checkbox and previous/next links.

End every unit with a mixed-topic scored review, written exam-style questions, suggested mark allocations that add up correctly, and a revision checklist. Never claim a marking scheme is official without evidence. Keep explanatory material substantial; do not reduce the website to the one-page-per-topic PDF style.

### C correctness rules

- Prefer portable C99/C17 examples, using `int main(void)` and correct standard headers. Clearly label C90/C99/C11/C23 differences when relevant.
- Explain classroom terminology alongside formal C terminology where they differ (e.g. operators as punctuators, declarations distinct from statements).
- Distinguish implementation-dependent sizes, character encodings and terminal behavior from language guarantees. Do not present typical data type sizes as universal.
- Avoid unsafe or obsolete input functions, incorrect format specifiers, invalid pointer usage and uninitialized reads. For erroneous examples, explicitly label them and explain the issue.
- Do not predict a fixed result for undefined or unspecified behavior. Do not imply that precedence dictates operand evaluation order.
- Compile and run representative complete examples with `cc -std=c17 -Wall -Wextra -pedantic` when possible. Use `-lm` where required. For intentionally newer features use the appropriate compiler mode. Do not claim a fragment is a complete program.
- Use HTML escaping for C code in markup: `&lt;`, `&gt;`, `&amp;`. Preserve C backslashes in HTML and escape them correctly in JavaScript strings.

## 5. Implementation and accessibility

- Single standalone HTML file per page: semantic HTML5, embedded CSS and vanilla JavaScript; no external fonts, libraries, APIs, tracking or backend. Content remains readable without JS; quizzes and demonstrations may require it.
- Reuse the existing CSS tokens, class names, breakpoints and components defined in `DESIGN_SYSTEM.md`. No redesign, gradients, decorative imagery, heavy animation or unnecessary CSS.
- Use headings in logical order, native buttons/links/inputs, visible focus, associated labels, `fieldset`/`legend` for quiz choices, a skip link, descriptive nav labels and live status for dynamic results.
- No horizontal page overflow at mobile widths. Allow code and wide tables to scroll within their own containers. Do not shrink body text to fit.
- Unit pages use hash navigation: `#overview`, descriptive unique lesson slugs, `#final-review`. Browser back/forward and deep links must work. Include a relative link to `index.html` labeled “All units” in the sidebar and overview.
- On mobile, navigation uses the existing Menu button and dismissible backdrop. Keep `aria-expanded` in sync and support Escape, keyboard focus and dismissal. Do not leave focus stranded in a closed menu.
- Never use `eval`, `new Function`, unsafe HTML injection or arbitrary execution of student code. Use `textContent` for user input and simulated output; validate bounds and input values. Interactive demonstrations are models, not a C compiler, unless a real compiler is explicitly implemented and documented.

## 6. Quizzes and progress contract

Match Unit 2's implementation. Topic quizzes typically contain 5–8 questions and a final review typically contains 10–15; adapt counts to syllabus breadth. Use one clearly correct option per question, four plausible choices, accurate feedback and one mark per correct answer with no negative marking. Do not reveal answers before submission. Require all answers, show score and percentage plus a useful explanation for each answer, disable answers after grading, and allow retry. Keep highest score across attempts. These are formative practice assessments, not secure examinations: answers are visible in the HTML source.

Use `.quiz[data-quiz="lesson-slug"]`, sequential `fieldset[data-q]` starting at 0, a unique radio group `lesson-slug-q0`, options with numeric values 0–3, `.feedback`, `.quiz-result`, and `.quiz-reset`. The JS `quizzes` map uses the exact slug and ordered `{correct: 0, why: "..."}` entries; `correct` is the zero-based option index. Keep number of fields, answer keys and displayed counts synchronized. Use `role="status"` for the score and explicit correct/incorrect text in addition to color.

Use independent browser storage per unit: `bca-c-unit2-v1` for existing Unit 2; use `bca-c-unit<N>-v1` for new units (numeric N without leading zero). State shape: `{done: {}, scores: {}}`; keys are stable lesson slugs, with `final-review` for final scores. Do not reset a different unit's storage. Preserve compatible data during updates; if schema changes, implement migration or disclose an intentional reset. Handle unavailable/corrupt localStorage gracefully. Progress is device/browser-specific, not synced; completion is self-reported and independent of quiz scores. Reset must require confirmation and clear only the current unit. Homepage is a directory, not a centralized gradebook.

## 7. Acceptance checklist

Before publishing or enabling a unit:

- [ ] All teacher-provided topics covered; references, examples and explanations accurate.
- [ ] Full lesson structure, demo, worked answers, quiz, final review and marking guides present.
- [ ] Question counts and marks match answer data; correct, incorrect, incomplete and retry cases work.
- [ ] Lesson completion, persistence after refresh, reset confirmation and no-storage fallback work.
- [ ] All unit, lesson and previous/next links work; no duplicate IDs or broken anchors; homepage shows only real units as active.
- [ ] At 320, 390, 768 and 1440 CSS pixels (plus around 720/900 breakpoints), page has no unintended horizontal overflow; controls and navigation remain usable.
- [ ] Keyboard focus, mobile menu, skip link, Escape, labels and readable print output checked.
- [ ] Browser console has no uncaught JS errors; offline use and JS-disabled reading tested.
- [ ] No external network dependencies; filenames and relative links suitable for GitHub Pages.
- [ ] Update documentation if the agreed implementation contract changes; report any untested items.
