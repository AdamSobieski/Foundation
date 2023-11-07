## Introduction

What if software system events could be selected using CSS-based selectors, e.g., for logging purposes?

With this, software systems would be able to load CSS-based configuration files indicating those events to log or to otherwise process.

## Representing Events

A number of non-mutually-exclusive options for representing events can be considered:

1. Events could implement [`Event`](https://dom.spec.whatwg.org/#interface-event).
2. Events could implement [`DocumentFragment`](https://dom.spec.whatwg.org/#interface-documentfragment).
3. Events could implement [`boolean matches(DOMString selectors)`](https://dom.spec.whatwg.org/#dom-element-matches).
4. Other

Events could each have one or more classes. This might resemble the [publish-subscribe pattern](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern). In markup, this might resemble:

```xml
<event class="cls1 cls2" />
```

Events could have attributes. In markup, this might resemble:

```xml
<event class="cls1 cls2" attr="value" />
```

Events could be raised or dispatched with argument objects. These argument objects could be child elements of the events in a virtual DOM structure. In markup, this might resemble:

```xml
<event class="cls1 cls2">
  <argument key1="value1" key2="value2" />
</event>
```

Types of events could be represented in a virtual DOM structure via elements' names. In markup, this might resemble:

```xml
<html:progressevent class="cls1 cls2" xmlns:html="http://www.w3.org/1999/xhtml">
  <argument key1="value1" key2="value2" />
</html:progressevent>
```

## Selecting Events

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

Using element names to distinguish types of events would allow CSS-based selectors like:

```css
@namespace html url(http://www.w3.org/1999/xhtml);

html|* { ^*subscribe: yield(log4); }
```

## Event Streams

Syntax could be explored with which to enable expressiveness to select events and patterns thereof as occurring in event streams.

## Selected Previous Works
* [DOM Events](https://dom.spec.whatwg.org/#events)
* [XES](https://xes-standard.org/)
* [OCEL](https://www.ocel-standard.org/)
* [xAPI](https://xapi.com/)
* [Caliper](https://www.imsglobal.org/activity/caliper)
