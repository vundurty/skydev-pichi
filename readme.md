# zoar

A lightweight, human-readable shorthand for building websites. Write clean, readable code and see your page come to life instantly — no HTML tags, no CSS files, no build steps.

> Built by **Sudeep Vundurty**. A project of Shepherd Games Private Limited.

---

## What is zoar?

zoar is a symbolic web language designed to bridge the gap between abstract ideas and functional UI. It compiles to clean HTML and CSS, runs entirely in the browser with no dependencies, and is fast by default.

- ✦ **No boilerplate** — every line does something visible
- ✦ **Live preview** — changes render instantly as you type
- ✦ **Local first** — your files live on your PC, no cloud required
- ✦ **Fast output** — exports pure HTML/CSS, no JavaScript runtime

---

## The Editor

zoar comes with a built-in Monaco-powered editor (the same engine as VS Code) with:

- Syntax highlighting for all zoar tokens
- Auto-closing brackets and smart indentation
- Live preview pane with scroll position preserved
- Multi-page project support
- Asset manager — upload images, fonts, audio, and video
- Pop-out preview window for full DevTools inspection
- `Ctrl+S` to save, `Shift+Alt+F` to format

---

## Syntax

Every `.zoar` file is a page. Each line is an element. Styles go inside `[square brackets]`. Layout uses `{ curly braces }`.

### Elements

| Symbol | Output | Example |
|--------|--------|---------|
| `#` | `<h1>` | `# Hello World [bold text-size-40]` |
| `##` | `<h2>` | `## Subheading [text-size-28]` |
| `###` | `<h3>` | `### Small heading` |
| `t` | `<p>` | `t Some paragraph text. [text-color-666666]` |
| `:` | `<button>` | `: Click me [bg-111111 text-color-ffffff inner-12 round-8]` |
| `~` | `<a>` | `~ Visit us -> https://zoar.dev [text-color-ffb020 bold]` |
| `>` | `<img>` | `> photo.jpg [w-full round-12]` |
| `>>` | `<audio controls>` | `>> audio.mp3 [w-full]` |
| `>>>` | `<video controls>` | `>>> video.mp4 [w-full round-12]` |
| `<<` | `<iframe>` | `<< https://youtube.com/embed/xyz [w-full h-400 round-12]` |
| `-` | `<ul><li>` | `- Item one` |
| `1.` | `<ol><li>` | `1. First step` |
| `/` | `<label>` | `/ Your name [bold text-size-14]` |
| `_` | `<input>` | `_ Placeholder [border-1 round-8 inner-12]` |
| `__` | `<textarea>` | `__ Write here... [border-1 round-8 inner-12 h-160]` |
| `s` | `<summary>` | `s What is zoar?` |
| `h` | table header row | `h Name, Age, City` |
| `---` | `<hr>` | `---` |
| `--` | `<br>` | `--` |
| `{ }` | `<div>` | `{ ... } [flex col gap-16]` |
| `//` | comment | `// This line is ignored` |

### Navigation & Links

Use `-> /page` on any button or link to navigate. External URLs open in a new tab automatically.

```
// Button navigation (renders as <button>)
: About us -> /about [bg-ffb020 text-color-ffffff inner-12 round-8]

// Inline link (renders as <a>)
~ Read the docs -> /docs [text-color-ffb020 underline]

// External link — opens in new tab
~ Visit us -> https://zoar.dev [bold]

// Email link
~ Contact -> mailto:contact@shepherd.games
```

The filename maps directly to the route — `about.zoar` → `/about`.

### Metadata

Add a `----` block at the very top of any `.zoar` file to set page metadata. It never appears on the page itself.

```
----
title: My Page
description: A short description for search engines.
author: Your Name
lang: en
favicon: favicon.svg
og-title: My Page
og-description: Shown when shared on social media.
og-image: assets/cover.jpg
twitter-card: summary_large_image
canonical: https://mysite.com/page
----
```

