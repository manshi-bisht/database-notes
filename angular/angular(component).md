# Angular Day 2 — Components
**Full-Stack Internship · Module 5 · Frontend Frameworks**
**Instructor:** Dinesh Rawat Sir

---

## 1. What is a Component? (Simple Idea)

A **component** is a reusable, self-contained piece of the user interface (UI). It bundles three things together in one place:

- Its own **HTML** (template)
- Its own **CSS** (styles)
- Its own **TypeScript** (logic)

A website is just many components joined together, like:

```
Header component
Navigation component
Login form component
Product card component
Footer component
```

Instead of writing the same code again and again, you build a component **once** and reuse it everywhere.

### The Repetition Problem (Why Components Exist)

**Without components** — you copy-paste the same block for every product:

```html
<div class="card">
  <h2>iPhone 16</h2>
  <button>Buy</button>
</div>

<div class="card">
  <h2>Samsung S25</h2>
  <button>Buy</button>
</div>
```

Now imagine 100 products — that's 100 copies to write and fix.

**With components** — you build one `ProductCard` component and reuse it, just passing different data:

```html
<product-card name="iPhone 16"></product-card>
<product-card name="Samsung S25"></product-card>
```

Same component, different data. One piece of code, reused everywhere.

---

## 2. Why Use Components? (15 Advantages)

| # | Advantage | Meaning |
|---|-----------|---------|
| 1 | Code reusability | Write once, use many times |
| 2 | Easy maintenance | Fix a bug in one place, not many |
| 3 | Better organisation | Code split into smaller parts |
| 4 | Improved readability | Smaller files, easier to understand |
| 5 | Faster development | Reuse instead of starting from scratch |
| 6 | Consistency | Same button/card/form looks same everywhere |
| 7 | Independent development | Different devs can work on different components together |
| 8 | Easy testing | Components tested on their own |
| 9 | Scalability | Large apps easier to build & extend |
| 10 | Encapsulation | Each component manages its own logic/style without affecting others |
| 11 | Reduced duplication | No repeated HTML/CSS/JS |
| 12 | Better performance | Only changed components update, not whole page |
| 13 | Simpler debugging | Problems isolated to one component |
| 14 | Flexible composition | Complex pages built from smaller pieces |
| 15 | Easier collaboration | Teams work independently, fewer conflicts |

---

## 3. Real-World Analogy — The Car

Think of a car. It's made of independent, reusable parts:

```
Engine → Wheels → Doors → Steering → Seats
```

If a wheel breaks, you don't rebuild the whole car — you just replace that part.

Same with software: a webpage = header + sidebar + product list + cart + footer, each an independent, reusable component.

> **Note:** Plain JavaScript has **no built-in component feature**. This idea comes from frameworks/libraries like Angular, React, Vue, Svelte, and Web Components.

---

## 4. What is a Component in Angular?

In Angular, **everything on screen is a component** — the basic building block of the app.

> **An Angular component = Class + Template + Decorator**

```
┌─────────────────────────────┐
│      ANGULAR COMPONENT       │
│                               │
│  ┌─────────┐  ┌────────────┐│
│  │  CLASS  │  │  TEMPLATE  ││
│  │ (logic) │  │   (HTML)   ││
│  └─────────┘  └────────────┘│
│         ┌─────────────┐      │
│         │  DECORATOR   │      │
│         │ @Component() │      │
│         └─────────────┘      │
└─────────────────────────────┘
```

| Part | What it does |
|------|---------------|
| **Template** | Defines what the user *sees* — HTML + Angular's special syntax + data bindings |
| **Class** | Holds the data (properties) and logic (methods), written in TypeScript |
| **Decorator** | `@Component` — a special marker that adds metadata, turning a plain class into an Angular component |

---

## 5. Creating a Component with the CLI

Instead of making files by hand, ask the CLI:

```bash
ng generate component hello
```

Short form:

```bash
ng g c hello
```

This creates a folder with the component's files — the main one being **`hello.component.ts`**, where all three parts (class, template, decorator) live.

---

## 6. Building a Component — Step by Step

### Step 1: The Class

```typescript
export class AppComponent {
  name: string = "Angular";
}
```

- `name` → a **property**, type `string`, value `"Angular"`
- `export` → lets other parts of the app use this component

### Step 2: Import the Decorator

```typescript
import { Component } from "@angular/core";
```

### Step 3: Apply the Decorator + Metadata

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-hello",
  template: `<h1>Hello {{ name }}</h1>`,
})
export class AppComponent {
  name: string = "Angular";
}
```

This is a **complete Angular component**: class + template + decorator, all in one file.
Note: the template sits inside backticks (`` ` ``) so HTML can span multiple lines.

### Build Flow

```
CLASS (data + logic)
        │
        ▼
DECORATOR (@Component) ──► adds metadata (selector, template)
        │
        ▼
   TEMPLATE (HTML shown to user)
        │
        ▼
  FINAL COMPONENT
```

---

## 7. The Two Key Parts — Explained

### A. Template & Data Binding

```html
<h1>Hello {{ name }}</h1>
```

- `{{ name }}` → **data binding (interpolation)**
- Angular takes the `name` property from the class and inserts its value into the page
- Since `name = "Angular"` → page shows **"Hello Angular"**
- Change the property → page updates automatically

### B. The Selector

The **selector** is the custom HTML tag for the component.

```
selector: "app-hello"
```

Wherever Angular sees:

```html
<app-hello></app-hello>
```

...it replaces that tag with the component's template.

```
<app-hello></app-hello>   ──►   <h1>Hello Angular</h1>
     (selector tag)              (rendered output)
```

This is exactly like the `<product-card>` tag example from earlier — the selector is how you *place* a component on a page.

---

## 8. Running the App

```bash
ng serve
```

Then open:

```
http://localhost:4200
```

Result: page shows **"Hello Angular"**
- `<app-hello>` tag was replaced by the template
- `{{ name }}` was filled in from the class

---

## 9. Component Communication (Theory Only — Practice Tomorrow)

Angular components can talk to each other in a **parent → child** relationship:

```
        PARENT COMPONENT
              │
     @Input ──┼──► sends data DOWN to child
              │
              ▼
        CHILD COMPONENT
              │
    @Output ──┼──► sends events UP to parent
              │
              ▲
        PARENT COMPONENT
```

| Decorator | Direction | Purpose |
|-----------|-----------|---------|
| `@Input()` | Parent → Child | Pass data down into a child component |
| `@Output()` | Child → Parent | Send events up from child to parent |

*(Hands-on practice for this comes in the next class.)*

---

## 10. Quick Recap

- A component = reusable, self-contained UI piece (HTML + CSS + logic)
- Why: reusability, maintenance, consistency, testing, teamwork
- In Angular: **Component = Class + Template + Decorator**
  - Class → data & logic
  - Template → HTML shown to user (with `{{ }}` binding)
  - Decorator (`@Component`) → marks the class, adds selector + template
- Selector → custom tag (e.g. `app-hello`) that Angular replaces with the template
- CLI command: `ng generate component <name>` (short: `ng g c <name>`)


---