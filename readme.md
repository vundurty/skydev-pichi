# zoar

A symbolic, local-first language for building static websites fast.

Write `.zoar` files with compact syntax, preview instantly, and export clean HTML + CSS.

---

## What Zoar Is

Zoar is a shorthand layer over HTML and CSS:

- One line = one element
- Styles live in `[ ... ]`
- Layout/content blocks use `{ ... }`
- No framework/runtime in export
- Works locally with instant preview

---

## Editor Workflow

1. Create or open a local project folder.
2. Edit `.zoar` pages/modules in Monaco.
3. Save to refresh preview.
4. Export static site (HTML/CSS + assets).

Built-in editor features include:

- Welcome/start screen with recent projects
- Pages/modules/assets sidebar
- Live preview modes: `Default`, `Desktop`, `Tablet`, `Mobile`
- File formatting, save/save-as, export
- Asset and custom font support

---

## File Structure

Typical project:

```txt
home.zoar
about.zoar
modules/
  navbar.zoar
assets/
  logo.png
  demo.mp4
  inter.woff2
```

Routing:

- `home.zoar` => `/`
- `about.zoar` => `/about`
- nested page `docs/getting-started.zoar` => `/docs/getting-started`

Modules:

```zoar
@modules/navbar
```

`@modules/<name>` injects `modules/<name>.zoar` content.

---

## Frontmatter

Optional metadata at the top of a page:

```zoar
----
title: My Page
description: Page description
lang: en
author: Your Name
favicon: favicon.svg
og-title: My Page
og-description: Shared preview text
og-image: logo.png
twitter-card: summary_large_image
canonical: https://example.com/my-page
----
```

---

## Syntax (Current)

## Core Elements

| Symbol | Output | Example |
|---|---|---|
| `#` | `<h1>` | `# Title [t-size-40 t-bold]` |
| `##` | `<h2>` | `## Section` |
| `###` | `<h3>` | `### Subsection` |
| `t` | `<p>` | `t Paragraph text [t-color-666666]` |
| `:` | `<button>` | `: Click me [bg-color-111111 t-color-ffffff]` |
| `~` | `<a>` | `~ Docs -> /docs [t-nounderline]` |
| `>` | `<img>` | `> logo.png [w-120]` |
| `>>` | `<audio controls>` | `>> demo.mp3 [w-full]` |
| `>>>` | `<video controls>` | `>>> demo.mp4 [w-full aspect-video]` |
| `<<` | `<iframe>` | `<< https://example.com [w-full h-400]` |
| `/` | `<label>` | `/ Email` |
| `_` | `<input>` | `_ Enter email [input-type-email]` |
| `__` | `<textarea>` | `__ Message [min-h-120]` |
| `-` | `<ul><li>` | `- Item` |
| `1.` | `<ol><li>` | `1. Step one` |
| `---` | `<hr>` | `---` |
| `--` | `<br />` | `--` |
| `{ ... }` | `<div>` | `{ t Box } [inner-16 round-8]` |
| `//` | comment | `// ignored` |

Unknown plain lines fall back to inline text (`<span>`).

## Block Symbols

Modern block syntax (preferred):

### Table

```zoar
| {
  # Name, Role
  Sudeep, Founder
  Zoar, Product
} [max-w-720]
```

- Header row uses `# `.
- Commas split columns.
- Literal `{ }` text inside cells is preserved.

### Accordion

```zoar
+ {
  {
    # Item One
    t Body one
  }
  {
    # Item Two
    t Body two
  }
} [w-full]
```

### Blockquote

```zoar
" {
  t Quoted content
  ~ Source -> https://zoar.dev
} [inner-16]
```

### Callouts

```zoar
"i { t Info message }
"t { t Tip message }
"w { t Warning message }
"d { t Danger message }
```

Variants:

- `"i` => info
- `"t` => tip
- `"w` => warning
- `"d` => danger

Legacy class-based callouts still parse (`[callout-*]`), but symbol form is preferred.

### Code Block

```zoar
` {
  # js
  const x = 1;
  if (x) {
    console.log("ok");
  }
} [w-full]
```

- First `# ...` line is code header/language label.
- Inner braces in code are treated as code text.

### Rich Text Block

```zoar
t {
  # Title inside block
  t paragraph
  Plain line auto-converts to paragraph
} [t-italic]
```

- Supports nested Zoar syntax inside.
- Plain lines are auto-promoted to `t ...` inside rich blocks.

### Select

```zoar
v {
  item 1
  # item 2
  item 3
} [w-full]
```

- `# option` marks selected option.
- If no `#`, first option is selected.
- Blank options are supported (including first/last lines).

### Form

```zoar
f {
  / Email
  _ Enter email [input-type-email]
  : Submit
  : Reset [button-type-reset]
} -> https://httpbin.org/post [w-full]
```

- `-> action` is required for `f` blocks.
- Default form method is `post`.
- `button-type-submit|reset|button` supported on `:`.

---

## Multiline Placement Rules

