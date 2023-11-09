## Introduction

What if CSS selectors could be used to filter DOM events and HTML server-sent events?

By using CSS selectors, client-side event-filtering logic could: (1) route events to scripting functions, and (2) be transmitted to servers to enable server-side filtering.

Use cases include scenarios where software developers would want to provide users with dynamic client-side filtering and/or subscription to events and where they would want to be able to transmit instantaneous filtering criteria and logic, in this case relevant CSS selectors, to their servers to be able to subsequently filter events there. So doing can enable transmitting fewer events, and, potentially, other optimizations over sets of clients.

As CSS is modifiable at runtime via the [CSSOM](https://drafts.csswg.org/cssom/), both client-side and server-side event-stream filtering could be dynamic and responsive.

For example, let us envision a website which delivers real-time stock market data visualization. There are approximately 2,400 companies traded on the New York Stock Exchange and this is too much data to stream to each client for client-side filtering. As users select stocks of interest to them, CSS filters could be created describing events of interest, these selectors could be transmitted to the server, and users would subsequently receive only those described events, only those update events for the companies of interest to them.

## Discussion

The DOM interface for events is [`Event`](https://dom.spec.whatwg.org/#interface-event) and the HTML interface for server-sent events is [`EventSource`](https://html.spec.whatwg.org/multipage/server-sent-events.html#the-eventsource-interface).

Presently, Web developers are expected to use JavaScript to filter or select events based on events' types. Further processing could subsequently occur based on events' data. For examples:

```js
const sse = new EventSource("/api/v1/sse");

sse.addEventListener("notice", (e) => {
  console.log(e.data);
});

sse.addEventListener("update", (e) => {
  console.log(e.data);
});
```

At the WICG, there is also an [Observable API](https://github.com/WICG/observable) under development. Here is an example of that API:

```js
element.on('click')
  .filter(e => e.target.matches('.foo'))
  .map(e => ({x: e.clientX, y: e.clientY }))
  .subscribe({next: handleClickAtPoint});
```

Software libraries for [reactive programming](https://en.wikipedia.org/wiki/Reactive_programming) and [event stream processing](https://en.wikipedia.org/wiki/Stream_processing) are myriad; some are listed [here](https://github.com/WICG/observable#userland-libraries).

In .NET, there is an interface [IQbservable&lt;T&gt;](https://learn.microsoft.com/en-us/previous-versions/dotnet/reactive-extensions/hh229328(v=vs.103)) which enables client-side event-stream queries to be constructed in such a way that resultant queries can be processed server-side.

Event-stream querying languages include, but are not limited to: [Stream Analytics Query Language](https://learn.microsoft.com/en-us/stream-analytics-query/stream-analytics-query-language-reference), [StreamSQL](https://en.wikipedia.org/wiki/StreamSQL), [Kafka KSQL](https://www.confluent.io/blog/ksql-open-source-streaming-sql-for-apache-kafka/), [SQLStreams](http://sqlstream.com/), [SamzaSQL](https://ieeexplore.ieee.org/document/7530060/), and [Storm SQL](http://storm.apache.org/releases/2.1.0/storm-sql.html).

## Representing Events

With respect to representing events, a number of non-mutually-exclusive options can be considered:

1. Events implement [`Event`](https://dom.spec.whatwg.org/#interface-event).
2. Events implement [`DocumentFragment`](https://dom.spec.whatwg.org/#interface-documentfragment).
3. Events implement [`boolean matches(DOMString selectors)`](https://dom.spec.whatwg.org/#dom-element-matches).
4. Other

Types of events could be identified by URI's, having both a namespace URI and a local name. Events could have attributes. Events could have classes or categories, resembling the [publish-subscribe pattern](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern). Events could have arguments or data. In markup, these features, all together, might resemble:

```xml
<html:progressevent class="cls1 cls2" xmlns:html="http://www.w3.org/1999/xhtml">
  <data key1="value1" key2="value2" />
</html:progressevent>
```

With such an XML-based model of events, CSS-based selectors can be utilized.

## Selecting Events

A special-purpose CSS property, `subscribe`, could be used for expressing whether a client wants to subscribe to a selected event.

```css
.cls1:has(> [key1='value1']) { subscribe: true; }
```

Alternatively, this special-purpose property could be multi-valued and utilized to indicate which event processors or JavaScript functions to route selected events to:

```css
.cls1:has(> [key1='value1']) { subscribe: function1 function2; }
```

As described in [Objects and Iterators with Style](/Notes/Objects%20and%20Iteration%20with%20Style.md), multiple values for a property could be aggregated from multiple declarations.

```css
.cls1:has(> [key1='value1']) { ^*subscribe: yield(function1) yield(function2); }
.cls2 { ^*subscribe: yield(function3); }
```

Using element names to distinguish types of events would allow CSS-based selectors like:

```css
@namespace html url(http://www.w3.org/1999/xhtml);

html|* { ^*subscribe: yield(function4); }
```

## Event Streams

CSS-based selector syntax possibilities could be explored with which to select events based on patterns occurring in event streams.

## Selected Previous Works
* [DOM Events](https://dom.spec.whatwg.org/#events)
* [Server-sent Events](https://html.spec.whatwg.org/multipage/server-sent-events.html)
* [XES](https://xes-standard.org/)
* [OCEL](https://www.ocel-standard.org/)
* [xAPI](https://xapi.com/)
* [Caliper](https://www.imsglobal.org/activity/caliper)
