# Finite-state Machines

## Introduction

Explored, here, are uses of parallel finite-state machines for determining which:

1. menu items in an application's menuing system to instantaneously display or enable.
2. functions from a larger set of functions to instantaneously provide to interoperating AI systems.

## Mathematics

Using the standard notation for deterministic finite-state machines, a finite-state machine can be represented as a tuple $(\Sigma, S, s_{0}, \delta, F)$.

* $\Sigma$ is the input alphabet, for our purposes events.
* $S$ is a finite non-empty set of states.
* $s_{0}$ is an initial state, $s_{0} \in S$.
* $\delta$ is the transition function, $\delta : S \times \Sigma \rightarrow S$.
* $F$ is the set of final states, $F \subseteq S$.

For a set of parallel finite-state machines, $M$, we can consider individual finite-state machines, $m_{i} = (\Sigma_{i}, S_{i}, s_{i, 0}, \delta_{i}, F_{i})$.

Letting $\phi_{i}$ be the set of menu items indicated to be displayed or enabled by the current state of a finite-state machine, $m_{i}$, under discussion is that the total set of menu items to be displayed or enabled by a software application, $\Phi_{M}$, can be considered to be:

$$\Phi_{M} = \bigcup\limits_{i=1}^{N} \phi_{i}$$

## Style

Some extensions to cascading stylesheets are presented here towards utilizing style to place data on the states of finite-state machines.

### Object Values

Ideas are presented here with respect to declaring values for style properties that are objects. Let us consider the following syntax with nested curly brackets:

```css
div { prop: { x: 123; y: 456; }; }
```

which intends to communicate that the element:

```xml
<div id="el" class="cls" />
```

would have a style property, `prop`, with a value that would be an object with properties, `prop.x` would be equal to `123` and `prop.y` would be equal to `456`.

### Multiple Values

Ideas are presented here with respect to declaring multiple values for style properties within and across declarations. Let us consider the following CSS-based syntax:

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

## Markup

The following markup-language sketch shows a simple approach for expressing FSMs with interoperating script and style.

With respect to FSMs, selectors could select sets of states for attaching properties and values. There could be two special properties, `menu` and `export`. The `menu` set of functions would be those which are to be instantaneously enabled in an application's menuing system. The `export` set of functions would be those functions which are to be instantaneously available to external components such as AI assistants.

```xml
<automata version="1.0">
  <head>
    <script type="text/javascript src="..." />
    <style type="text/css">
      <![CDATA[
        state { *menu: yield(func0); *export: yield(cp_func0); }
        #main, #second, #third { *menu: yield(func1) yield(func2) yield(func3); }
        .has-selection { *menu: yield(func4); selection: true; }
        .txt-selection { *menu: yield(func5); *export: yield(cp_func1); }
        .img-selection { *menu: yield(func6); *export: yield(cp_func2); }
      ]]>
    </style>
  </head>
  <body>
    <automaton id="fsm1" initial="main">
      <state id="main">
        <transition event="..." target="second" />
        <transition event="..." target="third" />
      </state>
      <state id="second" class="has-selection txt-selection" />
      <state id="third"  class="has-selection img-selection" />
      <state id="fourth" style="*menu: yield(func7)" />
    </automaton>
  </body>
</automata>
```

## Object Model

Finite-state machine object models can provide programmatic access to applications' FSMs, their states, and transitions, e.g.,

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
