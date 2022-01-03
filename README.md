# Reduce JavaScript

JavaScript allows dynamic interactions and changes to a website.  
This list collects ways to implement typical JavaScript features without JavaScript.

## Features

### Lightbox

The CSS `:target` Selector can be used to implement a CSS-only lightbox.

Browser compatibility: All modern browsers and IE9+ (see [caniuse](https://caniuse.com/?search=%3Atarget))  
See: https://developer.mozilla.org/en-US/docs/Web/CSS/:target#pure-css_lightbox



## Addendum: Reduce jQuery

jQuery is a popular JS framework used on millions of websites. When used incorrectly, it can increase loading times by quite a lot!

For example, each call of `$('.element')` will take some time. Therefore duplicate calls should be avoided. It is better to define a constant `const $element = $('.element');` and use `$element` instead of separate calls.

Another example:
```javascript
// <div class="element" style="display: none"><h1>Test</h1></div>
const $element = $('.element');
$element.show();
$element.find('h1').text('Hello!');
```

However JavaScript evolved quite a bit, so one may not even need to use jQuery for most parts:

```diff
-$('.element')
+document.querySelectorAll('.element')
```
```diff
-$('.element')[0]
+document.querySelector('.element')
```
```diff
-$('.element')[0].find('li')
+document.querySelector('.element').querySelectorAll('li')
```

```diff
-$(() => {
+document.addEventListener('DOMContentLoaded', () => {
  console.log('loaded');
}
```

Where needed, one can still create a jQuery object:

```javascript
const myElement = document.querySelector('.element');
const $myElement = $(myElement);
$myElement.show();
// querySelector does not know :hidden pseudo selector
const $hiddenElement = $('.element:hidden');
```
