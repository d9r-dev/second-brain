---
title: Accessibility
draft: false
publish: true
tags:
  - Accessibility
  - web-dev
date: 2024-09-02
---

## Accessibility Guidelines

### Landmarks
- **Header, Footer, Main, Aside, Nav, Section**: These elements have roles that assist screen readers.
- If there are multiple landmarks, describe them with `aria-label`, e.g., `<nav aria-label="social">`.
- **Aside** should be related to the main content.
- **Section** is independent of the main content.

### Buttons and Links
- The `<button>` element should be used for actions on the current page.
- The `<a>` element should be used for navigation to another view. Source

### Semantic Elements and Roles
- If you can't use the correct semantic element for technical reasons, assign a role to the element. For example, if a button is built as `<a>`, it should have `role="button"`. The `<button>` element already has this role built-in, so adding it would be redundant.
- Elements should have a name. For example, `<div role="button">Company</div>` has the name "Company".
- `<select name="countryCode">` does not have a name. The `name` attribute is for computers. Therefore, the select should have an `aria-label`.
- Example: `<select aria-label="Country calling code" name="countryCode">…</select>` 

### Custom Elements
- Custom elements should have a value. For example, an accordion can be open or closed.
- Example: `<div role="button" aria-expanded="false"> When do I get charged for a ride?</div>` Source

### Color and Contrast
- Do not rely solely on colors (for colorblind users). Links should remain underlined.

### Images
- **Decorative vs. Meaningful Images**:
  - Decorative images can be removed from the website without impact. They should have an empty `alt` attribute or be set as a CSS background image.
  - Icon fonts should have `role="img"` and `aria-hidden="true"`.
  - Inline SVGs should have `<svg aria-hidden="true">`.
  - Alt texts should ideally describe the function of the image, e.g., "Home of norelem".
  - Background images, SVGs, and fonts should have `role="img"` and `aria-label="*Descriptive Text*"`.

### Links
- Link states should be clearly distinguishable, readable, and have high contrast.
- Links should be meaningful. Google prefers descriptive link texts.
- Never remove visual focus.
- **Skip Links**: The first element that gets focused should be a link to the main content, e.g., on Amazon.

### Forms
- Inputs that describe required fields should have both the `required` attribute and `aria-required="true"`.
- Inputs without a label should have `aria-label="Description"`.
- Control groups should consist of `<fieldset>` and `<legend>`.

```html
<fieldset>
  <legend>Your date of birth</legend>
  <label for="dobDay">Day</label>
  <select id="dobDay">…</select>
  <label for="dobMonth">Month</label>
  <select id="dobMonth">…</select>
  <label for="dobYear">Year</label>
  <input id="dobYear" type="text" placeholder="YYYY">
</fieldset>
````

### Autocomplete

- Set up autocomplete for fields:
    - `<input id="email" autocomplete="email" name="email" aria-required="true" placeholder="Email" required>`
    - `<select id="dobDay" autocomplete="bday-day" aria-required="true" required>`
    - `<select id="dobMonth" autocomplete="bday-month" aria-required="true" required>`
    - `<input id="dobYear" autocomplete="bday-year" placeholder="YYYY" aria-required="true" required>` Source

### Error Handling

- Associate error messages with form controls using `aria-describedby`. The value should be the ID of the error message.
- Add `aria-invalid="true"` to the invalid form control to inform screen readers that the form control has failed. An improved version of the input field:

HTML

```html
<input name="firstName" id="firstNameInput" type="text" pattern="[^.]*?" aria-describedby="firstName-length-error" aria-invalid="true">
<p id="firstName-length-error" role="alert">Your first name must have at least two letters and no unusual characters</p>
```
