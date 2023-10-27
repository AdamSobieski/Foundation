## Document Object Model Ideas

### Elements with Proxy, Fallback, Replacement, or Substitute Elements and Accessibility

What if DOM elements could provide proxy, fallback, replacement, or substitute elements for themselves for scenarios such as providing shadow trees or _accessibility surrogates_?

```webidl
partial interface Element
{
  Element? getProxy(DOMString name, optional object context);
  Element? getProxyNS(DOMString? namespace, DOMString name, optional object context);
  ...
}
```

With such methods on elements, developers would be able to simply query arbitrary elements to see if they have proxy, fallback, replacement, or substitute elements for indicated scenarios.

```js
var shadow_dom = element.getProxy('shadow');
var wai_aria = element.getProxy('wai-aria');
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

What if element values for attributes could be wrapped in a well-known content-negotiation structure, e.g., `ext:alt` so that content could be obtained for different content types and languages?

**Option 1**: Using the special-attribute technique:

```xml
<ns:element ns:text-attr="text">
  <ns:tree-attr xml:parseType="attribute">
    <ext:alt>
      <ext:data ext:type="text/plain" ext:lang="en">...</ext:data>
      <ext:data ext:type="text/plain" ext:lang="fr">...</ext:data>
      <ext:data ext:type="text/html" ext:lang="en">...</ext:data>
      <ext:data ext:type="text/html" ext:lang="fr">...</ext:data>
    </ext:alt>
  </ns:tree-attr>
</ns:element>
```

**Option 2**: Using the special-child technique:

```xml
<ns:element ns:text-attr="text">
  <xml:attributes>
    <ns:tree-attr>
      <ext:alt>
        <ext:data ext:type="text/plain" ext:lang="en">...</ext:data>
        <ext:data ext:type="text/plain" ext:lang="fr">...</ext:data>
        <ext:data ext:type="text/html" ext:lang="en">...</ext:data>
        <ext:data ext:type="text/html" ext:lang="fr">...</ext:data>
      </ext:alt>
    </xs:tree-attr>
  </xml:attributes>
</ns:element>
```

### Metadata on Elements

What if DOM elements could have metadata attached to them? While easy to model in WebIDL, what might XML-based serializations resemble?

**Option 1**: Using the special-attribute technique:

```xml
<ns:element id="el">
  <ns:metadata xml:parseType="attribute">
    <rdf:Description rdf:about="#id">
      <!-- this would be metadata about the element -->
    </rdf:Description>
  </ns:metadata>
</ns:element>
```

**Option 2**: Using the special-attribute technique in a different manner:

```xml
<ns:element id="el">
  <rdf:Description rdf:about="#id" xml:parseType="metadata">
    <!-- this would be metadata about the element -->
  </rdf:Description>
</ns:element>
```

**Option 3**: Using the special-child technique:

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

**Option 4**: Using the special-child technique in a different manner:

```xml
<ns:element id="el">
  <xml:metadata xml:type="application/rdf+xml">
    <rdf:Description rdf:about="#id">
      <!-- this would be metadata about the element -->
    </rdf:Description>
  </xml:metadata>
</ns:element>
```
