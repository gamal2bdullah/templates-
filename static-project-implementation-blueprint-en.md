# Static Project Implementation Blueprint
## Advanced Solar Load Calculator → Pure HTML/CSS/JavaScript Architecture

### Document Purpose
This document converts the original application study into a **ready-to-build static project blueprint**. It defines the target folder structure, file responsibilities, implementation standards, data flow, UI/UX system, calculation engine strategy, and delivery criteria for a **world-class static application** built with **HTML, CSS, and JavaScript only**.

---

## 1. Target Outcome

The final product must be a **fully static, modular, professional-grade web application** that preserves the original calculator’s capabilities while removing all runtime framework dependencies such as React, TypeScript compilation, and component bundling.

The static version must provide:

- Accurate electrical load calculations
- Appliance inventory management
- Load schedules and profile building
- PF, harmonics, surge, and phase analysis
- Validation and warning engine
- Exportable PDF reports
- Local persistence via `localStorage`
- Clean Arabic-friendly RTL support
- Responsive UI/UX for desktop and mobile
- Maintainable modular codebase with clear separation of concerns

---

## 2. Non-Negotiable Constraints

The static build must comply with all of the following:

- Use only `HTML`, `CSS`, and `JavaScript`
- No React, no TypeScript, no build-time UI framework dependency in the final deliverable
- No component framework required at runtime
- Preserve the original engineering logic and outputs
- Keep calculations deterministic and testable
- Support offline usage after first load
- Organize files in a production-ready structure
- Include `imgs/`, `icons/`, and `libs/` directories
- Use a modular architecture that remains scalable
- Support RTL first, with optional LTR compatibility if needed
- Keep print and PDF output professional and legible

---

## 3. Recommended Static Folder Structure

```text
project/
├── index.html
├── manifest.json
├── README.md
├── assets/
│   ├── css/
│   │   ├── app.css
│   │   ├── components.css
│   │   ├── layout.css
│   │   ├── forms.css
│   │   ├── tables.css
│   │   ├── charts.css
│   │   ├── print.css
│   │   └── rtl.css
│   ├── js/
│   │   ├── app.js
│   │   ├── router.js
│   │   ├── store.js
│   │   ├── events.js
│   │   ├── storage.js
│   │   ├── ui.js
│   │   ├── dom.js
│   │   ├── constants.js
│   │   ├── formatters.js
│   │   ├── validators.js
│   │   ├── calculations/
│   │   │   ├── core.js
│   │   │   ├── assumptions.js
│   │   │   ├── validation.js
│   │   │   ├── pf.js
│   │   │   ├── harmonics.js
│   │   │   ├── surge.js
│   │   │   ├── phase.js
│   │   │   ├── profiles.js
│   │   │   └── reports.js
│   │   ├── data/
│   │   │   ├── appliances.js
│   │   │   ├── presets.js
│   │   │   └── examples.js
│   │   ├── views/
│   │   │   ├── dashboard.js
│   │   │   ├── inventory.js
│   │   │   ├── schedule.js
│   │   │   ├── analysis.js
│   │   │   ├── reports.js
│   │   │   ├── settings.js
│   │   │   ├── library.js
│   │   │   ├── assumptions.js
│   │   │   ├── validation.js
│   │   │   ├── documentation.js
│   │   │   └── tests.js
│   │   ├── components/
│   │   │   ├── header.js
│   │   │   ├── sidebar.js
│   │   │   ├── modal.js
│   │   │   ├── toast.js
│   │   │   ├── tabs.js
│   │   │   ├── cards.js
│   │   │   ├── tables.js
│   │   │   ├── inputs.js
│   │   │   ├── charts.js
│   │   │   └── empty-state.js
│   │   ├── reports/
│   │   │   ├── pdf.js
│   │   │   ├── audit.js
│   │   │   └── templates.js
│   │   └── tests/
│   │       ├── cases.js
│   │       └── runner.js
│   ├── imgs/
│   │   ├── logo-horizontal.svg
│   │   ├── logo-icon.svg
│   │   ├── logo-mark.svg
│   │   ├── hero.svg
│   │   ├── empty-state.svg
│   │   └── report-cover.svg
│   ├── icons/
│   │   ├── dashboard.svg
│   │   ├── inventory.svg
│   │   ├── analysis.svg
│   │   ├── reports.svg
│   │   ├── settings.svg
│   │   └── more.svg
│   └── libs/
│       ├── jspdf.umd.min.js
│       ├── jspdf-autotable.min.js
│       └── charting-library.min.js
└── data/
    └── seed.json
```

