# Angular — Binding, Directives & Pipes (Deep Dive)
---

The template is the HTML the user sees. Angular gives it superpowers: showing data, reacting to clicks, looping over lists, showing things conditionally, and formatting values. This note breaks each of those superpowers down properly — what it does, why it exists, and how data actually flows.

---

## Data Binding: The Four Kinds

Binding is simply the **connection** between your class (the TypeScript data) and your template (the HTML view). The direction of that connection is what changes, and the brackets tell you which direction.

```
   CLASS (TypeScript)                    TEMPLATE (HTML)
   ┌─────────────────┐                   ┌─────────────────┐
   │  name = "X"     │                   │  <h1>{{name}}   │
   │  imageUrl = ".."│  ───── data ────► │ <img [src]=..   │
   │  isBusy = true  │                   │ <button [dis. . │
   └─────────────────┘                   └─────────────────┘
                                                │
   ┌────────────────┐                           │
   │  save() {...}  │  ◄──── event ─────────────┘
   └────────────────┘     <button (click)=..>
```

### Interpolation — `{{ }}`

This is the simplest binding. It takes a value from the class and **prints it as text** inside the HTML. It is **one-way** and **read-only** — class to view, nothing goes back.

```html
<h1>Hello {{ name }}</h1>
```
```ts
// class
name = "Angular";
```
Output on page: `Hello Angular`

Think of `{{ }}` as a **placeholder** — wherever it sits in the HTML, Angular quietly replaces it with the class value, and keeps it updated automatically whenever that value changes.

---

### Property Binding — `[ ]`

Interpolation only writes **text**. But what if you want to set an actual **property** of an HTML element — like whether a button is disabled, or which image an `<img>` tag points to? That's what square brackets do.

```html
<img [src]="imageUrl" />
<button [disabled]="isBusy">Save</button>
```

Here, `[src]` is not text on the page — it is literally setting the `src` property of the `<img>` element to whatever `imageUrl` holds in the class. Same with `[disabled]` — if `isBusy` is `true`, the button becomes disabled; if `false`, it becomes clickable again.

**Key difference from `{{ }}`:**

| | `{{ }}` Interpolation | `[ ]` Property Binding |
|---|---|---|
| Used for | Displaying text between tags | Setting a property/attribute on a tag |
| Example | `<h1>{{ name }}</h1>` | `<img [src]="imageUrl" />` |
| Data type | Always becomes a string | Can be any type (string, boolean, number, object) |

---

### Event Binding — `( )`

So far both directions moved data **into** the template. Event binding flips it — it lets the **view talk back to the class**. When something happens on the page (a click, a keypress, a form submit), round brackets catch that event and call a method in your class.

```html
<button (click)="save()">Save</button>
```
```ts
// class
save() {
  console.log("saved!");
}
```

Every time the user clicks the button, Angular runs `save()`. This is **view to class** — the opposite direction of `{{ }}` and `[ ]`.

```
   [ ]  Property Binding    class ──────► view    (data goes IN)
   ( )  Event Binding        view ──────► class    (event goes OUT)
```

---

### Two-Way Binding — `[( )]`

What if you need **both directions at once**? Type something in a box, and the class property should update immediately — *and* if the class property changes some other way, the box should reflect that too. That's two-way binding, nicknamed **"banana in a box"** because of how `[()]` looks.

```html
<input [(ngModel)]="username" />
<p>You typed: {{ username }}</p>
```

```
        ┌──────────────────────┐
        │   <input>  (view)    │
        └──────────┬───────────┘
             ▲              │
      class updates    user types
      box shows it      box updates class
             │              ▼
        ┌─────────────────────┐
        │  username  (class)  │
        └─────────────────────┘
```

**Important setup note:** Two-way binding with `ngModel` requires `FormsModule`.
- In an **older NgModule-based project** → add `FormsModule` to that module's `imports` array.
- In a **standalone component** → add `FormsModule` directly to the component's own `imports` array.

Without this import, `[(ngModel)]` will throw an error, because Angular doesn't know what `ngModel` means without `FormsModule` providing it.

---

### The Four Bindings, Side by Side

