## Document Object Model Ideas

### Elements with Proxies, Fallbacks, Replacements, or Substitutes and Accessibility

What if DOM elements could provide proxy, fallback, replacement, or substitute elements for themselves for scenarios such as providing shadow trees or _accessibility surrogates_?

```webidl
partial interface Element
{
  Element? getProxy(DOMString name, optional object options);
  Element? getProxyNS(DOMString? namespace, DOMString name, optional object options);
  ...
}
```

With such methods on elements, developers would be able to simply query arbitrary elements to see if they have proxy, fallback, replacement, or substitute elements for indicated scenarios.

```js
var shadow_dom = element.getProxy('shadow');
var wai_aria = element.getProxy('wai-aria');
```

Such a function could be useful for internationalization scenarios. Using a vanilla proxy type descriptor like `content`, one could provide an options object indicating the desired language:

```js
var proxy = element.getProxy('content', { lang: 'en' });
```

Using existing HTTP content negotiation concepts, the objects might, instead, resemble:

```js
var proxy = element.getProxy('content', {
  accept: 'text/html, application/xhtml+xml, application/xml;q=0.9, */*;q=0.8',
  accept-language: 'en;q=0.8, de;q=0.7, fr;q=0.6, *;q=0.5`
});
```

### Element Values for Attributes

What if DOM elements could have either text strings or elements as the values of their attributes? While easy to model in WebIDL, what might XML-based serializations resemble?

**Option 1**: A special attribute, `xml:parseType`, could enable serialization.

```xml
<ns:element ns:text-attr="text">
  <ns:tree-attr xml:parseType="attribute">
    <!-- this would be the content of a tree-based attribute -->
  </ns:tree-attr>
</ns:element>
```

**Option 2**: A special child element, `xml:attributes`, could also enable serialization.

```xml
<ns:element ns:text-attr="text">
  <xml:attributes>
    <ns:tree-attr>
      <!-- this would be the content of a tree-based attribute -->
    </ns:tree-attr>
  </xml:attributes>
</ns:element>
```

### Content Negotiation and Internationalization

What if element values for attributes could be wrapped in a well-known content-negotiation structure, e.g., `xml:alt` and `xml:data`, so that content could be obtained for different content types and languages?

**Option 1**: Using a special-attribute technique:

```xml
<ns:element ns:text-attr="text">
  <ns:tree-attr xml:parseType="attribute">
    <xml:alt>
      <xml:data xml:type="text/plain" xml:lang="en">...</xml:data>
      <xml:data xml:type="text/plain" xml:lang="fr">...</xml:data>
      <xml:data xml:type="text/html" xml:lang="en">...</xml:data>
      <xml:data xml:type="text/html" xml:lang="fr">...</xml:data>
    </xml:alt>
  </ns:tree-attr>
</ns:element>
```

**Option 2**: Using a special-child technique:

```xml
<ns:element ns:text-attr="text">
  <xml:attributes>
    <ns:tree-attr>
      <xml:alt>
        <xml:data xml:type="text/plain" xml:lang="en">...</xml:data>
        <xml:data xml:type="text/plain" xml:lang="fr">...</xml:data>
        <xml:data xml:type="text/html" xml:lang="en">...</xml:data>
        <xml:data xml:type="text/html" xml:lang="fr">...</xml:data>
      </xml:alt>
    </xs:tree-attr>
  </xml:attributes>
</ns:element>
```

### Metadata on Elements

What if DOM elements could have metadata attached to them? While easy to model in WebIDL, what might XML-based serializations resemble?

**Option 1**: Using a special-attribute technique:

```xml
<ns:element id="el">
  <ns:metadata xml:parseType="attribute">
    <rdf:Description rdf:about="#id">
      <!-- this would be metadata about the element -->
    </rdf:Description>
  </ns:metadata>
</ns:element>
```

**Option 2**: Using a different special-attribute technique:

```xml
<ns:element id="el">
  <rdf:Description rdf:about="#id" xml:parseType="metadata">
    <!-- this would be metadata about the element -->
  </rdf:Description>
</ns:element>
```

**Option 3**: Using a special-child technique:

```xml
<ns:element id="el">
  <xml:attributes>
    <ns:metadata>
      <rdf:Description rdf:about="#id">
        <!-- this would be metadata about the element -->
      </rdf:Description>
    </ns:metadata>
  </xml:attributes>
</ns:element>
```

**Option 4**: Using a different special-child technique:

```xml
<ns:element id="el">
  <xml:metadata xml:type="application/rdf+xml">
    <rdf:Description rdf:about="#id">
      <!-- this would be metadata about the element -->
    </rdf:Description>
  </xml:metadata>
</ns:element>
```
