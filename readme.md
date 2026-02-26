# Skydev

A lightweight, human-readable shorthand for building websites. Write clean, readable code and see your page come to life instantly — no HTML tags, no CSS files, no build steps.

> Built and maintained by **Shepherd Games Private Limited**.

---

## What is Skydev?

Skydev is a symbolic web language designed to bridge the gap between abstract ideas and functional UI. It compiles to clean HTML and CSS, runs locally with no dependencies, and is fast by default.

- ✦ **No boilerplate** — every line does something visible
- ✦ **Live preview** — changes render instantly as you type
- ✦ **Local first** — your files live on your PC, no cloud required
- ✦ **Fast output** — exports pure HTML/CSS, no JavaScript runtime

---

## The Editor

Skydev comes with a built-in Monaco-powered editor (the same engine as VS Code) with:

- Syntax highlighting for all Skydev tokens
- Auto-closing brackets and smart indentation
- Live preview pane
- Multi-page project support
- `Ctrl+S` to save, `Shift+Alt+F` to format

---

## Syntax

Every `.sd` file is a page. Each line is an element. Styles go inside `[square brackets]`. Layout uses `{ curly braces }`.

### Elements

| Symbol | Output | Example |
|--------|--------|---------|
| `#` | `<h1>` | `# Hello World [bold text-size-40]` |
| `##` | `<h2>` | `## Subheading [text-size-28]` |
| `###` | `<h3>` | `### Small heading` |
| `t` | `<p>` | `t Some paragraph text. [text-color-666666]` |
| `:` | `<button>` | `: Click me [bg-black text-color-white inner-12 round-8]` |
| `img` | `<img>` | `img photo.jpg [w-full round-12]` |
| `{ }` | `<div>` | `{ ... } [flex col gap-16]` |
| `//` | comment | `// This line is ignored` |

### Navigation

Use `-> /page` on any button to link to another page:

```
: About us -> /about [bg-4f9eff text-color-white inner-12 round-8]
```

The filename maps directly to the route — `about.sd` → `/about`.

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
strikethrough     text-decoration: line-through
caps              text-transform: uppercase
lowercase         text-transform: lowercase
capitalize        text-transform: capitalize

text-left         text-align: left
text-center       text-align: center
text-right        text-align: right
truncate          overflow: hidden; text-overflow: ellipsis; white-space: nowrap
no-wrap           white-space: nowrap
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
hidden            display: none
row               flex-direction: row
col               flex-direction: column
wrap              flex-wrap: wrap
grow              flex-grow: 1
center            align-items + justify-content: center
between           justify-content: space-between
justify-start     justify-content: flex-start
justify-end       justify-content: flex-end
justify-evenly    justify-content: space-evenly
items-center      align-items: center
items-start       align-items: flex-start
items-end         align-items: flex-end
grid-cols-3       grid-template-columns: repeat(3, 1fr)
grid-rows-2       grid-template-rows: repeat(2, 1fr)
col-span-2        grid-column: span 2
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
pointer-none          pointer-events: none
disabled              opacity: 0.5; cursor: not-allowed
```

### State Prefixes

Prefix **any** utility with `hover-`, `focus-`, `mobile-`, or `tablet-`:

```
hover-bg-000000        on :hover → background-color: #000
hover-text-color-fff   on :hover → color: #fff
hover-scale-105        on :hover → transform: scale(1.05)
hover-shadow-20        on :hover → box-shadow: ...
focus-outline-color-blue  on :focus → outline-color: blue
mobile-text-size-16    @media (max-width: 640px)
mobile-col             @media (max-width: 640px) → flex-direction: column
tablet-grid-cols-2     @media (max-width: 1024px)
```

---

## Example

```skydev
// Navbar
{
    # MySite [text-size-18 bold text-color-111111]
    {
        : Home [text-color-555 inner-8 round-6 hover-bg-f5f5f5 transition]
        : About -> /about [text-color-555 inner-8 round-6 hover-bg-f5f5f5 transition]
    } [flex row gap-4]
    : Get Started [bg-111111 text-color-white inner-y-10 inner-x-20 round-8 hover-bg-333 transition]
} [flex row items-center justify-between inner-x-40 inner-y-16 border-b-1 border-color-eeeeee sticky top-0 z-100]

// Hero
{
    # Build websites without writing CSS. [text-size-52 bold text-color-111111 leading-60 max-w-700]
    t A new way to design for the web. [text-size-18 text-color-666666 leading-32]
    {
        : Start Building [bg-111111 text-color-white inner-y-14 inner-x-32 round-10 hover-bg-333 transition]
        : Read the Docs -> /docs [border-1 inner-y-14 inner-x-32 round-10 hover-bg-f5f5f5 transition]
    } [flex row gap-12]
} [flex col gap-24 inner-x-40 inner-y-96 max-w-800]
```

---

## File Structure

```
my-project/
├── home.sd        →  /
├── about.sd       →  /about
├── contact.sd     →  /contact
└── blog.sd        →  /blog
```

---

## Running the Server

Skydev runs on Deno:

```bash
deno run --allow-net --allow-read server.ts
```

Then open `http://localhost:8080` in your browser.

---

## License & Attribution

- **The Syntax** — Free to use for personal and commercial projects.
- **The Software** — Distributed as-is.
- **The Source** — Currently private. Open-source release planned.

If you build a tool using the Skydev syntax, please credit the original specification.
Any output generated by this tool should ideally retain a `// Built with Skydev` comment.

---

© 2025 Shepherd Games Private Limited