---

## 4. File-by-File Responsibility Map

### Root Layer
- `index.html`  
  Main application shell, layout container, font links, metadata, and script/style entry points.

- `manifest.json`  
  Optional PWA metadata for installable static deployment.

- `README.md`  
  Developer documentation, setup notes, and usage instructions.

### CSS Layer
- `app.css`  
  Global tokens, typography, base layout, and design system variables.

- `components.css`  
  Shared styles for buttons, cards, tabs, panels, modals, toasts, and badges.

- `layout.css`  
  Grid system, sidebar layout, content areas, responsive breakpoints.

- `forms.css`  
  Inputs, selects, toggles, validation states, helper text, and form spacing.

- `tables.css`  
  Inventory table, analysis table, sticky headers, zebra states, empty states.

- `charts.css`  
  Chart wrappers, legends, axes, responsive containers, print-friendly chart styles.

- `print.css`  
  PDF and printer-friendly layout, page breaks, monochrome fallback, readable report output.

- `rtl.css`  
  Direction-specific overrides for Arabic-first interface behavior.

### JavaScript Core
- `app.js`  
  Entry point, initialization pipeline, boot sequence, and app composition.

- `router.js`  
  Hash-based or state-based navigation between views.

- `store.js`  
  Central application state, derived data, state mutation API, and event publication.

- `events.js`  
  Lightweight pub/sub mechanism for decoupled view updates.

- `storage.js`  
  Persistence to `localStorage`, serialization, migration, and backup restore.

- `ui.js`  
  DOM rendering orchestration, view mounting, skeletons, and interaction wiring.

- `dom.js`  
  DOM helpers, query utilities, element creation helpers, and safe update functions.

- `constants.js`  
  App-wide constants, enums, labels, thresholds, and engineering defaults.

- `formatters.js`  
  Number formatting, electrical unit formatting, localized display helpers.

- `validators.js`  
  Field-level and model-level validation rules for user input integrity.

### Calculation Engines
- `core.js`  
  Main load calculation engine and aggregate metrics.

- `assumptions.js`  
  Default engineering assumptions and override handling.

- `validation.js`  
  Rule checking, severity grading, and corrective recommendations.

- `pf.js`  
  Power factor analysis and correction modeling.

- `harmonics.js`  
  Harmonic distortion analysis and mitigation logic.

- `surge.js`  
  Inrush/surge stacking and transient load behavior.

- `phase.js`  
  Three-phase distribution, balance, and imbalance detection.

- `profiles.js`  
  Daily, weekly, seasonal, and holiday-aware load profile generation.

- `reports.js`  
  Report-ready aggregate data shaping and summary extraction.

### Data Layer
- `appliances.js`  
  Canonical appliance library, category mappings, default ratings, and templates.

- `presets.js`  
  Ready-made project presets for common scenarios.

- `examples.js`  
  Demo scenarios and onboarding examples.

### Views Layer
Each view is a pure rendering module with event binding:
- `dashboard.js`
- `inventory.js`
- `schedule.js`
- `analysis.js`
- `reports.js`
- `settings.js`
- `library.js`
- `assumptions.js`
- `validation.js`
- `documentation.js`
- `tests.js`

### Components Layer
Reusable UI fragments:
- `header.js`
- `sidebar.js`
- `modal.js`
- `toast.js`
- `tabs.js`
- `cards.js`
- `tables.js`
- `inputs.js`
- `charts.js`
- `empty-state.js`

### Reports Layer
- `pdf.js`  
  PDF generation pipeline using local JS libraries.

- `audit.js`  
  Structured audit report objects for traceability and compliance.

- `templates.js`  
  Layout templates and content blocks for reports.

### Tests Layer
- `cases.js`  
  Golden test scenarios and expected values.

- `runner.js`  
  In-browser test runner with pass/fail summary.

---

## 5. Application Architecture Rules

### 5.1 Separation of Concerns
The project must be organized into these independent layers:

1. **State layer**  
   Owns data and mutations.

2. **Calculation layer**  
   Pure functions only. No DOM access. No storage access.

