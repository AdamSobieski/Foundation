## Fallbacks, Proxies, Replacements, Substitutes, or Surrogates

What if DOM elements could provide fallback, proxy, replacement, substitute, or surrogate elements for themselves?

```webidl
partial interface Element
{
  Element? getProxy(DOMString name, optional object options);
  Element? getProxyNS(DOMString? namespace, DOMString name, optional object options);
  ...
}
```

With such methods on the `Element` interface, developers would be able to query arbitrary elements to see whether they have fallback, proxy, replacement, substitute, or surrogate elements for various scenarios.

### Accessibility

The following example shows how an _accessibility surrogate_ could be obtained, e.g., from a custom element.

```js
var x1 = element.getProxy('wai-aria');
```

### Internationalization

Using a vanilla proxy name like `content`, one could use an options object for internationalization scenarios:

```js
var x2 = element.getProxy('content', {
  accept-language: 'en;q=0.8, de;q=0.7, fr;q=0.6, *;q=0.5'
});
```

### Content Negotiation

Using existing HTTP content negotiation concepts, that options object could more fully resemble:

```js
var x3 = element.getProxy('content', {
  accept: 'text/html, application/xhtml+xml, application/xml;q=0.9, */*;q=0.8',
  accept-language: 'en;q=0.8, de;q=0.7, fr;q=0.6, *;q=0.5'
});
```

## Brainstorming with Respect to Implementation

### Attributes with NodeList Values

What if elements could have both strings and one or more other elements for the values of their attributes?

Sketching this in WebIDL, new methods for tree-based attributes could be added so as to maintain backwards compatibility with existing methods for using text-based attributes.

```webidl
partial interface Element
{
  NodeList getElementAttribute(DOMString qualifiedName);
  NodeList getElementAttributeNS(DOMString? namespace, DOMString localName);
  [CEReactions] undefined setElementAttribute(DOMString qualifiedName, NodeList value);
  [CEReactions] undefined setElementAttributeNS(DOMString? namespace, DOMString qualifiedName, NodeList value);
  ...
}
```

What might a corresponding XML-based serialization resemble?

**Option 1**: A special attribute, `xml:parseType`, could enable serialization.

```xml
<ns:element ns:text-attr="text">
  <ns:tree-attr xml:parseType="attribute">
    <!-- the element(s) here would be in the NodeList value for the tree-based attribute -->
  </ns:tree-attr>
</ns:element>
```

**Option 2**: A special child element, `xml:attributes`, could also enable serialization.

```xml
<ns:element ns:text-attr="text">
  <xml:attributes>
    <ns:tree-attr>
      <!-- the element(s) here would be in the NodeList value for the tree-based attribute -->
    </ns:tree-attr>
  </xml:attributes>
</ns:element>
```

### Content Negotiation

What if elements could be wrapped in a well-known content-negotiation structure, e.g., `xml:alt` and `xml:data`, so that contents could be provided for indicated content types and languages?

```xml
<ns:parent-element>
  <xml:alt>
    <xml:data xml:lang="en">
      <ns:child-element>Hello.</ns:child-element>
    </xml:data>
    <xml:data xml:lang="fr">
      <ns:child-element>Bonjour.</ns:child-element>
    </xml:data>
    <xml:data>
      <ns:child-element>The fallback content.</ns:child-element>
    </xml:data>
  </xml:alt>
</ns:parent-element>
```

What if attributes' values could be wrapped in a well-known content-negotiation structure, e.g., `xml:alt` and `xml:data`, so that contents could be provided for indicated content types and languages?

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

## Metadata

What if DOM elements could have metadata attached to them?

What might XML-based serializations resemble?

**Option 1**: Using a special-attribute technique:

```xml
<ns:element id="el">
  <ns:metadata xml:parseType="attribute">
    <rdf:Description rdf:about="#id">
      <!-- here would be metadata about the element -->
    </rdf:Description>
  </ns:metadata>
</ns:element>
```

**Option 2**: Using a special-child technique:

```xml
<ns:element id="el">
  <xml:attributes>
    <ns:metadata>
      <rdf:Description rdf:about="#id">
        <!-- here would be metadata about the element -->
      </rdf:Description>
    </ns:metadata>
  </xml:attributes>
</ns:element>
```

**Option 3**: Using a hybrid technique:

```xml
<ns:element id="el">
  <xml:metadata xml:parseType="attribute">
    <rdf:Description rdf:about="#id">
      <!-- here would be metadata about the element -->
    </rdf:Description>
  </xml:metadata>
</ns:element>
```
