## Document Object Model Ideas

### Elements with Proxy, Fallback, Replacement, or Substitute Elements

What if XML DOM elements could provide proxy, fallback, replacement, or substitute elements for themselves for scenarios such as shadow DOM or accessibility?

```webidl
partial interface Element
{
  Element? getProxy(DOMString name, optional object context);
  Element? getProxyNS(DOMString? namespace, DOMString name, optional object context);
  ...
}
```

With such methods on elements, JavaScript developers would be able to simply query arbitrary document elements to see if they have proxy, fallback, replacement, or substitute elements for indicated scenarios.

```js
var shadow_dom = element.getProxy('shadow');
var wai_aria = element.getProxy('wai-aria');
```

### Element Values for Attributes

What if XML DOM elements could have either text strings or elements as the values of their attributes? While easy to model in WebIDL, what might XML-based serializations resemble?

**Option 1**: A special attribute, `xml:parseType`, could enable serialization.

```xml
<ns:element ns:attr1="text">
  <ns:attr2 xml:parseType="attribute">
    <!-- this would be a tree-based attribute -->
  </ns:attr2>
</ns:element>
```

**Option 2**: A special child element, `xml:attributes`, could also enable serialization.

```xml
<ns:element ns:attr1="text">
  <xml:attributes>
    <ns:attr2>
      <!-- this would be a tree-based attribute -->
    </ns:attr2>
  </xml:attributes>
</ns:element>
```

### Metadata on Elements

What if XML DOM elements could have metadata attached to them? While easy to model in WebIDL, what might XML-based serializations resemble?

**Option 1**: Using the special-attribute technique:

```xml
<ns:element id="el">
  <rdf:Description rdf:about="#id" xml:parseType="attribute">
    <!-- this would be metadata about the element -->
  </rdf:Description>
</ns:element>
```

**Option 2**: Also using the special-attribute technique:

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
    <rdf:Description rdf:about="#id">
      <!-- this would be metadata about the element -->
    </rdf:Description>
  </xml:attributes>
</ns:element>
```

**Option 4**: Also using the special-child technique:

```xml
<ns:element id="el">
  <xml:metadata xml:type="application/rdf+xml">
    <rdf:Description rdf:about="#id">
      <!-- this would be metadata about the element -->
    </rdf:Description>
  </xml:metadata>
</ns:element>
```
