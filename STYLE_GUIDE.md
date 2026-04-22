# Style Guide

Design rules for the Trust & Risk research website. Follow these strictly — they are enforced by code review and by the audit that ships with the repository.

Scope: this guide applies to the **main site only** (pages under `src/pages/` except `that-one-paper/`). The `/that-one-paper/` subsite is its own brand with a separate system documented in the `design_handoff_that_one_paper/` bundle.

---

## 1. Colour palette

Four colours. No exceptions.

```css
--cream:       #FFF9ED  /* Page surface */
--navy:        #003049  /* Primary ink, headings */
--burgundy:    #780000  /* Accents, emphasis, links */
--light-blue:  #669bbc  /* Secondary details */
```

### Do
- Page background: `#FFF9ED`
- Body text: `#003049`
- Headings: `#003049`
- Accents and links: `#780000`
- Secondary details: `#669bbc`
- Dark sections: `#003049` surface with `#FFF9ED` text

### Don't
- Never use `bg-white` or `#FFFFFF`. The main surface is `#FFF9ED`.
- Never put burgundy text on navy, or navy text on burgundy. The contrast fails.
- Do not introduce colours outside the palette (no `slate-*`, no grey defaults, no off-palette hex values).

### Valid combinations

| Surface  | Text     | Use                              |
|----------|----------|----------------------------------|
| `#FFF9ED`| `#003049`| Main page, light sections         |
| `#003049`| `#FFF9ED`| Dark sections, footer             |
| `#780000`| `#FFF9ED`| Active buttons, emphasis tags     |
| `#669bbc`| `#FFFFFF`| Secondary tags                    |

---

## 2. Typography

Single family: **Figtree** for everything.

- Use `font-figtree` or rely on the global default set on `html`.
- Italic emphasis uses Merriweather via `<em class="italic">` (wired in `Layout.astro`).

### Hierarchy

```
h1:    text-5xl md:text-6xl   font-bold     text-[#003049]
h2:    text-3xl md:text-4xl   font-bold     text-[#003049]
h3:    text-xl                font-semibold text-[#780000] | text-[#003049]
body:  text-base                              text-[#003049]/80
small: text-sm                                text-[#003049]/70
```

### Emphasis
- `<strong>` or `font-bold` for bold.
- `<em class="italic">` for italic nuance.
- Mix both when needed.

---

## 3. Standard components

### Primary button
```html
<button class="font-figtree px-6 py-3 bg-[#780000] text-[#FFF9ED] rounded-lg hover:bg-[#780000]/90 transition-all font-semibold">
  Label
</button>
```

### Secondary button
```html
<button class="font-figtree px-6 py-3 bg-[#FFF9ED] text-[#003049] border-2 border-[#003049] rounded-lg hover:bg-[#003049] hover:text-[#FFF9ED] transition-all font-semibold">
  Label
</button>
```

### Filter / toggle button
```html
<!-- inactive -->
<button class="font-figtree px-4 py-2 bg-[#FFF9ED] text-[#003049] border-2 border-[#003049] rounded-lg transition-all">
  Category
</button>

<!-- active -->
<button class="font-figtree px-4 py-2 bg-[#780000] text-[#FFF9ED] border-2 border-[#780000] rounded-lg transition-all">
  Category
</button>
```

### Input
```html
<input
  type="text"
  class="w-full px-6 py-4 font-figtree text-lg bg-[#FFF9ED] border-2 border-[#003049]/20 rounded-lg focus:border-[#780000] focus:outline-none focus:ring-2 focus:ring-[#780000]/20 transition-all"
  placeholder="Search..."
/>
```

Never use `bg-white` on an input. Use `bg-[#FFF9ED]`.

### Tag / badge
```html
<span class="inline-block px-3 py-1.5 bg-[#780000] text-[#FFF9ED] rounded-lg text-sm font-semibold">
  Tag
</span>
```

Important:
- Use `rounded-lg`, never `rounded-full`. A rectangle with `rounded-full` becomes a pill and violates the brand.
- No emojis inside tags or copy.

### Card
```html
<div class="bg-[#FFF9ED] border-l-4 border-[#780000] rounded-lg p-6 shadow-md hover:shadow-xl transition-all hover:-translate-y-1">
  ...
</div>
```

---

## 4. Sections

Use the shared components under `src/components/`:

- `<SectionNumbered>` for sections with a vertical side number. Alternate surface colours: odd sections use burgundy, even sections use navy.
- `<SectionBordered>` for sections accented by a left border. Border colour choices: `border-[#669bbc]`, `border-[#780000]`, or `border-[#003049]`.
- `<DarkSection>` for navy-background blocks with ivory text.

Typical snippet:

```astro
<SectionNumbered
  number="01"
  title="Section title"
  bgColor="bg-[#780000]"
  textColor="text-[#FFF9ED]"
>
  <p>Body...</p>
</SectionNumbered>
```

---

## 5. Corners and borders

- Buttons, cards, tags, inputs, section wrappers: `rounded-lg` (8px).
- `rounded-full` is reserved for genuinely square elements that should render as a circle (timeline dots, avatar frames, cursor rings). Never on rectangles.
- Default border thickness: `border-2`. Accent left border: `border-l-4`.
- Border colours: only `#003049`, `#780000`, or `#669bbc`.

---

## 6. Interactive states

### Hover
```css
hover:shadow-xl
hover:-translate-y-1
hover:bg-[#780000]/90
```

### Focus (inputs)
```css
focus:border-[#780000]
focus:outline-none
focus:ring-2
focus:ring-[#780000]/20
```

### Active (toggle buttons)
Apply via JS by toggling an `active` class that sets burgundy background, burgundy border, ivory text.

---

## 7. Responsive

Tailwind breakpoints:
- `sm`: 640px
- `md`: 768px
- `lg`: 1024px
- `xl`: 1280px

Example:

```html
<h1 class="text-4xl md:text-5xl lg:text-6xl">Title</h1>
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">...</div>
```

---

## 8. Hard rules

### Never

1. `bg-white` or `#FFFFFF`. Use `bg-[#FFF9ED]`.
2. Burgundy on navy or navy on burgundy — contrast fails.
3. `rounded-full` on rectangles — pill shape is forbidden.
4. Emojis in UI copy. Use words or inline SVG icons.
5. Fonts other than Figtree (or Merriweather for italic emphasis).
6. Colours outside `#FFF9ED / #003049 / #780000 / #669bbc`.
7. Em-dashes (`—`) in copy. Replace with commas.

### Always

1. Figtree for typography.
2. `#FFF9ED` for light surfaces.
3. `#003049` for primary text.
4. `#780000` for accents and links.
5. `rounded-lg` (8px) for all UI chrome.
6. `transition-all` on interactive elements.

---

## 9. Tag colour rotation

When rendering a list of tags, rotate through these three combinations:

```css
/* 1. Core / important */
.tag-core      { background: #780000; color: #FFF9ED; }

/* 2. Primary category */
.tag-primary   { background: #003049; color: #FFF9ED; }

/* 3. Secondary category */
.tag-secondary { background: #669bbc; color: #FFFFFF; }
```

---

## 10. Pre-commit checklist

- [ ] No `bg-white` anywhere
- [ ] No emojis in UI copy
- [ ] No `rounded-full` on rectangles
- [ ] No em-dashes (`—`) — replaced with commas
- [ ] Only the approved palette
- [ ] Only Figtree (plus Merriweather for `em.italic`)
- [ ] No burgundy on navy or navy on burgundy
- [ ] Hover transitions on interactive elements
- [ ] Responsive breakpoints (`md:`, `lg:`) used where relevant
