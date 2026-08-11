# Day 1: Introduction to Angular – Frontend Frameworks.


---

## 1. What is Angular?

Angular is a **JavaScript framework** used to build web applications. It is made and maintained by **Google**.

A lot of developers use it because it gives many benefits over writing plain JavaScript. Let's understand those benefits one by one.

Angular takes plain HTML and makes it dynamic — it can show/hide content, repeat items in a list, and update the screen automatically based on your code, without reloading the page.

It also connects your HTML directly to your data, so if the data changes, the screen updates instantly (this is called data binding).

And it breaks your page into small reusable pieces called components, so big apps stay organized and easy to manage.

---

## 2. Why use Angular? (Benefits)

### A) Performance (Speed)
Angular apps:
- Load fast in the beginning
- Detect changes efficiently (updates only the part of the screen that changed)
- Render (show) content quickly on screen

In short: **App opens fast + app updates fast.**

Angular also gives us:
- **Modularity** → code is split into small, clean, separate parts (easy to manage)
- **Dependency Injection** → an easy way to share code/services between different parts of the app
- **Testability** → it is easy to write tests for the app

Angular keeps getting faster with every new version. Right now Angular is on **version 22**, and speed improvement is a main goal in every update.

### B) Mobile Support
Angular is built keeping mobile phones in mind from day one — touch screens, small screens, less powerful hardware, everything is considered.

Because of this, we can build **one single app** that works properly on both **mobile and desktop**, without needing extra third-party tools.

### C) Language Choice
Angular lets us write code in:
- Plain JavaScript, OR
- Newer JavaScript versions, OR
- **TypeScript** (most popular, and what we will use in this course)

Angular itself is built using TypeScript.

---

## 3. What is ECMAScript?

**ECMAScript = the official name of the JavaScript language.**

- Every year, a new version of ECMAScript is released with new features.
- ECMAScript 6 was renamed to **ES2015** (same thing, different name).
- ES2015 gave us features we use daily now — classes, modules, arrow functions.

**One-line definition:** ECMAScript is just the official name for JavaScript, and it gets a new version every year.

---

## 4. What is TypeScript?

**TypeScript = JavaScript + extra features**, made by **Microsoft**.

- It is a **superset of JavaScript** → meaning: any JavaScript code is already valid TypeScript. TypeScript just adds more on top of it.
- Browsers cannot run TypeScript directly. So there is a **compiling step** that converts TypeScript into plain JavaScript.
- Main things TypeScript adds:
  - **Types** (so you catch mistakes early)
  - Object-Oriented features like **classes, interfaces, inheritance** (similar to Java/C++)

If you already know OOP (Object-Oriented Programming), TypeScript will feel easy.
---

## 5. Flow: JavaScript → TypeScript → Angular

```
        ECMAScript (official name of JS)
                  |
                  v
        JavaScript (the actual language)
                  |
                  v
        TypeScript (JS + Types + OOP features)
                  |
          (compiling step)
                  |
                  v
        Plain JavaScript (browser understands this)
                  |
                  v
        Angular App runs in the browser
```

---

## 6. What is Angular CLI?

**CLI = Command Line Interface.** It is Angular's official tool that you use with the `ng` command.

Instead of setting up files and folders manually, CLI does all the heavy work for you:
- Creates the project
- Generates code
- Runs the app
- Builds it for release/production

**One-line definition:** Angular CLI is a helper tool you run in the terminal — it creates, builds, and runs your Angular project so you can focus only on writing the app.

### Most Used CLI Commands

| Command | What it does |
|---|---|
| `ng new <name>` | Creates a brand-new Angular project, fully set up |
| `ng serve` | Runs the app on your machine, auto-reloads on save |
| `ng generate component <name>` (short: `ng g c <name>`) | Creates a new component with all its files |
| `ng build` | Packages the app into final files for a real server |
| `ng test` | Runs your tests |
| `ng version` | Shows installed Angular/CLI versions |

**Why CLI matters:** It gives every Angular project the same clean structure, and saves hours of manual setup. One command → a whole working feature appears, correctly wired up.

---

## 7. Quick Revision (Remember This)

- Angular = popular framework from Google for building web apps
- **Performance:** fast loads + fast updates + clean modularity + dependency injection + easy testing
- **Mobile:** one single app works on both mobile & desktop
- **Language:** we write Angular in TypeScript (most popular choice)
- **ECMAScript** = official name of JavaScript
- **TypeScript** = JavaScript + types, made by Microsoft
- **Install steps:** Node.js → `npm install -g @angular/cli` → `ng new` → `ng serve`
- **CLI (`ng`)** = the tool that creates, runs, and builds your app for you

---