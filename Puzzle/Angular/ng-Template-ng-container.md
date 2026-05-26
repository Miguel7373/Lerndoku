

This document explains **`ng-template`** and **`ng-container`** in Angular, what they are, why they exist, and how to use them correctly. These are **structural concepts**, meaning they affect how the DOM is rendered.

---

## 1. What is `ng-template`?

`ng-template` is **Angular’s way of defining a template that is NOT rendered by default**.

Think of it as:

> _"This is a piece of HTML Angular may use later, but don’t show it yet."_

### Key characteristics

- It does **not** render to the DOM automatically
    
- It only appears when Angular is told to use it
    
- Often used with structural directives like `*ngIf`, `*ngFor`, or `ngTemplateOutlet`
    

### Basic example

```html
<ng-template>
  <p>This will not be shown</p>
</ng-template>
```

Nothing appears on the page.

---

## 2. `ng-template` with `*ngIf`

Angular internally converts `*ngIf` into an `ng-template`.

### Example

```html
<p *ngIf="isLoggedIn">Welcome back!</p>
```

Behind the scenes, Angular treats this as:

```html
<ng-template [ngIf]="isLoggedIn">
  <p>Welcome back!</p>
</ng-template>
```

---

## 3. `else` with `ng-template`

`ng-template` is commonly used for `else` blocks.

### Example

```html
<div *ngIf="isAdmin; else noAccess">
  Admin Panel
</div>

<ng-template #noAccess>
  <p>Access denied</p>
</ng-template>
```

### How this works

- If `isAdmin` is `true` → first block renders
    
- If `false` → Angular renders the `ng-template` named `noAccess`
    

---

## 4. What is `ng-container`?

`ng-container` is a **logical wrapper that does NOT appear in the DOM**.

Think of it as:

> _"Group elements together without adding an extra HTML element."_

### Why it exists

Angular structural directives (`*ngIf`, `*ngFor`) can only be placed **once per element**.

`ng-container` solves this.

---

## 5. Basic `ng-container` example

```html
<ng-container *ngIf="isVisible">
  <h1>Title</h1>
  <p>Description</p>
</ng-container>
```

### Result

- If `isVisible` is `true` → both elements render
    
- No extra `<div>` is added to the DOM
    

---

## 6. `ng-container` vs `div`

### Using `div`

```html
<div *ngIf="condition">
  <p>Hello</p>
</div>
```

Adds a `<div>` to the DOM.

### Using `ng-container`

```html
<ng-container *ngIf="condition">
  <p>Hello</p>
</ng-container>
```

Adds **nothing** to the DOM.

✔ Cleaner HTML  
✔ Better CSS control

---

## 7. Multiple structural directives (IMPORTANT)

This is **not allowed** ❌

```html
<div *ngIf="show" *ngFor="let item of items"></div>
```

### Correct solution using `ng-container`

```html
<ng-container *ngIf="show">
  <div *ngFor="let item of items">
    {{ item }}
  </div>
</ng-container>
```

---

## 8. `ng-template` + `ng-container` together

```html
<ng-container *ngIf="items.length > 0; else empty">
  <div *ngFor="let item of items">
    {{ item }}
  </div>
</ng-container>

<ng-template #empty>
  <p>No items available</p>
</ng-template>
```

### Flow

- If items exist → list renders
    
- Otherwise → `empty` template renders
    

---

## 9. `ngTemplateOutlet`

`ngTemplateOutlet` allows you to **render a template manually**.

### Example

```html
<ng-template #card>
  <div class="card">Reusable Card</div>
</ng-template>

<ng-container *ngTemplateOutlet="card"></ng-container>
```

This renders the template content where the container is placed.

---

## 10. When to use what?

### Use `ng-template` when:

- You need conditional or delayed rendering
    
- You want `else` blocks
    
- You want reusable templates
    

### Use `ng-container` when:

- You need a wrapper without DOM output
    
- You want multiple structural directives
    
- You want cleaner HTML
    

---

## 11. Quick mental model

- `ng-template` → **"Hidden HTML blueprint"**
    
- `ng-container` → **"Invisible wrapper"**
    

---

## 12. Common mistakes

Expecting `ng-template` to render automatically  
Using `div` when `ng-container` is better  
Forgetting `#templateName` for `else`

---

## 13. Summary

- `ng-template` defines **what can be rendered**
    
- `ng-container` defines **where and how things are grouped**
    
- Both help keep Angular templates **clean, efficient, and readable**
    

---

Mastering these two concepts is essential for clean Angular code.