# Finite-state Machine Object Model

Software applications can have one or more [finite-state machines](https://en.wikipedia.org/wiki/Finite-state_machine) (FSMs). Each state of an FSM can have a set of functions attached to it. The functions which are instantaneously available from an application are the union of those sets of functions available at each of the application's FSM's current states. The total functions which are instantaneously available from an application can be useful for determining which commands to enable in menuing systems and which functions to providing to interoperating AI assistants.

As software applications interact with users, agents, and incoming data, they can change the current states of their FSMs, e.g., via transitions.

## Described Functions

Descriptions of functions can include natural-language names and descriptions of them and their parameters. Function descriptions can also provide text-based paths for placing functions into menuing systems, e.g., "View/Zoom/Zoom in".

## Style-based Selectors

CSS-based selectors can select sets of states for attaching described functions to each state in those sets. There could be two special-purpose properties, `menu` and `assistant`. The `menu` set of functions would be those which are enabled in an application's menuing system. The `assistant` set of functions would be those functions which are to be instantaneously available to AI assistants.

```css
state { menu: +foo0; assistant: +cp_foo0 }
#main, #second, #third { menu: +foo1 +foo2 +foo3 }
.has_selection { menu: +foo4 }
.txt_selection { menu: +foo5; assistant: +cp_foo1 }
.img_selection { menu: +foo6; assistant: +cp_foo2 }
```

## Markup

The following markup language, FSML, shows a simple approach for expressing FSMs.

```xml
<automata version="1.0">
  <automaton id="m1" initial="main">
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
var c = m1.getStateById('main').className;
var s = m1.currentState;
m1.transition(event);
```

## See Also

* [SCXML](https://www.w3.org/TR/scxml/)
