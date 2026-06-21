# Auron Template Conversion Strategy to Arabic and RTL

## 1) Final Objective

The objective is not merely to “translate a website,” but to **fully re-stabilize the presentation layer** so that the Arabic version becomes:

- visually stable
- faithful to the original composition in quality and feel
- structurally compatible with RTL
- free from layout collapse caused by direction flipping
- free from image, card, slider, and navigation distortions
- preserved in the same premium visual language as the English version

This strategy is built on one clear principle:  
**Arabic and RTL conversion must change reading direction, not the identity of the design.**

---

## 2) Diagnose the template structure before execution

The supplied template is not a single simple page; it is a complete system composed of:

- **15 HTML files**
  - `index.html`
  - `about-us.html`
  - `services.html`
  - `service-details.html`
  - `projects.html`
  - `project-details.html`
  - `blog.html`
  - `single-post.html`
  - `testimonials.html`
  - `faq.html`
  - `pricing-plan.html`
  - `contact-us.html`
  - `careers.html`
  - `our-expertise.html`
  - `404.html`

- **Main CSS**
  - `css/style.css`

- **CSS libraries**
  - `css/vendor/bootstrap.min.css`
  - `css/vendor/aos.css`
  - `css/vendor/slick.css`
  - `css/vendor/fancybox.css`
  - `css/vendor/bootstrap-icons.min.css`

- **Core JavaScript**
  - `js/script.js`
  - `js/script-counter.js`
  - `js/submit-form.js`

- **JavaScript libraries**
  - `js/vendor/jquery.min.js`
  - `js/vendor/bootstrap.bundle.min.js`
  - `js/vendor/aos.js`
  - `js/vendor/slick.min.js`
  - `js/vendor/fancybox.umd.js`

- **PHP form handler**
  - `php/form_process.php`

- **Multiple images and icons** tied to the visual identity and content structure

This means the RTL conversion must be done across **four interlocking layers**:
1. HTML structure
2. Bootstrap layout
3. Custom CSS system
4. JavaScript behavior

Any partial fix to only one layer will create an Arabic version that appears translated but is not structurally stable.

---

## 3) The governing principle of the conversion

Before changing anything, adopt the following rule:

### Do not rely on:
- flipping the entire page only through `dir="rtl"`
- adding a random `rtl.css` on top of the original design
- replacing text without revisiting spacing and position
- using `transform: scaleX(-1)` at page level
- changing container direction without reviewing sliders, overlays, and absolute elements

### Do rely on:
- converting the **visual geometry** element by element
- converting **physical properties** to **logical properties** wherever possible
- building a **dedicated RTL layer** on top of the original rather than patching blindly
- reviewing every `absolute`, `relative`, `fixed`, `transform`, and `overflow` dependency
- re-tuning every direction-sensitive component: navbar, breadcrumbs, cards, sliders, accordions, forms, footers, hero blocks

---

## 4) Highest-priority execution strategy

## Phase 0: Freeze the English version as a visual reference

### Goal
Prevent accidental changes that damage the original template.

### Execution
1. Create a fixed reference copy of the English template.
2. Document the current look of every page:
   - home page
   - services page
   - projects page
   - blog page
   - contact page
   - FAQ page
3. Capture screenshots of each section in:
   - desktop
   - tablet
   - mobile
4. Document the positions of:
   - long headings
   - images with critical aspect ratios
   - buttons
   - icons
   - dropdowns
   - cards
   - footer blocks
   - sliders
   - absolute visual blocks

### Outputs
- Untouched visual reference
- Before/after comparison matrix
- A list of RTL-sensitive components

---

## Phase 1: Build the language and direction structure

### 1.1 Separate Arabic from English
The best approach is to avoid mixing both versions in the same page without strict control.  
Use one of the following:

#### Preferred option
- Separate folder, such as:
  - `/ar/`
  - `/en/`

#### Or
- Paired files:
  - `index-ar.html`
  - `about-us-ar.html`
  - etc.

### 1.2 Set the HTML root
In the Arabic version:

```html
<html lang="ar" dir="rtl">
```

### 1.3 Set the `<body>`
Add Arabic-specific classes such as:
- `rtl`
- `lang-ar`
- `is-arabic`

### 1.4 Do not rely on `dir="rtl"` alone
Because `dir` changes the default text direction, but it does not solve:
- `left/right` positions
- grid offsets
- floating decorations
- slider arrows
- overlay positions
- spacing utilities
- icon alignment
- dropdown positioning

---

## Phase 2: Convert Bootstrap correctly