3. **Rendering layer**  
   Converts state into HTML/UI.

4. **Interaction layer**  
   Binds user actions to state updates and rerenders.

5. **Persistence layer**  
   Manages save/load/restore.

6. **Reporting layer**  
   Converts state and results into printable/exportable artifacts.

### 5.2 Pure Function Standard
All electrical calculation functions should be:
- deterministic
- side-effect free
- easy to test
- reusable across views and reports

### 5.3 Single Source of Truth
- The application state must exist only in `store.js`
- Calculations must read from state snapshots
- Views must never mutate data directly
- Storage must only persist state snapshots

---

## 6. Static Build Strategy

The project should be built as a static app in one of two ways:

### Option A: Direct Static Implementation
The application is written directly in plain JavaScript and deployed as-is.

Use this when:
- The final target is pure static hosting
- No build tooling is desired
- Long-term maintenance must remain simple

### Option B: Transitional Conversion
The existing React codebase is used only as a reference, and the final output is rewritten into static modules.

Use this when:
- The original logic is already mature
- You want to preserve calculations and UI behavior
- You need a clean final architecture without framework runtime dependencies

For this project, **Option B is the preferred route** because it preserves engineering precision while producing a true static deliverable.

---

## 7. Rendering Model

### 7.1 App Shell
The `index.html` file should contain:
- `header`
- `aside`
- `main`
- `footer`
- modal root
- toast root
- report root

### 7.2 View Switching
Use one of these strategies:
- hash routing
- state-driven view switching
- section-based rendering

Recommended:
- hash routing for simplicity and debuggability

### 7.3 Component Rendering
Each component should expose functions such as:
- `renderHeader()`
- `renderSidebar()`
- `renderDashboard()`
- `renderInventory()`
- `renderReports()`

### 7.4 Event Binding
Use delegated events rather than attaching listeners to every element individually.

Benefits:
- less memory overhead
- fewer bugs
- easier rerendering
- cleaner lifecycle management

---

## 8. UI/UX Design System

### 8.1 Visual Principles
The interface should be:
- professional
- minimal but advanced
- data-dense without visual noise
- Arabic-first and RTL-native
- highly legible
- responsive
- print-friendly
- audit-friendly

### 8.2 UI Structure
Recommended layout:
- Top header with project identity and key status indicators
- Collapsible sidebar with icons and labels
- Main content area with cards, tables, charts, and panels
- Right-side drawers for advanced editing where appropriate
- Modal dialogs for confirm/inspect actions
- Toasts for feedback
- Empty states for zero-data scenarios

### 8.3 Design Tokens
Standardize these tokens in CSS:
- color palette
- spacing scale
- border radius scale
- elevation/shadow scale
- typography scale
- animation timing
- z-index layers

### 8.4 Accessibility Requirements
- Proper contrast ratios
- Keyboard navigable controls
- Clear focus states
- Meaningful labels
- Screen-reader friendly semantics
- Avoid color-only meaning for warnings/errors

---

## 9. Engineering Logic Preservation Plan

The following engine responsibilities must be preserved exactly during conversion:

### 9.1 Load Calculations
- Connected load
- Running load
- Simultaneous load
- Energy per day
- Energy per month
- Energy per year
- Apparent power
- Reactive power
- Current estimates
- Surge estimates

### 9.2 Performance Analysis
- Diversity factor
- Demand factor
- Coincidence factor
- PF correction
- Phase balancing
- Harmonics review
- Voltage and load warnings
- Capacity recommendations

### 9.3 Validation
- Missing fields
- Invalid quantities
- Impossible power values
- Unrealistic duty cycles
- Phase imbalance
- High inrush conditions
- Overloaded circuit warnings

---

## 10. Data Model Requirements

### 10.1 Appliance Object
Each appliance entry should contain:
- id
- name
- category
- ratedPowerW
- quantity
- usageHoursPerDay
- dutyCycle
- powerFactor
- startingMultiplier
- phase
- notes
- enabled
- source

### 10.2 Project State
The central state should include:
- project metadata
- appliance list
- selected templates
- assumptions
- validation results
- calculated summaries
- report settings
- UI preferences
- persistence metadata

### 10.3 Derived Metrics
Derived values should never be stored manually if they can be computed from state. Examples:
- total load
- daily energy
- monthly energy
- annual energy
- peak current
- phase totals
- warning counts

