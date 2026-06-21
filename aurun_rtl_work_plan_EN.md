# Advanced Professional Work Plan for Converting the Website to Arabic and RTL

## 1) Execution Objective
Convert the entire website into a stable Arabic RTL version at the visual, technical, and structural levels, while preserving the original visual identity, the same layout logic, the same spacing quality, and the same visual feel, and preventing any grid collapse, element breakage, alignment distortion, or behavioral instability.

## 2) Working Principle
The conversion is not only a “text translation” task. It is a multi-layer reconfiguration process that includes:
- HTML structure
- document and block direction
- Bootstrap and its RTL version, if present
- custom CSS and inheritance
- JavaScript related to direction and motion
- Arabic fonts
- any external libraries that assume LTR
- visual and behavioral testing after each layer

## 3) Golden Rule
Any element that depends on:
- left / right
- margin-left / margin-right
- padding-left / padding-right
- float
- text-align
- transform positioning
- absolute positioning
- carousel direction
- icon arrows
- offcanvas / dropdown alignment
- AOS entrance direction
- SVG positioning
- pseudo-element directional layout

must be reviewed separately, because this is the class of issues most likely to break RTL.

## 4) Phase One: Full Structural Decomposition

### 4.1 File inventory
- List all HTML files.
- List all CSS files.
- List all JavaScript files.
- List all external libraries.
- List all images, icons, fonts, and SVG files.
- List any translation files or hard-coded text embedded in code.

### 4.2 Classify files by impact
- core files that control the global layout
- UI component files
- motion and animation files
- slider and gallery files
- form and interaction files
- header, footer, and navigation files
- print or backup files

### 4.3 Build a dependency map
For every file:
- what does it import?
- what does it affect?
- what does it depend on?
- does it only work in LTR?
- does it contain explicit directional rules?
- does it change when `dir` changes?

## 5) Phase Two: Deep Visual Structure Analysis

### 5.1 Layout grid analysis
- inspect columns
- inspect offsets
- inspect gutters
- inspect containers
- inspect rows
- inspect absolute positions
- inspect z-index stacking
- inspect overflow clipping
- inspect section heights

### 5.2 Sensitive area analysis
- header
- main navigation
- offcanvas
- hero sections
- cards
- content services
- buttons
- forms
- footer
- sliders
- galleries
- FAQ
- testimonials
- partner sections
- any section that contains images alongside text

### 5.3 Interaction element analysis
- hover states
- focus states
- active states
- open/close states
- accordion states
- modal states
- dropdown states
- tab states
- Slick/Fancybox lightbox behavior

## 6) Phase Three: Set Up the Core RTL Layer

### 6.1 Set the document
- set `lang="ar"`
- set `dir="rtl"` on `html` or on `body`, depending on the template architecture
- ensure sections that need partial LTR remain isolated

### 6.2 Text layers
- default text alignment
- `unicode-bidi` where needed
- handling Arabic and English text mixed with numbers
- protecting mixed headings from unintended reversal

### 6.3 Global tuning
- review all spacing utilities
- review all alignment utilities
- review `flex-direction`
- review `justify-content`
- review `align-items`
- review `order`

## 7) Phase Four: Bootstrap RTL

### 7.1 Choose the correct version
- ensure that Bootstrap RTL or an equivalent build is being used
- ensure that LTR Bootstrap is not mixed with incompatible RTL CSS

### 7.2 Review Bootstrap utilities
- `ms-*` / `me-*`
- `ps-*` / `pe-*`
- `start` / `end`
- navbar alignment
- dropdown placement
- offcanvas placement
- modal position assumptions
- input groups
- form controls
- icon alignment if Bootstrap utilities are used

### 7.3 Risk zones inside Bootstrap
- rows that depend on `offset`
- columns aligned to the left
- flex utilities written under LTR assumptions
- navigation elements that expect a leftward direction
- close buttons
- breadcrumbs
- dropdown menus
- any component that relies on `left` / `right` in generated or custom CSS

## 8) Phase Five: Convert the Custom CSS

### 8.1 Physical-to-logical conversion
Replace:
- `margin-left` → `margin-inline-start`
- `margin-right` → `margin-inline-end`
- `padding-left` → `padding-inline-start`
- `padding-right` → `padding-inline-end`
- `left` → `inset-inline-start`
- `right` → `inset-inline-end`
- `text-align: left` → `text-align: start`
- `text-align: right` → `text-align: end`

### 8.2 Review every impactful property
- border-radius asymmetry
- background-position
- background-size
- transform translateX
- absolute offsets
- pseudo-elements positioned by side
- decorative lines and arrows
- element connectors
- timeline layouts
- feature boxes with side accents

### 8.3 Handle exceptions
- elements that must remain LTR
- code blocks, numbers, email addresses, links, or technical data
- charts or badges
- currency and date elements
- mixed Arabic/English text

## 9) Phase Six: Review JavaScript Related to Direction

### 9.1 Layout-dependent scripts
- width and height calculations
- scripts that move elements on the X axis
- scripts that set element positions
- scripts that move arrows or indicators between sides