For raw block symbols (`|`, `+`, `"`, `"i/t/w/d`, `` ` ``, `t`, `v`, `f`, `~`, `:`):

- Symbol and `{` can be same line or next line.
- Closing `}` and style tail can be same line or next line.
- For action blocks (`~`, `:`, `f`), `-> ...` tail can be same line or next line.

Example forms all parse:

```zoar
~ { > logo.png } -> /home

~
{
  > logo.png
}
-> /home [cursor-pointer]
```

---

## Styling Format

Use utility tokens in square brackets:

```zoar
t Hello [t-size-18 t-color-222222 t-leading-28]
```

Rules:

- Tokens are space-separated.
- Unknown tokens pass through as CSS classes.
- Old text tokens (`bold`, `text-size-*`, etc.) are deprecated/ignored.
- Use `id-<name>` to set element id from style list.

### Responsive + State Prefixes

- `hover-*` => `:hover`
- `focus-*` => `:focus`
- `mobile-*` => `@media (max-width: 640px)`
- `tablet-*` => `@media (max-width: 1024px)`

Example:

```zoar
~ Docs -> /docs [t-color-555555 hover-t-color-111111 mobile-hidden]
```

---

## Utility Reference (Current)

## Layout (static tokens)

- `flex`, `grid`, `block`, `inline`, `inline-flex`, `hidden`
- `row`, `col`, `wrap`, `nowrap`
- `grow`, `shrink`, `no-grow`, `no-shrink`
- `center`, `between`
- `justify-start|end|center|between|around|evenly`
- `items-start|end|center|baseline|stretch`
- `self-start|end|center|stretch`

## Spacing

- `inner-<n>`, `inner-x-<n>`, `inner-y-<n>`, `inner-t/l/r/b-<n>`
- `outer-<n>`, `outer-x-<n>`, `outer-y-<n>`, `outer-t/l/r/b-<n>`
- `gap-<n>`, `gap-x-<n>`, `gap-y-<n>`

## Sizing

- `w-*`, `h-*`, `min-w-*`, `max-w-*`, `min-h-*`, `max-h-*`
- Supports px numbers, fractions (`1/2`), `full`, `screen`
- `basis-*`, `basis-auto`

## Typography (`t-*`)

- Size/color: `t-size-*`, `t-color-*`
- Rhythm: `t-leading-*`, `t-tracking-*`
- Align: `t-left|right|center|justify`
- Decoration: `t-underline`, `t-nounderline`, `t-strikethrough`
- Transform: `t-caps`, `t-lowercase`, `t-capitalize`
- Wrapping: `t-nowrap`, `t-prewrap`, `t-breakword`, `t-truncate`
- Style: `t-italic`
- Weights:
  - Named: `t-thin`, `t-extralight`, `t-light`, `t-regular`, `t-medium`, `t-semibold`, `t-bold`, `t-extrabold`, `t-black`
  - Numeric: `t-50` up to `t-900` in steps of 50
- Font family: `font-<asset-name>`

## Background + Gradient

- `bg-color-*`
- `bg-opacity-*`
- `bg-cover`, `bg-contain`, `bg-center`, `bg-no-repeat`
- Gradient forms:
  - `bg-gradient`
  - `bg-from-*`, `bg-via-*`, `bg-to-*`
  - `bg-angle-<number|t|r|b|l|tl|tr|bl|br>`
  - `bg-gradient-to-<t|r|b|l|tl|tr|bl|br>`
  - shorthand: `bg-gradient-a-b` or `bg-gradient-a-b-c`

## Border/Radius/Outline

- `border`, `border-<n>`, `border-width-<n>`
- `border-color-*`, `border-style-*`
- `border-t/b/l/r-<n>`
- `round`, `round-<n>`, `round-sm|lg|xl|full`, `pill`
- `outline`, `outline-none`, `outline-width-*`, `outline-color-*`

## Effects

- `shadow`, `shadow-none`, `shadow-<n>`, `shadow-color-*`
- `opacity-*`, `blur-*`, `brightness-*`
- `backdrop-blur-*`
- `mix-blend-normal|multiply|screen|overlay|...`

## Position/Z/Overflow

- `relative`, `absolute`, `fixed`, `sticky`, `static`, `isolate`
- `top/right/bottom/left/inset-<n>`
- `z-auto`, `z-<n>`
- `overflow-hidden|scroll|auto|visible`
- `overflow-x-hidden`, `overflow-y-auto|scroll`

## Transform/Transition

- `scale-*`, `rotate-*`, `translate-x-*`, `translate-y-*`
- `transition`, `transition-colors`, `transition-transform`, `transition-opacity`
- `duration-*`
- `ease-linear|in|out|in-out`

## Interaction + Order

- `cursor-pointer|default|not-allowed|grab`
- `select-none|all`
- `pointer-none`
- `disabled`
- `order-<n>`, `order-first|last|none`
- `content-start|end|center|between|around|evenly|stretch`

## Media + Grid helpers

- `object-cover|contain|fill|none|scale-down`
- `object-center|top|bottom|left|right`
- `aspect-<w>/<h>`, `aspect-square`, `aspect-video`, `aspect-auto`
- `grid-cols-<n>`, `grid-rows-<n>`
- `col-span-<n|full>`, `row-span-<n|full>`

## Input/Button helpers

- `input-type-*` on `_`
- `button-type-submit|reset|button` on `:`

---

## Navigation Semantics

- Internal `-> /page` uses editor bridge in preview (`loadFile`) and exports to static links.
- External `http...` / `mailto:` open in new tab for links/buttons.
- Anchor links `#section` are supported.

---

## Example Starter

```zoar
----
title: Zoar Starter
description: Minimal example
lang: en
----

{
  # Build websites without writing CSS [t-size-42 t-bold t-center]
  t Zoar compiles to clean HTML + CSS [t-size-18 t-color-666666 t-center]
  {
    ~ Docs -> /docs [t-nounderline t-color-111111 border-1 border-color-dddddd inner-y-10 inner-x-16 round-8]
    : Open Editor -> https://editor.zoar.dev [bg-color-ffb020 t-color-ffffff inner-y-10 inner-x-16 round-8]
  } [flex row gap-10 items-center mobile-col]
} [flex col gap-20 items-center inner-x-24 inner-y-64]
```

---

## Notes

- Parser is strict for `f` blocks: they must resolve to `f { ... } -> target`.
- Deprecated text tokens are ignored in current builds (use `t-*` equivalents).
- Unknown style tokens are preserved as class names for custom CSS hooks.

