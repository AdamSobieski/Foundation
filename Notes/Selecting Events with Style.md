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

Types of events could be represented in a virtual DOM structure via elements' names.

```xml
<html:progressevent class="cls1 cls2">
  <argument key1="value1" key2="value2" />
</html:progressevent>
```

This would allow events to have XML names, with namespaces, and corresponding CSS-based selectors:

```css
html|* { log: true; }
```

## Event Selection

With a virtual DOM structure for events, selectors could describe events and their arguments.

A special-purpose CSS property, `log` could be used to indicate whether or not to log the event.

```css
.cls1 { log: true; }
```

```css
.cls1:has(> [key1='value1']) { log: true; }
```

A multi-valued special-purpose CSS property, `subscribe` could, similarly, indicate which logs to log the event to.

```css
.cls1:has(> [key1='value1']) { subscribe: log1 log2; }
```

As described in [Objects and Iterators with Style](/Notes/Objects%20and%20Iteration%20with%20Style.md), multiple values for a property could be aggregated from multiple declarations.

```css
.cls1:has(> [key1='value1']) { ^*subscribe: yield(log1) yield(log2); }
.cls2 { ^*subscribe: yield(log3); }
```

## Event Streams

Syntax could be explored with which to enable expressiveness to select events and patterns thereof as occurring in event streams.

## Selected Previous Works
* [DOM Events](https://dom.spec.whatwg.org/#events)
* [XES](https://xes-standard.org/)
* [OCEL](https://www.ocel-standard.org/)
* [xAPI](https://xapi.com/)
* [Caliper](https://www.imsglobal.org/activity/caliper)
