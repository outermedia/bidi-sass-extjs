# bidi-sass-extjs
SASS mixin collection to simplify bidirectional support in ExtJS framework (v4.x)

## Supported styles

- `padding`
- `padding-left`
- `padding-right`
- `margin`
- `margin-left`
- `margin-right`
- `border-width`
- `border-left-width`
- `border-right-width`
- `border-style`
- `border-left-style`
- `border-right-style`
- `border-color`
- `border-left-color`
- `border-right-color`
- `border-left`
- `border-right`
- `border-radius` (cross-browser aware with vendor-prefixes)
- `border-top-left-radius` (cross-browser aware with vendor-prefixes)
- `border-top-right-radius` (cross-browser aware with vendor-prefixes)
- `border-bottom-right-radius` (cross-browser aware with vendor-prefixes)
- `border-bottom-left-radius` (cross-browser aware with vendor-prefixes)
- `clear`
- `float`
- `text-align`
- `extjs-bidi` (applies multiple styles in single selector)

## Examples

### Single styles
Generating single styles in a direction aware fashion looks like this
```scss
.foo {
    @include padding(1px 2px 3px 4px); // compact style variant
    @include margin-left(.5em);
}
```
and results in the following CSS
```css
.foo:not(.x-rtl) {
    padding: 1px 2px 3px 4px;
}

.foo.x-rtl {
    padding: 1px 4px 3px 2px;
}
.foo:not(.x-rtl) {
    margin-left: .5em;
}

.foo.x-rtl {
    margin-right: .5em;
}
```

### Combined styles
You can avoid redundant selectors by using the following `mixin` to set multiple styles in one step
```scss
.foo {
    @include extjs-bidi((
        padding: 1px 2px 3px 4px,
        margin-left: .5em
    ));
}
```
to generate styles combined in one selector
```css
.foo:not(.x-rtl) {
    padding: 1px 2px 3px 4px;
    margin-left: .5em;
}

.foo.x-rtl {
    padding: 1px 4px 3px 2px;
    margin-right: .5em;
}
```

### Sub-selectors
All mixins accept an optional sub-selector
```scss
.foo {
    @include margin-left(.5em, "bar");
}
```
which is appended to the selector the mixin is included into
```css
.foo:not(.x-rtl) .bar {
    margin-left: .5em;
}

.foo.x-rtl .bar {
    margin-right: .5em;
}
```

### Named parameters
Use named parameters in more complex cases for improved readability
```scss
.foo {
    @include extjs-bidi($sub-selector: "bar", $styles: (
        padding: 1px 2px 3px 4px,
        margin-left: .5em
    ));
}
```