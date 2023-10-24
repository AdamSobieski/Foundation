## Objects and Iteration with Style

Extensions to cascading stylesheets are presented here towards utilizing style to place data, properties and values, on the states of finite-state machines.

### Object Values

Ideas are presented here with respect to declaring values for style properties that are objects. Let us consider the following syntax:

```css
div { prop: { x: 123; y: 456; }; }
```

which intends to communicate that the element:

```xml
<div id="el" class="cls" />
```

would have a style property, `prop`, with a value that would be an object with properties, `prop.x` would be equal to `123` and `prop.y` would be equal to `456`.

### Multiple Values

Ideas are presented here with respect to declaring multiple values for style properties within and across declarations. Let us consider the following syntax:

```css
div { *prop: yield(x); }
#el { *prop: yield(y); }
.cls { *prop: yield(z) yield(w); }
```

which hopes to communicate that the element:

```html
<div id="el" class="cls" />
```

would have a set of values, `{x, y, z, w}`, for its property `prop`. It would obtain the value `x` from being a `div` element, the value `y` from having an id of `el`, and the values `z` and `w` from having a class of `cls`.
