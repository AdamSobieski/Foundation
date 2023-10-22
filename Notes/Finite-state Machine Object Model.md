# Finite-state Machine Object Model

## Introduction

Explored, here, are uses of parallel finite-state machines for determining which:

1. menu items in an application's menuing system to display or enable.
2. functions from a larger set of functions to provide contextually to interoperating AI systems.

## Mathematics

Using the standard notation for deterministic finite-state machines, a machine can be represented as a tuple $(\Sigma, S, s_{0}, \delta, F)$.

$\Sigma$ is the input alphabet, for our purposes events. $S$ is a finite non-empty set of states. $s_{0}$ is an initial state, $s_{0} \in S$. $\delta$ is the transition function, $\delta : S \times \sigma \rightarrow S$. $F$ is the set of final states, $F \subseteq S$.

For a set of parallel finite-state machines, $M$, we can consider each finite-state machine, $m_{i} = (\Sigma_{i}, S_{i}, s_{i, 0}, \delta_{i}, F_{i})$.

Let us use the symbol $c_{i}$ to indicate the current state of finite-state machine $m_{i}$.

Those menu items to be displayed or enabled in a software application can be defined to be the union of those expressed to be enabled on the current state of each parallel finite-state automaton in its system of parallel finite-state machines.

$$\bigcup\limits_{i=1}^{N} f(c_{i})$$

where $f(\cdot)$ is the set of menu items expressed to be displayed or enabled at a state.

## Style

### Object Values

Ideas are presented here with respect to declaring values for style properties that are objects. Let us consider the following syntax with nested curly brackets:

```css
div { prop: { x: 123; y: 456; }; }
```

which intends to communicate that the element:

```xml
<div id="el" class="cls" />
```

would have a style property, `prop`, with a value that would be an object with properties. The expression `prop.x` would be equal to `123` and `prop.y` would be equal to `456`.

### Multiple Values

Ideas are presented here with respect to declaring multiple values for style properties across declarations. Let us consider the following CSS-based syntax:

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

### Finite-state Machines

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

The following markup language sketch shows a simple approach for expressing FSMs with interoperating script and style.

```xml
<automata version="1.0">
  <head>
    <style type="text/css">
      <![CDATA[
        state { *menu: yield(foo0); *export: yield(cp_foo0); }
        #main, #second, #third { *menu: yield(foo1) yield(foo2) yield(foo3); }
        .has_selection { *menu: yield(foo4); selection: true; }
        .txt_selection { *menu: yield(foo5); *export: yield(cp_foo1); }
        .img_selection { *menu: yield(foo6); *export: yield(cp_foo2); }
      ]]>
    </style>
  </head>
  <body>
    <automaton id="fsm1" initial="main">
      <state id="main">
        <transition event="..." target="second" />
      </state>
      <state id="second" class="has_selection txt_selection" />
      <state id="third"  class="has_selection img_selection" />
      <state id="fourth" style="*menu: yield(foo7)" />
    </automaton>
  </body>
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

## Selected Previous Works
* [SCXML](https://www.w3.org/TR/scxml/)
* [Apache Commons SCXML](http://jakarta.apache.org/commons/scxml/)
* [JSSCxml](https://github.com/Touffy/JSSCxml)
* [uSCXML](https://github.com/tklab-tud/uscxml)
* [PySCXML](https://github.com/jroxendal/PySCXML)
* [XState](https://github.com/statelyai/xstate)
