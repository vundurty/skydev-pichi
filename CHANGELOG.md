# Changelog

## Release 8

- Renamed parser references to `zoarParser` and aligned parser/export behavior.
- Added raw block symbols:
  - `| { ... }` for tables
  - `+ { ... }` for accordions
  - `" { ... }` for blockquotes
  - `"i`, `"t`, `"w`, `"d` for callouts
  - `` ` { ... } `` for code blocks
  - `t { ... }` for rich text blocks
- Added multiline tolerance for raw blocks and action blocks (`~` / `:`):
  - symbol and `{` can be on same or next line
  - `}` tails and `->` tails can be on same or next line
- Added strict form/select blocks:
  - `v { ... }` select support with `#` selected option marker and blank option support
  - `f { ... } -> target` form support with required action target
  - `button-type-submit|reset|button` and `input-type-*` handling
- Reworked text styling system to `t-*` tokens and removed old text token compatibility from docs flow.
- Expanded font-weight support:
  - named weights (`t-thin` ... `t-black`)
  - numeric weights in 50-step increments (`t-50` ... `t-900`)
- Standardized background color token to `bg-color-*` and removed old `bg-*` color alias usage.
- Added gradient shorthand system:
  - `bg-gradient-a-b` and `bg-gradient-a-b-c`
  - `bg-from-*`, `bg-via-*`, `bg-to-*`
  - `bg-angle-*` and `bg-gradient-to-*`
- Added/expanded utility support for:
  - grid rows/cols and spans (`grid-rows-*`, `grid-cols-*`, `row-span-*`, `col-span-*`)
  - object/aspect utilities
  - blend/backdrop utilities (`mix-blend-*`, `backdrop-blur-*`)
  - responsive prefixes (`mobile-*`, `tablet-*`) and state prefixes (`hover-*`, `focus-*`)
- Improved module behavior and preview consistency for module edits/assets.
- Removed pop-out preview service worker flow and related dependency (`preview-sw.js`) from active UX path.
- Added preview device modes in app menu:
  - `Default`, `Desktop`, `Tablet`, `Mobile`
  - viewport behavior aligned with responsive breakpoints for preview testing.
- Reworked editor shell UX:
  - new top menu actions (new/open/save/save as/export/format/about/welcome)
  - sidebar cleanup, resizing, spacing and visual stability improvements
  - removed redundant editor/preview toolbar actions
  - added About popup with dynamic year and branding content
- Added welcome/start screen redesign:
  - full-screen onboarding layout
  - create/open project actions
  - recent project list persistence
  - templates placeholder section for future cloud templates
- Added dirty-buffer behavior across file switches (unsaved text retained in-memory until reload/exit).
- Updated language highlighting in Monaco for new symbols (`|`, `+`, `"`).
- Refreshed root documentation to match current syntax and utility structure.

## Release 7

- Updated starter template to the minimal Zoar starter layout.
- Added root `favicon.svg` handling in project setup and export flow.
- Improved browser compatibility UX for File System Access API.
- Added parser tests and e2e flow tests (create/open/save/export).
- Added CI checks for formatting, linting, parser tests, and e2e tests.