### Table

Wrap rows in `{ }` and add `[table]` to the closing brace. Use `h` for a header row.

```
{
    h Feature, Free, Pro
    Live Preview, ✓, ✓
    Custom Fonts, ✓, ✓
    Priority Support, ✗, ✓
} [table]
```

No `h` line = no header, plain rows only.

### Blockquote

Use any block with `[blockquote]` on the closing brace:

```
{
    t Design is not just what it looks like. Design is how it works. [italic leading-28]
    t — Steve Jobs [text-size-13 bold text-color-888888 outer-t-8]
} [blockquote]
```

### Accordion

Wrap child blocks in an outer block with `[accordion]`. Use `s` for the clickable summary title.

```
{
    {
        s What is zoar?
        t A markup language for building websites without writing CSS.
    }
    {
        s Do I need to know HTML?
        t No. zoar handles all the HTML and CSS for you.
    }
} [accordion]
```

### Embeds & iframes

Use `<<` to embed any URL — YouTube, Google Maps, Figma, CodePen, or any other embeddable content. Just grab the `src` URL from the embed code — zoar handles all the iframe attributes automatically.

```
// YouTube video
<< https://www.youtube.com/embed/dQw4w9WgXcQ [w-full h-400 round-12]

// Google Map
<< https://www.google.com/maps/embed?pb=... [w-full h-300 round-8]

// Figma prototype
<< https://www.figma.com/embed?embed_host=share&url=... [w-full h-600]
```

All standard style tokens work — `w-`, `h-`, `round-`, `border-`, `shadow-` etc.

### Custom Fonts

Upload any font file (`.ttf`, `.woff2`, `.otf`, `.woff`) via the Assets panel. The utility name is derived from the filename — lowercased, spaces and underscores become hyphens.

```
// Upload roboto.woff2 → use font-roboto
# Hello [font-roboto bold text-size-48]

// Upload Playfair Display.ttf → use font-playfair-display
t Body text [font-playfair-display text-size-16]

// Apply to an entire block
} [font-roboto flex col gap-16]
```

### Forms

Input type is set via `input-type-*` inside `[...]` alongside other styles:

```
/ Full name [bold text-size-14]
_ Your name [border-1 round-8 inner-12 w-full]

/ Email [bold text-size-14]
_ name@email.com [input-type-email border-1 round-8 inner-12 w-full]

/ Password [bold text-size-14]
_ Password [input-type-password border-1 round-8 inner-12 w-full]

_ [input-type-checkbox]
_ [input-type-radio]

__ Tell us more... [border-1 round-8 inner-12 w-full h-160]
```

Supported input types: `text` (default), `email`, `password`, `number`, `tel`, `url`, `date`, `time`, `file`, `range`, `color`, `search`, `checkbox`, `radio`.

### Lists

Consecutive `-` lines auto-group into `<ul>`. Consecutive `1.` lines auto-group into `<ol>`.

```
- Landing pages
- Portfolio sites
- Documentation

1. Open a project folder
2. Edit home.zoar
3. See it live instantly
```

### Styles

All styles go inside `[...]`. Numbers are always in `px` unless noted.

#### Spacing
```
inner-20          padding: 20px
inner-x-20        padding-left/right: 20px
inner-y-20        padding-top/bottom: 20px
inner-t-20        padding-top: 20px
inner-b-20        padding-bottom: 20px
inner-l-20        padding-left: 20px
inner-r-20        padding-right: 20px

outer-20          margin: 20px
outer-x-20        margin-left/right: 20px
outer-y-20        margin-top/bottom: 20px
outer-t-20        margin-top: 20px

gap-16            gap: 16px
gap-x-16          column-gap: 16px
gap-y-16          row-gap: 16px
```

#### Sizing
```
w-200             width: 200px
w-full            width: 100%
w-1/2             width: 50%
w-screen          width: 100vw
h-400             height: 400px
h-screen          height: 100vh
min-w-300         min-width: 300px
max-w-800         max-width: 800px
min-h-200         min-height: 200px
max-h-600         max-height: 600px
```

