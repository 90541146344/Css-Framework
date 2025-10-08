# AuroraCSS — Custom CSS Framework

## 🌐 Framework Overview
AuroraCSS is a lightweight, customizable CSS framework built using **Sass**.  
It provides a clean and consistent design theme for all standard HTML elements and includes powerful utility classes for fast and flexible styling.

---

## 🎯 Objective
The goal of this framework is to make it easy for developers to build responsive, visually appealing websites using a consistent theme and reusable utility classes.

---

## 🧩 Features & Requirements

### 1. Built with Sass and Sass Partials
AuroraCSS is structured using multiple Sass partials for better organization and scalability:
```
scss/
├── _variables.scss
├── _mixins.scss
├── _base.scss
├── _components.scss
├── _utilities.scss
└── main.scss
```

### 2. Customizable Using Variables
The framework uses **Sass and CSS variables** that can be easily modified to match any design preference.
```scss
$color-primary: #007bff;
$font-base: 'Inter', sans-serif;

:root {
  --color-primary: #007bff;
  --font-base: 'Inter', sans-serif;
}
```

### 3. Custom Theme for Standard HTML Elements
AuroraCSS applies consistent and elegant styles for:
- Headings (`h1–h6`)
- Lists (`ul`, `ol`)
- Buttons (`.btn`, `.btn-primary`, `.btn-outline`)
- Forms and Inputs (`input`, `textarea`, `select`)
- Tables (`table`, `th`, `td`)

### 4. Utility Classes for Common Styling
Utility classes provide flexibility for quick styling adjustments:
- **Colors:** `.text-primary`, `.bg-light`
- **Font Weight:** `.fw-bold`, `.fw-light`
- **Font Size:** `.fs-1`, `.fs-2`
- **Margin & Padding:** `.m-2`, `.p-3`, `.mt-4`, `.pb-2`
- **Borders:** `.border`, `.border-primary`, `.rounded`

### 5. Consistent and Appealing Theme
All elements in AuroraCSS share a cohesive color palette, spacing scale, and typography system — ensuring a professional and unified visual style across websites.

### 6. Compiled CSS Version
Both compiled and minified CSS versions are included:
```
dist/
├── aurora.css
└── aurora.min.css
```

### 7. Installation, Usage & Customization

#### Installation
You can install or clone the framework using Git:
```bash
git clone https://github.com/<your-username>/aurora-css-framework.git
```

#### Usage
Include the compiled CSS in your HTML:
```html
<link rel="stylesheet" href="dist/aurora.css">
```

#### Customization
Modify the values inside `_variables.scss` or override them with CSS variables:
```css
:root {
  --color-primary: #ff6b6b;
  --font-base: 'Poppins', sans-serif;
}
```

---

## 🧑‍💻 Team Members
- Team Leader: [Navneet Dhillon]
- Member 1: [Filepe Olliveira]
- Member 2: [Sristi Sharma]
- Member 3: [Jasleen Kaur]
- Member 4: [Subham Thappa]

---


