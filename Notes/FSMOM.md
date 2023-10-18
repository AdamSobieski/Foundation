# Finite-state Machine Object Model

Software applications can have one or more [finite-state machines](https://en.wikipedia.org/wiki/Finite-state_machine) (FSMs). Each state of an FSM can have a set of functions attached to it. The functions which are instantaneously available from an application are the union of those sets of functions available at each of the application's FSM's current states. The total functions which are instantaneously available from an application can be useful for determining which commands to enable in menuing systems and which functions to providing to interoperating AI assistants.

As software applications interact with users, agents, and incoming data, they can change the current states of their FSMs, e.g., via transitions.

## Described Functions

Descriptions of functions can include natural-language names and descriptions of them and their parameters. Function descriptions could also provide text-based paths for placing functions into menuing systems, e.g., `"View/Zoom/Zoom in"`.

## Styling

CSS-based selectors can select sets of states for attaching described functions to each state in those sets. There could be two special-purpose properties, `menu` and `export`. The `menu` set of functions would be those which are to be instantaneously enabled in an application's menuing system. The `export` set of functions would be those functions which are to be instantaneously available to external components such as AI assistants.

In addition to states having sets of functions attached to them, states could have data attached to them. In the following example, states with class `has_selection` would have a property, `selection` set to `true`.

```css
state { menu: +foo0; export: +cp_foo0 }
#main, #second, #third { menu: +foo1 +foo2 +foo3 }
.has_selection { menu: +foo4; selection: true }
.txt_selection { menu: +foo5; export: +cp_foo1 }
.img_selection { menu: +foo6; export: +cp_foo2 }
```

In CSS, the [cascade](https://developer.mozilla.org/en-US/docs/Web/CSS/Cascade) is an algorithm that defines how user agents combine property values originating from different sources. Above, the `+value` syntax is meant to assign values to properties using another algorithm, one where elements of a set are to be added to a set from all sources.

That is, we can consider the following CSS-like syntax:
```css
div { p: +x }
#el { p: +y  }
.cls { p: +z }
```
which hopes to communicate that:
```html
<div id="el" class="cls" />
```
would have a set of values, `{x, y, z}`, for its property `p`. It would obtain `x` from being a `div` element, `y` from having an id of `el`, and `z` from having a class of `cls`.

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
    <state id="fourth" style="menu: +foo7" />
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
var selection = window.getComputedStyle(s, 'selection');
```

and/or these data could be accessed via a `style` property.

```js
if(s.style.selection) { ... }
```

## See Also

* [SCXML](https://www.w3.org/TR/scxml/)
* [CSSOM](https://drafts.csswg.org/cssom/)