The template is built on Bootstrap 5.  
In the Arabic version, Bootstrap must be treated as a **geometric layer**, not just a styling library.

### 2.1 Use Bootstrap RTL
Do not use the raw Bootstrap LTR build.  
The Arabic version should rely on:
- Bootstrap RTL build
- or a custom build with native RTL support

### 2.2 Review the heavily used utilities
Based on the analysis, the template relies heavily on:
- `ms-*` / `me-*`
- `ps-*` / `pe-*`
- `text-md-start`
- `justify-content-start`
- `justify-content-end`
- `flex-row`
- `flex-md-row`
- `align-items-*`
- `gap-*`
- `col-*`
- `offset-*`
- `dropdown-menu`
- `navbar`
- `offcanvas`
- `breadcrumb-item`

### 2.3 Conversion rule
Every utility in the Arabic version must be reviewed with the following principle:
- use `start` and `end` instead of `left` and `right`
- `me` and `ms` must be checked in the context of direction
- icon placement must be mirrored logically, not just visually

### 2.4 The most dangerous Bootstrap mistake
The page may appear to work, but:
- columns may reverse unintentionally
- CTA buttons may stretch or overlap
- the navbar may break in small screens
- dropdowns may open in the wrong place
- the offcanvas may appear from the wrong side

### 2.5 Implementation recommendation
- Use Bootstrap RTL
- Then add a template-specific override layer
- Then review every utility class in every page

---

## Phase 3: Build an Arabic CSS layer on top of the original

This is the most important phase.  
The analysis showed a large number of physical properties that will break RTL if they are not handled correctly.

## 3.1 Real CSS problems found

### a) Absolute/relative placements tied to left and right
There are many rules such as:
- `left: 0`
- `right: 0`
- `left: 50px`
- `right: 62px`
- `left: 25px`
- `left: 12px`
- `left: 10px`

These are not small details.  
These are the elements that decide whether the Arabic version feels natural or visually broken.

### b) Negative direction-based spacing
Examples:
- `margin-left: -30px`
- `margin-left: -12px`
- `margin-right: -12px`
- `margin-left: -15px`

These are usually used to create:
- visual overlap
- an element extending outside the container
- non-standard centering
- decorative effects

### c) Side borders
Rules such as:
- `border-left`
- `border-right`
- side-specific border colors
- asymmetric border radii

These can cause side accents, panels, and cards to look inverted or detached.

### d) Fixed side padding
Rules such as:
- `padding-left`
- `padding-right`
- `padding-left: 40px`
- `padding-right: 40px`

These often determine:
- content breathing room
- icon and label spacing
- readability inside cards and forms

### e) Decorative elements tied to one page edge
Examples:
- corner ornaments
- strips
- badges
- floating blocks
- section dividers

These elements often assume a single page edge and will look wrong when the direction changes.

## 3.2 Correct CSS strategy

### Level 1: Move physical properties to logical properties
Use logical CSS wherever possible:
- `margin-inline-start`
- `margin-inline-end`
- `padding-inline-start`
- `padding-inline-end`
- `inset-inline-start`
- `inset-inline-end`
- `border-start-start-radius`
- `border-start-end-radius`
- `border-end-start-radius`
- `border-end-end-radius`

### Level 2: Add RTL overrides
For components that cannot be fully converted with logical properties:
- create RTL-specific overrides
- target only the affected component
- keep the original English behavior intact

### Level 3: Redefine critical classes
For the most sensitive blocks:
- hero
- social strip
- project cards
- card buttons
- form elements
- footer areas
- overlays
- absolute captions

redefine the class rules explicitly for RTL.

## 3.3 Map of critical elements that must be handled manually

### 1) Hero section
Possible issues:
- title and subtitle alignment
- image placement
- decorative elements
- call-to-action spacing
- text block width
- visual balance around the hero image

### 2) Titles and captions
Possible issues:
- title width expansion
- subtitle wrapping
- alignment with icons or accents
- spacing between heading and paragraph
- caption blocks with side bars

### 3) Service cards
Possible issues:
- icon placement
- card padding
- side labels
- hover accent direction
- CTA alignment
- content overflow

### 4) Project cards
This pattern usually depends on:
- overlay
- badge
- description box
- CTA group

This type distorts quickly in RTL because overlays and absolute blocks are often built on an offset from one side only.

### 5) Testimonial and quote blocks
These are sensitive because of:
- avatar placement
- quote icon
- testimonial text
- author details
- slider controls

### 6) FAQ / Accordion
Arrows and internal layout usually need:
- icon side swap
- heading spacing repair
- collapse header alignment
- consistent open/close state layout

