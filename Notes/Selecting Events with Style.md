## Introduction

How can criteria for filtering event streams and related program logic be made portable between clients and servers?

By being able to transmit criteria for filtering event streams and related program logic between clients and servers, fewer events would need be to be transmitted in event streams.

## Discussion

Web developers often use JavaScript to filter DOM events and HTML server-sent events. For example:

```js
const sse = new EventSource("/api/v1/sse");

sse.addEventListener("notice", (e) => {
  console.log(e.data);
});

sse.addEventListener("update", (e) => {
  console.log(e.data);
});
```

At the WICG, there is also an [Observable API](https://github.com/WICG/observable) under development. Here is an API example:

```js
element.on('click')
  .filter(e => e.target.matches('.foo'))
  .map(e => ({x: e.clientX, y: e.clientY }))
  .subscribe({next: handleClickAtPoint});
```

The DOM interface for events is [`Event`](https://dom.spec.whatwg.org/#interface-event) and the HTML interface for server-sent events is [`EventSource`](https://html.spec.whatwg.org/multipage/server-sent-events.html#the-eventsource-interface).

Comparable models of events and event streams include [XES](https://xes-standard.org/), [OCEL](https://www.ocel-standard.org/), [xAPI](https://xapi.com/), and [Caliper](https://www.imsglobal.org/activity/caliper).

Software libraries for [reactive programming](https://en.wikipedia.org/wiki/Reactive_programming) and [event stream processing](https://en.wikipedia.org/wiki/Stream_processing) are myriad; some are listed [here](https://github.com/WICG/observable#userland-libraries).

In .NET, there is an interface [IQbservable&lt;T&gt;](https://learn.microsoft.com/en-us/previous-versions/dotnet/reactive-extensions/hh229328(v=vs.103)) which enables client-side event-stream queries to be constructed in such a way that resultant queries can be processed server-side.

Event-stream querying languages include, but are not limited to: [Stream Analytics Query Language](https://learn.microsoft.com/en-us/stream-analytics-query/stream-analytics-query-language-reference), [StreamSQL](https://en.wikipedia.org/wiki/StreamSQL), [Kafka KSQL](https://www.confluent.io/blog/ksql-open-source-streaming-sql-for-apache-kafka/), [SQLStreams](http://sqlstream.com/), [SamzaSQL](https://ieeexplore.ieee.org/document/7530060/), and [Storm SQL](http://storm.apache.org/releases/2.1.0/storm-sql.html).

## Representing and Selecting Events

CSS is a Web Standard and Web developers are familiar with its syntax and semantics. Using CSS selectors, software developers could: (1) perform client-side or server-side event-stream filtering, and (2) transmit filtering criteria and related program logic between clients and servers. As CSS is modifiable at runtime via the [CSSOM](https://drafts.csswg.org/cssom/), event-stream filtering could be dynamic and responsive.

With respect to representing events, a number of non-mutually-exclusive options can be considered. Events could implement:

1. [`Event`](https://dom.spec.whatwg.org/#interface-event).
2. [`DocumentFragment`](https://dom.spec.whatwg.org/#interface-documentfragment).
3. [`boolean matches(DOMString selectors)`](https://dom.spec.whatwg.org/#dom-element-matches).
4. another interface.

Types of events could be identified by URI's, having both a namespace URI and a local name. Events could have attributes. Events could have classes or categories, resembling the [publish-subscribe pattern](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern). Events could have arguments or data. In markup, these features, all together, might resemble:

```xml
<html:progressevent class="cls1 cls2" xmlns:html="http://www.w3.org/1999/xhtml">
  <data key1="value1" key2="value2" />
</html:progressevent>
```

With such an XML-based model of events, CSS-based selectors can be utilized.

A special-purpose CSS property, `process`, could be used for expressing whether a client wants to subscribe to a selected event.

```css
.cls1:has(> [key1='value1']) { process: true; }
```

Alternatively, this special-purpose property could be multi-valued and utilized to indicate which event processors or JavaScript functions to route selected events to:

```css
.cls1:has(> [key1='value1']) { process: function1 function2; }
```

For a concrete example, let us imagine a website which delivers real-time stock market data for visualization. There are roughly 2,400 companies traded on the New York Stock Exchange and there is far too much data to stream every update to every client for subsequent client-side filtering. As users dynamically select the stocks of interest to them, CSS filters could be created which describe the interesting events. These event selectors could be transmitted to servers so that users would need only receive those events interesting to them, the update events for those companies of interest to them.

```xml
<nyse:update xmlns:nyse="...">
  <data company="ABCD" value="12.34" time="12:34:56.78" />
</nyse:update>
```

and a corresponding CSS selector to select incoming updates for company `ABCD` might resemble:

```css
nyse|update:has(> [company='ABCD']) { process: onupdate; }
```

The text for the CSS selector `nyse|update:has(> [company='ABCD'])` could be sent to the server, alongside other selectors, to indicate which events to send to the client, which companies' stock market data that the user wanted to instantaneously visualize.

## Event Streams

CSS-based selector syntax possibilities could be explored with which to select events based on patterns occurring in event streams.

## Selected Previous Works
* [DOM Events](https://dom.spec.whatwg.org/#events)
* [Server-sent Events](https://html.spec.whatwg.org/multipage/server-sent-events.html)
* [XES](https://xes-standard.org/)
* [OCEL](https://www.ocel-standard.org/)
* [xAPI](https://xapi.com/)
* [Caliper](https://www.imsglobal.org/activity/caliper)
