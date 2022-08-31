# WAI-ARIA

`WAI-ARIA` stands for the `Web Accessibility Initiative’s Accessible Rich Internet` Applications specification. The purpose of WAI-ARIA (often referred to as just ARIA) is to define a way to make web content more accessible when native HTML is unable to do so.

## The Five Rules of ARIA

1. Always use native HTML elements and attributes over ARIA when possible.
2. Never change native semantics, unless you have no other choice.
3. All interactive ARIA controls must be usable with a keyboard.
4. Never use `role='presentation'` or `aria-hidden='true'`on focusable elements.
5. All interactive elements must have an accessible name.

## ARIA Labels

The `aria-label` attribute overrides any native label and modifies the name property in the accessibility tree, though it’s best used when an element doesn’t already have a native label. When you add `aria-label` to an element, you pass in a string as the value, which will become that elements accessible name. `aria-label` doesn’t work on every HTML element, though. Adding the attribute to a plain `<div>` or a `<span>`will have no effect, for example.

A common use for this attribute can be for the “close” button often seen in menus or modals:

```html
<button type='button' aria-label='Close menu'>X</button>
```

## aria-labelledby

The `aria-labelledby` attribute overrides both native labels as well as the `aria-label`attribute. When you use this attribute, the accessible name of the labeled element (the one with the `aria-labelledby` attribute) has its accessible name changed to a concatenated string of the text contents or `alt` attributes of the labeling elements (the ones whose `id` are passed in)

```html
<!-- Here's the labelling element -->
<h2 id='label'>Shirts</h2>

<!-- And here's the labelled element. Note the order of the ID references passed in -->
<button type='button' id='shop-btn' aria-labelledby='label shop-btn'>Shop Now</button>
```

Although it may work somewhat similarly to the native `<label>` element, `aria-labelledby` does not have the same event handling by default. This is functionality you would have to add in yourself via JavaScript.

## aria-describedby

The `aria-describedby` attribute modifies the description property in the accessibility tree. Similar to the `aria-labelledby` attribute, when you use this attribute you pass in the `id` values of other elements as the `aria-describedby` value, and the elements whose `id` value are passed in can also be visually hidden.

```html
<label>Password:
  <input type='password' aria-describedby='password-requirements' />
</label>

<!-- Meaningful text + ARIA! -->
<span id='password-requirements'>Password must be at least 10 characters long.</span>
```
## Hiding Content from the Accessibility Tree

Similar to how you can visually hide elements with the `hidden` HTML attribute or the `display` and `visibility` CSS properties, you can use the `aria-hidden` attribute to hide certain elements, such as decorative images and icons, from the accessibility tree. The difference with `aria-hidden`, however, is that the element will remain visible for sighted users. This can be especially useful when you want to add an icon inside of another element. For example, if we were to use Material Icons inside of a button:

```html
<!-- Example 1 -->
<button type='button'>
  <span class='material-icons'>add</span>
  Add Book
</button>

<!-- Example 2 -->
<button type='button'>
  <span class='material-icons' aria-hidden='true'>add</span>
  Add Book
</button>
```


