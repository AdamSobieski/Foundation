# Finite-state Machine Object Model

Software applications can have one or more [finite-state machines](https://en.wikipedia.org/wiki/Finite-state_machine) (FSMs). Each state of an FSM can have a set of functions attached to it. The functions which are instantaneously available from an application are the union of those sets of functions available at each of the application's FSM's current states. The total functions which are instantaneously available from an application can be useful for determining which commands to enable in menuing systems and which functions to providing to interoperating AI assistants.

As software applications interact with users, agents, and incoming data, they can change the current states of their FSMs, e.g., via transitions.

## Described Functions

Descriptions of functions can include natural-language names and descriptions of them and their parameters. Function descriptions could also provide text-based paths for placing functions into menuing systems, e.g., `"View/Zoom/Zoom in"`.

## Styling

In CSS, [cascade](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade) and [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) are the means by which user agents determine which singular property values, from candidates originating from different sources, to assign to elements' properties.

Ideas are presented here with respect to declaring multiple values for properties across declarations. Let us consider the following CSS-based syntax:

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

With respect to FSMs, CSS-based selectors could select sets of states for attaching described functions to each state in those sets. There could be two special-purpose properties, `menu` and `export`. The `menu` set of functions would be those which are to be instantaneously enabled in an application's menuing system. The `export` set of functions would be those functions which are to be instantaneously available to external components such as AI assistants.

In addition to states having sets of functions attached to them, states could have data attached to them. In the following example, states with class `has_selection` would have a property, `selection` set to `true`.

```css
state { *menu: yield(foo0); *export: yield(cp_foo0); }
#main, #second, #third { *menu: yield(foo1) yield(foo2) yield(foo3); }
.has_selection { *menu: yield(foo4); selection: true; }
.txt_selection { *menu: yield(foo5); *export: yield(cp_foo1); }
.img_selection { *menu: yield(foo6); *export: yield(cp_foo2); }
```

## Markup

The following markup language, FSML, shows a simple approach for expressing FSMs.

```xml
<automata version="1.0">
  <automaton id="fsm1" initial="main">
    <state id="main">
      <transition event="..." target="second" />
    </state>
    <state id="second" class="has_selection txt_selection" />
    <state id="third"  class="has_selection img_selection" />
    <state id="fourth" style="*menu: yield(foo7)" />
  </automaton>
</automata>
```

## Object Model

A finite-state machine object model (FSMOM) will provide programmatic access to the FSMs of an application and to their states and transitions, e.g.,

```js
var fsm1 = automata.getStateMachineById('fsm1');
var c = fsm1.getStateById('main').className;
var s = fsm1.currentState;
fsm1.transition(event);
```

With respect to accessing data on objects for states, something like `window.getComputedStyle()` could be of use

```js
var selection = window.getComputedStyle(s).getPropertyValue('selection');
```

and/or these data could be accessed via a `style` property.

```js
if(s.style.getPropertyValue('selection') == 'true') { ... }
```

With respect to multiple-valued properties, perhaps these could be iterated:

```js
var fsm1 = automata.getStateMachineById('fsm1');
var main = fsm1.getStateById('main');

for (const value of main.style.getPropertyValue('menu'))
{
  console.log(value);
}
```

## See Also

* [SCXML](https://www.w3.org/TR/scxml/)
* [DOM](https://dom.spec.whatwg.org/)
* [CSSOM](https://drafts.csswg.org/cssom/)