### 7) Contact forms
Possible issues:
- label placement
- input padding
- icon alignment
- placeholder direction
- submit button width
- validation text wrapping

### 8) Footer
Possible issues:
- multi-column order
- social icon positions
- contact line alignment
- copyright row behavior
- spacing between widgets

---

## Phase 4: Handle JavaScript and behavioral dependencies

## 4.1 Slick Slider

### Possible issues
- slider direction does not match RTL
- arrow order is semantically reversed
- autoplay and swipe feel unnatural
- dots and navigation are aligned for LTR
- cloned slides may behave unexpectedly

### Required action
- enable RTL mode where supported
- mirror controls and arrow semantics
- test slide order and touch behavior on all breakpoints

## 4.2 Fancybox

### Possible issues
- control buttons remain on the wrong side
- navigation arrows convey the wrong direction
- close button placement may conflict with RTL layout
- captions may align incorrectly

### Required action
- relocate controls
- swap arrow placement or semantics when needed
- verify modal, image, and gallery interactions in Arabic

## 4.3 AOS

### Risks
- entrance motion may still come from the wrong side
- reveal animations may conflict with RTL reading flow
- decorative motion may feel directionally inverted

### Required action
- separate semantic direction from visual direction
- remap left/right entrance patterns for RTL
- verify section-by-section animation behavior

## 4.4 Counters

### Required action
- verify numeric formatting
- ensure locale output matches the Arabic page
- keep number reading clear and stable
- test percentages, decimals, and large values

## 4.5 Form submission scripts

### Required action
- translate all success and error strings
- localize validation output
- keep client-side and server-side messages consistent
- ensure Arabic feedback is complete

## 4.6 Bootstrap components

Any Bootstrap component using:
- dropdown
- offcanvas
- collapse
- modal
- toast

must be tested in RTL because Bootstrap itself does not guarantee that the custom layout built on top of it will stay correct.

---

## Phase 5: Handle Arabic text typographically

Arabic is not only translation.  
Arabic changes the visual rhythm of the site.

## 5.1 Arabic font
Choose a clear, strong Arabic font that supports:
- multiple weights
- readability on small screens
- long paragraphs
- premium visual tone

### Rule
The font should preserve the dignity and geometry of the original design, not just display Arabic letters.

## 5.2 Handle longer text
Arabic text frequently needs:
- more vertical breathing room
- wider line height
- more flexible cards
- less rigid fixed widths
- adaptive headings

### Required action
- test long headings
- test multi-line buttons
- test paragraph wrapping
- test form helper text and validation
- test mixed Arabic/English content

## 5.3 Text alignment
- default alignment should follow RTL logic
- headings with mixed content may need `unicode-bidi`
- technical strings may need isolated LTR spans

---

## Phase 6: Design RTL layers for each component

## 6.1 Navbar
### What can break?
- logo and menu relation
- toggle button placement
- dropdown side
- spacing between items
- icon direction
- mobile collapse behavior

### What should be done?
- rebuild spacing from the RTL side
- test desktop and mobile separately
- ensure dropdowns open on the correct visual edge
- keep the logo composition stable

## 6.2 Hero block
### Risks
- title alignment drift
- image offset imbalance
- CTA misplacement
- decorative layers appearing on the wrong side

### Required action
- rebuild the hero spacing system
- preserve the original balance
- test text, media, and overlay interactions

## 6.3 Cards
### Risks
- icon drift
- text block collision
- overlay mismatch
- side highlight inversion

### Required action
- define card internal flow again
- ensure consistent padding and height
- keep hover states readable in RTL

## 6.4 Breadcrumb
### Risks
- separator direction
- path reading order
- icon or chevron inversion

### Required action
- reverse separator meaning if needed
- preserve hierarchy and readability

## 6.5 Footer
### Risks
- content order mismatch
- contact row inversion
- social icon alignment
- newsletter form spacing

### Required action
- rebuild footer columns for RTL
- verify multi-line content
- keep copyright row clean and consistent

---

## Phase 7: Precise file-by-file conversion methodology

### Home page
- hero
- services preview
- projects preview
- counters
- testimonials
- FAQ teaser
- contact teaser

Each section must be tested individually, not only as a full page.

### Services page
- service grid
- service details cards
- icon placements
- CTA alignment

### Service details page
- detail body layout
- sidebar behavior
- quotes and supporting visuals

### Projects page
- cards
- filters if present
- image captions
- overlay behavior

### Project details page
- hero details
- gallery
- navigation elements
- project metadata blocks

### Blog page
- article cards
- excerpt alignment
- meta row
- pagination

