## Fallbacks, Proxies, Replacements, Substitutes, and Surrogates

What if DOM elements could provide fallback, proxy, replacement, substitute, or surrogate elements for themselves?

```webidl
partial interface Element
{
  Element? getProxy(DOMString type, optional object options);

  readonly property boolean isProxy;
  readonly attribute DOMString? proxyType;
  readonly attribute object? proxyOptions;
  readonly property Element? origin;
}
```

### Accessibility

The following example shows how an _accessibility surrogate_ could be obtained.

```js
var x1 = element.getProxy('wai-aria');
```

Accessibility surrogates for HTML elements and for (nestable) [custom elements](https://html.spec.whatwg.org/multipage/custom-elements.html) could be comprised of HTML elements decorated with ARIA attributes or could be comprised of _ARIA elements_.

For example, a nested custom element resembling:
```xml
<custom-widget>
  <custom-button>Click here</custom-button>
</custom-widget>
```

could provide an HTML-based accessibility surrogate resembling:

```xml
<div class="accessibility-surrogate">
  <button aria-details="info-note">Click here</button>
  <div role="note" id="info-note">
    <p>Please visit our <a href="...">accessibility page</a> for more information.</p>
  </div>
</div>
```

or, alternatively, could provide an ARIA-elements-based accessibility surrogate resembling:

```xml
<aria:input aria:role="button" xhtml:onclick="...">
  <aria:label>
    <aria:alt>
      <aria:data aria:type="text/plain">Click here</aria:data>
      <aria:data aria:type="application/xhtml+xml" aria:media="(prefers-contrast: more)">
        <xhtml:span class="high-contrast">Click here</xhtml:span>
      </aria:data>
      <aria:data aria:type="application/ssml+xml">
        <ssml:speak>
          <ssml:phoneme ssml:alphabet="ipa" ssml:ph="klɪk">Click</ssml:phoneme>
          <ssml:phoneme ssml:alphabet="ipa" ssml:ph="hir">here</ssml:phoneme>
        </ssml:speak>
      </aria:data>
      <aria:data aria:type="application/braille">⠠⠉⠇⠊⠉⠅ ⠓⠑⠗⠑</aria:data>
    </aria:alt>
  </aria:label>
  <aria:details>
    <aria:note aria:type="application/xhtml+xml">
      Please visit our <xhtml:a href="...">accessibility page</xhtml:a> for more information.
    </aria:note>
  </aria:details>
</aria:input>
```

[Accessibility trees](https://w3c.github.io/aria/#dfn-accessibility-tree) and HTML document trees are already "parallel structures". ARIA elements could be "parallel structures" intended for consumption by [assistive technologies](https://w3c.github.io/aria/#dfn-assistive-technologies).

### Internationalization

Using a generic proxy name like `content`, one could use an options object for internationalization scenarios:

```js
var x2 = element.getProxy('content', {
  accept-language: 'en;q=0.8, de;q=0.7, fr;q=0.6, *;q=0.5'
});
```

### Content Negotiation

Using existing HTTP content-negotiation concepts, that options object could more fully resemble:

```js
var x3 = element.getProxy('content', {
  accept: 'text/html, application/xhtml+xml, application/xml;q=0.9, */*;q=0.8',
  accept-language: 'en;q=0.8, de;q=0.7, fr;q=0.6, *;q=0.5'
});
```

## Brainstorming with Respect to Implementation

### Attributes with One or More Element Values

What if elements could have both strings and one or more other elements for the values of their attributes?

Sketching this in WebIDL, ensuring backwards compatibility, new methods for tree-based attributes could be added.

```webidl
partial interface Element
{
  NodeList getAttributeElements(DOMString qualifiedName);
  NodeList getAttributeElementsNS(DOMString? namespace, DOMString localName);
  [CEReactions] undefined setAttributeElements(DOMString qualifiedName, NodeList value);
  [CEReactions] undefined setAttributeElementsNS(DOMString? namespace, DOMString qualifiedName, NodeList value);
  ...
}
```

or

```webidl
partial interface Element
{
  HTMLCollection getAttributeElements(DOMString qualifiedName);
  HTMLCollection getAttributeElementsNS(DOMString? namespace, DOMString localName);
  [CEReactions] undefined setAttributeElements(DOMString qualifiedName, HTMLCollection value);
  [CEReactions] undefined setAttributeElementsNS(DOMString? namespace, DOMString qualifiedName, HTMLCollection value);
  ...
}
```

What might a corresponding XML-based serialization resemble?

**Option 1**: A special attribute, `xml:parseType`, could enable serialization.

```xml
<ns:element ns:text-attr="text">
  <ns:tree-attr xml:parseType="attribute">
    <!-- the element(s) here would be the value of the tree-based attribute -->
  </ns:tree-attr>
</ns:element>
```

**Option 2**: A special child element, `xml:attributes`, could also enable serialization.

```xml
<ns:element ns:text-attr="text">
  <xml:attributes>
    <ns:tree-attr>
      <!-- the element(s) here would be the value of the tree-based attribute -->
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

### Metadata

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

### Custom Elements

How might developers customize and implement `getProxy()` for custom elements, in particular with respect to accessibility, internationalization, and content negotiation scenarios?

The following example (from [the HTML spec](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements-accessibility-example)) shows the state of the art with respect to custom elements and accessibility:

```js
class MyCheckbox extends HTMLElement {
  static formAssociated = true;
  static observedAttributes = ['checked'];

  constructor() {
    super();
    this._internals = this.attachInternals();
    this.addEventListener('click', this._onClick.bind(this));

    this._internals.role = 'checkbox';
    this._internals.ariaChecked = 'false';
  }

  get form() { return this._internals.form; }
  get name() { return this.getAttribute('name'); }
  get type() { return this.localName; }

  get checked() { return this.hasAttribute('checked'); }
  set checked(flag) { this.toggleAttribute('checked', Boolean(flag)); }

  attributeChangedCallback(name, oldValue, newValue) {
    // name will always be "checked" due to observedAttributes
    this._internals.setFormValue(this.checked ? 'on' : null);
    this._internals.ariaChecked = this.checked;
  }

  _onClick(event) {
    this.checked = !this.checked;
  }
}

customElements.define('my-checkbox', MyCheckbox);
```
