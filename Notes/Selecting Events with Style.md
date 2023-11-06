## Introduction

What if software system events could be selected using CSS-based selectors, e.g., for logging purposes?

With this, software systems could load CSS-based configuration files with which developers could specify which events to log or to otherwise process.

## Virtual DOM Structures

To use CSS-based selectors on events, _virtual DOM structures_ can be considered.

An event could be an element of one or more classes. This would resemble the [publish-subscribe pattern](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern).

```xml
<event class="cls1 cls2" />
```

Events could have attributes.

```xml
<event class="cls1 cls2" attr="value" />
```

Events could be raised with argument objects which could be child elements in a virtual DOM structure.

```xml
<event class="cls1 cls2">
  <argument key1="value1" key2="value2" />
</event>
```

## Multiple Event Types

Multiple types of events could be represented in a virtual DOM structure via elements, classes, or attributes' values.

```xml
<mouseevent class="cls1 cls2" />
```

```xml
<event class="mouseevent" />
```

```xml
<event type="mouseevent" class="cls1 cls2" />
```

## Event Selection

With a virtual DOM structure for events, selectors could describe events and their arguments.

A special-purpose CSS property, `log` could be used to indicate whether or not to log the event.

```css
event.cls1 { log: true; }
```

```css
event.cls1:has(> [key1='value1']) { log: true; }
```

A multi-valued special-purpose CSS property, `subscribe` could, similarly, indicate which logs to log the event to.

```css
event.cls1:has(> [key1='value1']) { subscribe: log1 log2; }
```

As described in [Objects and Iterators with Style](/Notes/Objects%20and%20Iteration%20with%20Style.md), multiple values for a property could be aggregated from multiple declarations.

```css
event.cls1:has(> [key1='value1']) { ^*subscribe: yield(log1) yield(log2); }
event.cls2 { ^*subscribe: yield(log3); }
```

## Selected Previous Works
* [DOM Events](https://dom.spec.whatwg.org/#events)
* [XES](https://xes-standard.org/)
* [OCEL](https://www.ocel-standard.org/)
* [xAPI](https://xapi.com/)
* [Caliper](https://www.imsglobal.org/activity/caliper)