---

## 11. PDF and Reporting Strategy

The reporting system should support:

- executive summary
- detailed load table
- assumptions disclosure
- validation warnings
- phase analysis
- PF analysis
- harmonics commentary
- surge commentary
- recommendations section
- versioning metadata
- page numbering and cover sheet

### Report Quality Rules
- Report must be printable in A4 and Letter
- Tables must remain readable
- Headings must be consistent
- Numbers must be formatted cleanly
- Warnings must be visually separated
- Page breaks must be predictable

---

## 12. Asset Strategy

### 12.1 `imgs/`
Store:
- logo variants
- hero illustrations
- empty-state graphics
- report cover art

### 12.2 `icons/`
Store:
- navigation icons
- action icons
- status icons
- feature icons

### 12.3 `libs/`
Store local copies of:
- PDF library
- table plugin
- chart library
- any lightweight helper library required at runtime

### Asset Rules
- Prefer SVG for logos and icons
- Keep images optimized
- Use consistent naming conventions
- Never mix design assets with business logic

---

## 13. Implementation Phases

### Phase 1: Core Extraction
Extract and rewrite:
- data models
- assumptions
- calculation functions
- validation logic

### Phase 2: Static App Shell
Build:
- `index.html`
- base layout
- navigation
- core design system

### Phase 3: Data and State
Implement:
- store
- persistence
- sample datasets
- mutation flows

### Phase 4: Views
Rebuild:
- dashboard
- inventory
- schedule
- analysis
- reports
- settings

### Phase 5: Reporting
Integrate:
- PDF generation
- audit report formatting
- print layout

### Phase 6: QA and Hardening
Add:
- test runner
- validation checks
- regression cases
- performance review

### Phase 7: Polish
Finalize:
- icons
- illustrations
- spacing
- transitions
- accessibility
- responsive tuning

---

## 14. Code Quality Rules

Every file must follow these standards:

- One responsibility per file
- No duplicate logic
- No hidden side effects
- No magic numbers without explanation
- Clear naming conventions
- Inline comments only where needed
- Functions should stay short and composable
- Views must not contain business rules
- Calculations must not access the DOM
- Storage logic must not render UI

---

## 15. Naming Conventions

### Files
- Use lowercase kebab-case or simple lowercase names
- Keep naming consistent across CSS, JS, and assets

### Functions
- Use descriptive verbs:
  - `calculateTotalLoad`
  - `buildPhaseSummary`
  - `validateAppliance`
  - `renderInventory`
  - `saveState`

### Constants
- Use uppercase snake case:
  - `DEFAULT_POWER_FACTOR`
  - `MAX_PHASE_IMBALANCE`
  - `STORAGE_KEY`

### IDs
- Use stable, predictable identifiers
- Never couple DOM IDs to translated text

---

## 16. Acceptance Criteria

The static build is complete only if all of the following are true:

- The application opens directly from `index.html`
- No framework runtime is required
- The main calculator workflow works
- State persists across reloads
- Validation messages appear correctly
- Report generation works
- Layout is responsive
- RTL display is correct
- Assets are organized
- Engine outputs match the original logic
- The codebase is easy to extend

---

## 17. Recommended Delivery Package

The final deliverable should include:

- `index.html`
- `assets/css/*`
- `assets/js/*`
- `assets/imgs/*`
- `assets/icons/*`
- `assets/libs/*`
- `data/seed.json`
- `README.md`
- optional `manifest.json`

---

## 18. Final Engineering Summary

This conversion should not be treated as a visual rewrite only. It is a **complete architectural migration** from a framework-based application into a **deterministic static product**.

The success of the conversion depends on three things:

1. **Preserving the calculation engine**
2. **Rebuilding the UI as modular static views**
3. **Maintaining a disciplined file structure**

If these three pillars are respected, the final static application will be stable, maintainable, professional, and ready for production deployment.

---

## 19. Immediate Next Step

The next practical step is to generate the actual starter project files for the structure above, beginning with:

- `index.html`
- `assets/css/app.css`
- `assets/js/app.js`
- `assets/js/store.js`
- `assets/js/router.js`
- `assets/js/calculations/core.js`
- `assets/js/views/dashboard.js`

This gives you a runnable static foundation that can be expanded module by module.