#### Typography
```
text-size-18      font-size: 18px
text-color-ff0000 color: #ff0000
leading-28        line-height: 28px
tracking-2        letter-spacing: 0.02em

bold              font-weight: 700
semi-bold         font-weight: 600
italic            font-style: italic
underline         text-decoration: underline
no-underline      text-decoration: none
strikethrough     text-decoration: line-through
caps              text-transform: uppercase
lowercase         text-transform: lowercase
capitalize        text-transform: capitalize

text-left         text-align: left
text-center       text-align: center
text-right        text-align: right
truncate          overflow: hidden; text-overflow: ellipsis; white-space: nowrap
no-wrap           white-space: nowrap

font-roboto       font-family: 'roboto', sans-serif  (custom font from assets/)
```

#### Colors
Use any CSS color name (`red`, `blue`) or a hex code **without** the `#`:
```
bg-ffffff         background-color: #ffffff
bg-red            background-color: red
text-color-333    color: #333
border-color-ddd  border-color: #ddd
shadow-color-000  shadow color: #000
outline-color-blue outline-color: blue
```

#### Layout & Flex
```
flex              display: flex
grid              display: grid
block             display: block
inline            display: inline
inline-flex       display: inline-flex
hidden            display: none
row               flex-direction: row
col               flex-direction: column
wrap              flex-wrap: wrap
nowrap            flex-wrap: nowrap
grow              flex-grow: 1
shrink            flex-shrink: 1
center            align-items + justify-content: center
between           justify-content: space-between
justify-start     justify-content: flex-start
justify-end       justify-content: flex-end
justify-evenly    justify-content: space-evenly
items-center      align-items: center
items-start       align-items: flex-start
items-end         align-items: flex-end
self-center       align-self: center
grid-cols-3       grid-template-columns: repeat(3, 1fr)
grid-rows-2       grid-template-rows: repeat(2, 1fr)
col-span-2        grid-column: span 2
col-span-full     grid-column: 1 / -1
```

#### Borders & Radius
```
border            border: 1px solid #ddd
border-2          border-width: 2px; border-style: solid
border-color-000  border-color: #000
border-t-1        border-top: 1px solid
border-b-1        border-bottom: 1px solid
border-l-1        border-left: 1px solid
border-r-1        border-right: 1px solid
round-8           border-radius: 8px
round-full        border-radius: 9999px
outline-color-blue outline-color: blue
outline-width-2   outline: 2px solid
outline-none      outline: none
```

#### Effects
```
shadow-12         box-shadow: 0 4px 12px rgba(0,0,0,0.15)
shadow-none       box-shadow: none
opacity-50        opacity: 0.5
blur-8            filter: blur(8px)
brightness-75     filter: brightness(0.75)
overflow-hidden   overflow: hidden
overflow-scroll   overflow: scroll
overflow-auto     overflow: auto
overflow-x-hidden overflow-x: hidden
overflow-y-auto   overflow-y: auto
```

#### Position
```
relative          position: relative
absolute          position: absolute
fixed             position: fixed
sticky            position: sticky
top-0             top: 0px
right-20          right: 20px
bottom-0          bottom: 0px
left--10          left: -10px  (negative = double dash)
inset-0           inset: 0
z-10              z-index: 10
```

#### Transforms
```
scale-110         transform: scale(1.1)
scale-90          transform: scale(0.9)
rotate-45         transform: rotate(45deg)
rotate--45        transform: rotate(-45deg)
translate-x-10    transform: translateX(10px)
translate-y--4    transform: translateY(-4px)
```

Multiple transforms combine automatically:
```
[scale-105 rotate-2 translate-y--4]
→ transform: scale(1.05) rotate(2deg) translateY(-4px)
```