```
┌────────────────┬───────────────────┬───────────────────────────────┐
│   Syntax       │   Direction       │   What it does                │
├────────────────┼───────────────────┼───────────────────────────────┤
│  {{ value }}   │  class → view     │  Shows a value as text        │
│  [ property ]  │  class → view     │  Sets an element's property   │
│  ( event )     │  view → class     │  Runs a method on an event    │
│  [( ngModel )] │  class ⇄ view    │  Keeps both in sync, always   │
└────────────────┴───────────────────┴───────────────────────────────┘
```

**One-line memory trick:** Square brackets = data going **in**. Round brackets = event coming **out**. Both together = **two-way**.

---

## Directives: `*ngIf`, `*ngFor`, `ngSwitch`

A **directive** is a special instruction you place on an HTML element to change how that element behaves — whether it shows up, how many times it repeats, or which version of it appears. The three structural directives you'll use constantly all start reshaping the actual DOM structure (not just styling it).

```
                     TEMPLATE ELEMENT
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
        *ngIf           *ngFor         ngSwitch
     (show/hide)     (repeat for      (pick ONE
                       each item)      of many)
```

---

### *ngIf — Show or Hide

`*ngIf` decides whether an element exists on the page **at all**, based on a condition. If the condition is `false`, Angular doesn't just hide it with CSS — it **removes the element completely** from the DOM.

```html
<p *ngIf="isLoggedIn">Welcome back!</p>
<p *ngIf="!isLoggedIn">Please log in.</p>
```

```
   isLoggedIn = true                 isLoggedIn = false
   ┌─────────────────────┐              ┌──────────────────┐
   │ <p>Welcome back!</p>│              │  (nothing here)  │
   │ (removed: 2nd <p>)  │              │ <p>Please log in.│
   └─────────────────────┘              └──────────────────┘
```

This matters because a hidden-with-CSS element still exists in memory and in the DOM tree, while an `*ngIf`-removed element is **completely gone** until the condition becomes true again — which is more efficient when the content is heavy or shouldn't even be reachable.

---

### *ngFor — Loop Over a List

`*ngFor` repeats one element **once for every item** in an array. It's how you turn a list of data into a list of visible elements, without manually writing each one.

```html
<ul>
  <li *ngFor="let color of colors">{{ color }}</li>
</ul>
```
```ts
// class
fruits = ["Red", "Green", "Grey"];
```

```
   colors = ["Red", "Green", "Grey"]
                    │
                    ▼   *ngFor repeats the <li> once per item
   ┌───────────────────────────────┐
   │ <ul>                          │
   │   <li>Red</li>                │
   │   <li>Green</li>              │
   │   <li>Grey</li>               │
   │ </ul>                         │
   └───────────────────────────────┘
```

Three items in the array → three `<li>` elements on the page. If the array changes (an item added or removed), Angular automatically updates the list to match — you never manually add or remove `<li>` tags yourself.

---

### ngSwitch — Pick One of Many

`ngSwitch` is like a `switch` statement, but for your template. Instead of showing/hiding one thing (`*ngIf`) or repeating something (`*ngFor`), it picks exactly **one block** to display out of several possible options, based on a matching value.

```html
<div [ngSwitch]="role">
  <p *ngSwitchCase="'admin'">You are an admin</p>
  <p *ngSwitchCase="'user'">You are a user</p>
  <p *ngSwitchDefault>Unknown role</p>
</div>
```

```
                     role = "admin"
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
        case 'admin'   case 'user'    default
            MATCH         skip           skip
              │
              ▼
     Only shows: "You are an admin"
```

If `role` matches `"admin"`, only that line renders — the others are skipped entirely. If `role` doesnt match any case, `*ngSwitchDefault` acts as the fallback, similar to the `default` case in a normal JavaScript switch statement.

---

### Directives, Side by Side

```
┌──────────────┬───────────────────────────────────────────────┐
│  Directive   │  What it decides                              │
├──────────────┼───────────────────────────────────────────────┤
│  *ngIf       │  Should this element exist at all? (yes/no)   │
│  *ngFor      │  How many copies of this element are needed?  │
│  ngSwitch    │  Which ONE of several elements should show?   │
└──────────────┴───────────────────────────────────────────────┘
```

---

## Pipes: Formatting a Value for Display

A **pipe** transforms how a value **looks on screen**, without ever touching or changing the actual data stored in the class. You apply a pipe using the `|` symbol, right inside interpolation.

