# CSS Architecture

## Description
Modern CSS architecture patterns including CSS custom properties, container queries, and scalable styling strategies.

## CSS Custom Properties
```css
:root {
  --color-primary: #6366f1;
  --color-surface: #1a1a2e;
  --radius-md: 12px;
  --shadow-card: 0 4px 24px rgba(0,0,0,0.12);
}

[data-theme="light"] {
  --color-surface: #ffffff;
  --shadow-card: 0 2px 12px rgba(0,0,0,0.06);
}
```

## Container Queries
```css
.card-container {
  container-type: inline-size;
}

@container (min-width: 400px) {
  .card { display: grid; grid-template-columns: 1fr 2fr; }
}
```

## Naming Convention (BEM)
```css
.block {}
.block__element {}
.block--modifier {}

/* Example */
.card {}
.card__title {}
.card--featured {}
```

## Responsive Design
```css
/* Mobile-first approach */
.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

@media (min-width: 768px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 1200px) {
  .grid { grid-template-columns: repeat(3, 1fr); }
}
```