### Single post page
- article body
- heading hierarchy
- inline images
- quotes
- author block
- comment area

### Contact page
- map area
- form fields
- contact cards
- social/contact metadata

### FAQ page
- accordion behavior
- arrow direction
- header spacing

### Pricing page
- price cards
- feature lists
- CTA buttons
- badge alignment

### Testimonials page
- quote blocks
- avatar alignment
- slider controls

### 404 page
- center block
- CTA
- graphic balance
- fallback layout

---

## Phase 8: CSS modification rules for critical components

## 8.1 Use local overrides
Do not rewrite the entire stylesheet unless necessary.  
Patch the exact target component.

## 8.2 Do not destroy the original
Preserve the English version exactly.  
RTL should be an additive layer, not a destructive rewrite.

## 8.3 Work in three layers
- base original CSS
- RTL override sheet
- component-level exceptions

## 8.4 Always monitor the following elements
- absolute elements
- side-based paddings
- asymmetrical border radii
- decorative pseudo-elements
- overlay captions
- CTA icons
- form controls
- slider controls

---

## Phase 9: Rules for images and visuals

### 9.1 Images are not automatically flipped
Some images:
- are neutral
- are backgrounds
- show people
- contain architectural compositions

Flipping them blindly can ruin the composition.

### 9.2 Images requiring review
- images containing text
- images with a clear direction of movement
- images where people look to one side
- images with visual guidance elements

### 9.3 Overlays and grids
Images inside overlays or cards need:
- aspect ratio inspection
- cropping inspection
- `object-fit` review
- focal point positioning review

---

## Phase 10: Unify scripting language and text outputs

### Static text that must be translated
- success messages
- error messages
- validation notices
- loading states
- empty states
- confirmation states

### Text that is often forgotten
- button labels
- helper text
- alt-like captions generated in code
- fallback messages
- console-facing output that leaks into the UI
- PHP response messages

---

## Phase 11: Deep testing strategy

## 11.1 Direction test
For every page, verify:
- root direction
- text direction
- component direction
- icon direction
- slider direction
- overlay direction

## 11.2 Page test
Check each page separately:
- home
- services
- projects
- blog
- contact
- FAQ
- pricing
- testimonials
- 404

## 11.3 State test
Test:
- hover
- focus
- active
- open
- collapsed
- modal
- slider movement
- form validation

## 11.4 Long-text test
Stress the layout with:
- long titles
- long paragraphs
- long button labels
- long validation text
- mixed Arabic/English content

## 11.5 Touch test
Verify:
- mobile tapping
- slider swipe
- menu open/close
- accordion expand/collapse
- form interaction

---

## Phase 12: Final acceptance criteria

The Arabic version is accepted only when:
- the design identity remains intact
- the hierarchy is preserved
- the geometry is stable
- no layout section collapses
- no visual distortion appears
- the RTL flow is natural
- the typography reads cleanly
- the scripts and forms behave correctly
- the visuals remain premium and consistent

---

## 13) Recommended practical order of execution

### Step 1
Prepare a separate Arabic version.

### Step 2
Add `lang="ar"` and `dir="rtl"`.

### Step 3
Replace Bootstrap LTR with Bootstrap RTL.

### Step 4
Build `rtl.css`.

### Step 5
Convert every `left/right/padding/margin/border` property to logical alternatives or RTL overrides.

### Step 6
Inspect and fix all absolute-positioned elements.

### Step 7
Fix sliders, Fancybox, AOS, and icon directionality.

### Step 8
Translate form messages and system text.

### Step 9
Validate images, overlays, cards, and sections on all breakpoints.

### Step 10
Perform a final visual and behavioral audit against the English reference.

---

## 14) Rules to prevent common failure modes

### Do not
- translate text only and ignore geometry
- rely on `dir="rtl"` alone
- mix Bootstrap RTL and LTR blindly
- reverse all images blindly
- ignore slider directionality
- leave English messages in forms
- assume cards will auto-adapt to Arabic length

### Do
- isolate components
- inspect absolute positioning
- use logical CSS properties
- localize JavaScript output
- test every page and breakpoint
- preserve the original visual language

---

## 15) Required outcome of this strategy

The result should be:
- a professional Arabic RTL version
- visually stable and technically sound
- structurally clean
- consistent with the English design
- readable at every breakpoint
- maintainable after launch
- resistant to visual breakage

---

## 16) Executive conclusion

This template requires a **direction-aware engineering conversion**, not a simple translation pass.  
The Arabic version must be rebuilt with RTL logic at the structure, style, and behavior layers while preserving the exact premium feel of the English version.