```
   RAW DATA (class)              PIPE (formatting)              DISPLAYED (view)
   ┌──────────────────┐            ┌──────────────┐            ┌───────────────┐
   │  name = "angular"│  ─────►    | uppercase    │  ─────►    │ ANGULAR       │
   └──────────────────┘            └──────────────┘            └───────────────┘

   The original "name" value in the class is still "angular" — only the DISPLAY changed.
```

```html
<p>{{ name | uppercase }}</p>            <!-- ANGULAR -->
<p>{{ price | currency:'INR' }}</p>      <!-- Rs 500.00 -->
<p>{{ today | date:'longDate' }}</p>     <!-- August 5, 2026 -->
```

**Commonly used built-in pipes:**

| Pipe | Purpose |
|---|---|
| `uppercase` | Converts text to ALL CAPS |
| `lowercase` | Converts text to all lowercase |
| `titlecase` | Capitalizes The First Letter Of Each Word |
| `date` | Formats a date value |
| `currency` | Formats a number as currency (e.g. `₹500.00`) |
| `number` | Formats a number (decimals, separators) |
| `percent` | Formats a number as a percentage |
| `json` | Converts an object to a readable JSON string (great for debugging) |
| `slice` | Cuts a portion of a string or array |

### Chaining Pipes

Pipes can be **chained** — the output of one pipe becomes the input of the next, read left to right.

```html
{{ name | slice:0:5 | uppercase }}
```

```
   name = "angular development"
              │
              ▼   slice:0:5  (takes first 5 characters)
          "angul"
              │
              ▼   uppercase
          "ANGUL"
```

---

## Custom Pipes: Building Your Own

When none of the built-in pipes do what you need, you can write your **own** pipe. A pipe is simply a class marked with the `@Pipe` decorator, containing one required method: `transform`.

```
     TEMPLATE                    PIPE CLASS                         RESULT
   ┌──────────────────┐       ┌──────────────────────────┐       ┌──────────┐
   │ {{ 10 | double }}│  ──►  │ transform(value) {       │  ──►  │    20    │
   └──────────────────┘       │   return value * 2;      │       └──────────┘
                              │ }                        │
                              └──────────────────────────┘
```

```ts
import { Pipe, PipeTransform } from "@angular/core";

@Pipe({ name: "double" })
export class DoublePipe implements PipeTransform {
  transform(value: number): number {
    return value * 2;
  }
}
```

Using it in a template:
```html
<p>{{ 10 | double }}</p> <!-- shows 20 -->
```

The `transform` method receives the value sitting on the **left** side of the `|`, does whatever calculation or formatting you write, and returns the changed result — which is what actually appears on the page. You can also generate a pipe file automatically using the Angular CLI: `ng generate pipe double`.

### 4.1 Pipes That Take Arguments

A pipe can also accept extra arguments, written after a colon `:` — just like the built-in `currency:'INR'` or `date:'longDate'` you saw earlier.

```ts
@Pipe({ name: "multiply" })
export class MultiplyPipe implements PipeTransform {
  transform(value: number, times: number): number {
    return value * times;
  }
}
```

```html
<p>{{ 10 | multiply:3 }}</p> <!-- shows 30 -->
```

```
   10 | multiply:3
        │      │
        │      └── second argument (times = 3)
        └───────── value going into transform() (value = 10)

   transform(10, 3)  →  10 * 3  →  30
```

The first value (before `|`) always maps to the pipe's main `value` parameter. Anything after the colon maps to the additional parameters of `transform`, in order.

---

## 5. How It All Fits Together

```
                         ANGULAR TEMPLATE
        ┌──────────────────────────────────────────────────────┐
        │                                                      │
        │   BINDING           connects class ⇄ view            │
        │   {{ }} [ ] ( ) [( )]                                │
        │                                                      │
        │   DIRECTIVES        reshapes WHAT is on the page     │
        │   *ngIf *ngFor ngSwitch                              │
        │                                                      │
        │   PIPES             changes HOW data LOOKS           │
        │   | uppercase | date | custom pipes                  │
        │                                                      │
        └──────────────────────────────────────────────────────┘
```

>Binding moves data between the class and the template. Directives decide **which elements exist** and **how many** of them appear. Pipes decide **how a value is displayed**, without ever changing the underlying data. Together, these three tools are what make an Angular template dynamic instead of static HTML.
---