### 9.2 Most sensitive libraries
- AOS
- Slick
- Fancybox
- counters
- sticky elements
- scroll-based animations
- smooth scroll handlers

### 9.3 What must be reviewed
- slider movement direction
- arrow placement
- pagination marker order
- whether animations should begin from the right instead of the left
- whether elements enter from the correct side
- whether visual reading flow remains stable during scrolling

## 10) Phase Seven: Arabic Fonts and Typography

### 10.1 Select the font
- clear Arabic font
- appropriate weights
- balance between readability and elegance
- compatibility with both small and large sizes

### 10.2 Typographic tuning
- line-height
- letter-spacing
- word-spacing
- font-smoothing
- fallback stacks
- balance between Arabic text and English headings

### 10.3 Measure the effect
- line length
- text density
- heading crowding
- long-word wrapping
- readability on small screens

## 11) Phase Eight: Handle Images and Graphics

### 11.1 Images with frames or direction
- images containing English text
- images with arrows or movement cues
- images that depend on the position of elements inside the image
- SVG files that contain left/right or directional points

### 11.2 Overlay inspection
- captions
- badges
- overlays
- floating labels
- pinned decorations
- corner ribbons

### 11.3 Prevent distortion
- control `object-fit`
- control `object-position`
- control containers
- preserve ratios
- review mobile cropping

## 12) Phase Nine: Reshape Sensitive Components

### 12.1 Header and navigation
- reverse link order if necessary
- tune the logo position
- tune the menu button
- tune icons
- tune dropdown alignment
- tune spacing between items

### 12.2 Offcanvas
- determine the correct opening side
- tune enter and exit motion
- review overlay and close button
- review scroll lock

### 12.3 Buttons and CTAs
- icon placement
- text-and-icon order
- internal padding
- hover and active states

### 12.4 Cards and promotional blocks
- image-text direction
- reading space
- visual balance
- placement of badges and decorative elements

## 13) Phase Ten: Verify No Visual Breakage

### 13.1 Golden check
For every page:
- does the structure remain readable?
- does the visual sequence remain natural?
- do the spacing rules remain balanced?
- do the cards still align?
- do decorative elements still remain in place?
- do headings remain uncut?
- do images remain inside their frames?
- do buttons remain correctly positioned?

### 13.2 Breakpoint check
- desktop large
- standard desktop
- tablet landscape
- tablet portrait
- large mobile
- small mobile

### 13.3 State check
- home page
- internal page
- page with a form
- page with a gallery
- page with a slider
- FAQ page
- page with long textual content

## 14) Phase Eleven: Mixed Arabic Text Handling
### 14.1 Bidirectional strings
- headings with English inside
- numbers inside Arabic phrases
- brand names
- email addresses
- links
- codes

### 14.2 Structural protection
- use `dir="ltr"` where needed inside technical passages
- use `<bdi>` or `<span dir="ltr">` for local protection
- prevent numeric order from reversing incorrectly
- prevent punctuation from visually colliding

## 15) Phase Twelve: Technical Stability

### 15.1 Loading review
- no duplicate files
- no conflicting library versions
- no uncoordinated RTL and LTR assets loaded together
- no conflicting CSS

### 15.2 Silent error review
- console errors
- warnings
- broken selectors
- missing assets
- 404 resources
- DOM/script mismatches

### 15.3 Performance review
- reduce reflow
- prevent overdraw
- compress images
- keep loading light
- avoid extra complexity introduced by conversion

## 16) Phase Thirteen: Strict QA Plan

### 16.1 Visual test
- compare before and after
- compare pixel alignment
- compare spacing
- compare visual hierarchy
- compare positioning

### 16.2 Behavioral test
- do the buttons work?
- do menus work?
- do sliders work?
- do forms work?
- do modals work?
- do links work?

### 16.3 Language test
- translation accuracy
- terminology consistency
- tone consistency
- uniform vocabulary
- no confusing Arabic-English mixing

## 17) Phase Fourteen: Risk Management

### 17.1 Highest risks
- CSS based on left/right
- default LTR scripts
- decorative elements placed on one side only
- asymmetric images and SVGs
- sliders that reverse direction incorrectly
- fixed sizes that cannot tolerate Arabic text length
- heading overflow
- card collapse
- Bootstrap and custom CSS conflicts

### 17.2 Mitigation policy
- isolate first
- convert logically second
- test third
- lock fourth
- re-check fifth

## 18) Phase Fifteen: Final Output Policy

- Arabic version complete
- RTL stable
- files organized
- CSS clean
- JS conflict-free
- libraries compatible
- Arabic fonts appropriate
- full testing documented
- future maintenance notes included

## 19) Success Criterion
Success does not mean that the page merely “renders in Arabic.” It means that:
- the layout did not break
- the direction feels natural
- the reading flow is correct
- the structure remained original
- the motion feels logical
- the typography is comfortable
- the images remain framed correctly
- the buttons remain in the right place
- no element flips or shifts in a visually disturbing way

## 20) Target Result
A stable Arabic RTL version that:
- is polished
- is maintainable
- remains compatible with libraries
- keeps the design identity intact
- preserves layout quality
- supports future expansion
- avoids visual breakage before it happens