#### Transitions
```
transition            transition: all 0.3s ease
transition-colors     color, background, border only
transition-transform  transform only
transition-opacity    opacity only
duration-200          transition-duration: 200ms
ease-in               timing: ease-in
ease-out              timing: ease-out
ease-in-out           timing: ease-in-out
```

#### Interactivity
```
cursor-pointer        cursor: pointer
cursor-not-allowed    cursor: not-allowed
cursor-grab           cursor: grab
select-none           user-select: none
select-all            user-select: all
pointer-none          pointer-events: none
disabled              opacity: 0.5; cursor: not-allowed
```

### State Prefixes

Prefix **any** utility with `hover-`, `focus-`, `mobile-`, or `tablet-`:

```
hover-bg-000000           on :hover → background-color: #000
hover-text-color-fff      on :hover → color: #fff
hover-scale-105           on :hover → transform: scale(1.05)
hover-shadow-20           on :hover → box-shadow: ...
focus-outline-color-blue  on :focus → outline-color: blue
mobile-text-size-16       @media (max-width: 640px)
mobile-col                @media (max-width: 640px) → flex-direction: column
tablet-grid-cols-2        @media (max-width: 1024px)
```

---

## Example

```
----
title: Home
description: Welcome to my zoar site.
favicon: favicon.svg
og-image: assets/cover.jpg
----

// Navbar
{
    > logo.png [h-28]
    {
        : Home [text-color-555555 inner-8 round-6 hover-bg-f5f5f5 transition]
        : About -> /about [text-color-555555 inner-8 round-6 hover-bg-f5f5f5 transition]
    } [flex row gap-4]
    : Get Started [bg-ffb020 text-color-ffffff inner-y-10 inner-x-20 round-8 hover-bg-e6a000 transition]
} [flex row items-center justify-between inner-x-40 inner-y-16 border-b-1 border-color-eeeeee sticky top-0 z-100]

// Hero
{
    # Build websites without writing CSS. [text-size-52 bold text-color-111111 leading-60 max-w-700]
    t A new way to design for the web. [text-size-18 text-color-666666 leading-32]
    {
        : Start Building [bg-ffb020 text-color-ffffff inner-y-14 inner-x-32 round-10 hover-bg-e6a000 transition]
        ~ Read the Docs -> /docs [text-color-111111 inner-y-14 inner-x-32 round-10 border-1 border-color-dddddd hover-bg-f5f5f5 transition]
    } [flex row gap-12]
} [flex col gap-24 inner-x-40 inner-y-96 max-w-800]

> hero.jpg [w-full h-400]

---

// FAQ
{
    {
        s What is zoar?
        t A markup language for building websites without writing CSS.
    }
    {
        s Is it free?
        t Yes, completely free to use.
    }
} [accordion outer-x-40]
```

---

## Modules

Modules let you write a piece of UI once and reuse it across every page — navbars, footers, banners, anything.

### Creating a Module

Modules live in a `modules/` subfolder inside your project. Create one from the **Modules** panel in the editor (click **+**), or add a `modules/footer.zoar` file manually.

```
modules/
├── navbar.zoar
└── footer.zoar
```

### Using a Module

Reference a module anywhere in a page using `@modules/name` on its own line:

```
@modules/navbar

# Hello World

t Welcome to my site.

@modules/footer
```

### Rules

- Module name = filename without `.zoar` (e.g. `footer.zoar` → `@modules/footer`)
- Modules can contain any zoar syntax — headings, blocks, buttons, images, etc.
- Modules can **not** be nested
- Frontmatter (`----` block) inside a module is ignored
- On export, modules are inlined into every page — no separate files in the ZIP

---

## File Structure

```
my-project/
├── home.zoar        →  /
├── about.zoar       →  /about
├── contact.zoar     →  /contact
├── favicon.svg
├── logo.png
└── assets/
    ├── hero.jpg
    └── roboto.woff2
```

---

© 2026 Shepherd Games Private Limited