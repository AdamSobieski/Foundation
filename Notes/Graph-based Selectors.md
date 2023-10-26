## Introduction

A new language inspired by CSS and SPARQL is described for selecting graphs, nodes, and edges.

### Use Cases

Use cases for this language include:

1. Visually styling displayed graphs, nodes, and edges.
2. Adding properties and values to graphs, nodes, and edges, e.g., to state machines, their states, and their transitions.
3. Logical rule-based systems.

### Path Syntax

Let us consider paths of alternating nodes and edges. For examples:

```css
node(...) > edge(...) > node(...) { property: value; }
```
```css
edge(...) > node(...) > edge(...) { property: value; }
```

The contents in the parentheses, above, are to be drawn from a subset of the CSS selector syntax as the following example intends to clarify:
```css
node([attr="value"]) > edge(*) > node(.has-selection) { color: blue; }
```

### Datasets with Multiple Graphs

Datasets may contain multiple graphs. The following examples show how selection can be expressed for these scenarios. The descendent combinator, a blank space, is used between selected graphs and their descendent nodes or edges.

```css
graph(...) node(...) > edge(...) > node(...) { property: value; }
```
```css
graph(...) edge(...) > node(...) > edge(...) { property: value; }
```

The following example makes concrete the parenthesized CSS-based selectors:

```css
graph(#id-123) node([attr="value"]) > edge(*) > node(.has-selection) { color: blue; }
```

The following example shows how one would express a selection from a named graph:

```css
@namespace rdf url(http://www.w3.org/1999/02/22-rdf-syntax-ns#)

graph([rdf|about="http://example.org/stuff/1.0/graph"]) node([attr="value"]) > edge(*) > node(.has-selection)
{
  color: blue;
}
```

### Selection

Let us expand the path syntax by utilizing a question-mark to indicate which component to select.

```css
?node([attr="value"]) > edge(*) > node(.has-selection) { color: blue; }
node([attr="value"]) > ?edge(*) > node(.has-selection) { color: blue; }
node([attr="value"]) > edge(*) > ?node(.has-selection) { color: blue; }
```

### Logical Operations

Logical operators, `not()`, `and()`, and `or()`, can be utilized.

```css
node([attr="value"]) > edge(*) > or(node(.txt-sel) > ?edge(.rt-clk), node(.img-sel) > ?edge(.rt-clk)) > node(.context-menu)
{
  color: blue;
}
```

### Repetition

`repeat(min, max, pattern)` can be a shorthand notation for describing a disjunction between a path repeated a number of times.

```css
node([attr="value"]) > repeat(0, 9, edge(.key-press) > node(*)) > edge(.key-press) > ?node(*)
{
  color: blue;
}
```

### Binding

The `:as(--variable-name)` syntax can be used to bind graphs, nodes, and edges to named variable instances.

## The Semantic Web

### RDF/XML

Towards providing the expressiveness to select and style both nodes and edges from RDF graphs, the following example select and styles from RDF/XML markup.

```rdf
<rdf:Description rdf:about="http://www.w3.org/TR/rdf-syntax-grammar"
    xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
    xmlns:dc="http://purl.org/dc/elements/1.1/"
    xmlns:ex="http://example.org/stuff/1.0/">
  <ex:editor>
    <rdf:Description>
      <ex:homePage>
        <rdf:Description rdf:about="http://purl.org/net/dajobe/" />
      </ex:homePage>
      <ex:fullName>Dave Beckett</ex:fullName>
    </rdf:Description>
  </ex:editor>
  <dc:title>RDF 1.1 XML Syntax</dc:title>
</rdf:Description>
```

Using the syntax under discussion, one could select one or more nodes and style them:

```css
@namespace rdf url(http://www.w3.org/1999/02/22-rdf-syntax-ns#)
@namespace ex  url(http://example.org/stuff/1.0/)

node([rdf|about="http://www.w3.org/TR/rdf-syntax-grammar"]) > edge(ex|editor) > node(*) > edge(ex|fullName) > ?node(*)
{
   color: blue;
}
```

Here is a mapping from that selector to a SPARQL query:

```sparql
PREFIX ex: <http://example.org/stuff/1.0/>
SELECT ?y
WHERE
{
  <http://www.w3.org/TR/rdf-syntax-grammar> ex:editor ?x .
  ?x ex:fullName ?y .
}
```

### SPARQL

Here is a SPARQL query which will be mapped to a selector in the new syntax.

```sparql
PREFIX ex: <http://example.org/stuff/1.0/>
SELECT ?y
WHERE
{
  ?x ex:p1 123 .
  ?x ex:p2 456 .
  ?x ex:p3 ?y .
}
```

```css
@namespace rdf url(http://www.w3.org/1999/02/22-rdf-syntax-ns#)
@namespace ex  url(http://example.org/stuff/1.0/)

and(
  node(*):as(--x) > edge(ex|p1) > node([rdf|value=123]),
  node(*):as(--x) > edge(ex|p2) > node([rdf|value=456]),
  node(*):as(--x) > edge(ex|p3) > ?node(*)
)
{
  color: blue;
}
```

Here is a more complex SPARQL query which involves multiple graphs:

```sparql
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
SELECT DISTINCT ?person
WHERE {
    ?person foaf:name ?name .
    GRAPH ?g1 { ?person a foaf:Person }
    GRAPH ?g2 { ?person a foaf:Person }
    GRAPH ?g3 { ?person a foaf:Person }
    FILTER(?g1 != ?g2 && ?g1 != ?g3 && ?g2 != ?g3) .
}  
```

This could be expressed utilizing the new selector syntax:

```css
@namespace rdf url(http://www.w3.org/1999/02/22-rdf-syntax-ns#)
@namespace foaf url(http://xmlns.com/foaf/0.1/)

and(
  graph(*):as(--g1) ?node(*):as(--person) > edge(rdf|type) > node(foaf|Person),
  graph(*):as(--g2) ?node(*):as(--person) > edge(rdf|type) > node(foaf|Person),
  graph(*):as(--g3) ?node(*):as(--person) > edge(rdf|type) > node(foaf|Person)
):filter(--g1 != --g2):filter(--g1 != --g3):filter(--g2 != --g3)
{
  color: blue;
}
```

Or, more succinctly:

```css
@namespace rdf url(http://www.w3.org/1999/02/22-rdf-syntax-ns#)
@namespace foaf url(http://xmlns.com/foaf/0.1/)

and(
  graph(*):as(--g1) ?node(foaf|Person):as(--person),
  graph(*):as(--g2) ?node(foaf|Person):as(--person),
  graph(*):as(--g3) ?node(foaf|Person):as(--person)
):filter(--g1 != --g2):filter(--g1 != --g3):filter(--g2 != --g3)
{
  color: blue;
}
```

## Logical Rules

Some logical rules can be expressed in the new language.

```xml
<ruleml:imp> 
  <ruleml:_rlab ruleml:href="#example2"/>
  <ruleml:_body> 
    <swrlx:individualPropertyAtom  swrlx:property="hasParent"> 
      <ruleml:var>x1</ruleml:var>
      <ruleml:var>x2</ruleml:var>
    </swrlx:individualPropertyAtom> 
    <swrlx:individualPropertyAtom  swrlx:property="hasSibling"> 
      <ruleml:var>x2</ruleml:var>
      <ruleml:var>x3</ruleml:var>
    </swrlx:individualPropertyAtom> 
    <swrlx:individualPropertyAtom  swrlx:property="hasSex"> 
      <ruleml:var>x3</ruleml:var>
      <owlx:Individual owlx:name="#female" />
    </swrlx:individualPropertyAtom> 
  </ruleml:_body> 
  <ruleml:_head> 
    <swrlx:individualPropertyAtom  swrlx:property="hasAunt"> 
      <ruleml:var>x1</ruleml:var>
      <ruleml:var>x3</ruleml:var>
    </swrlx:individualPropertyAtom> 
  </ruleml:_head> 
</ruleml:imp>
```
```css
and(
  ?node(*):as(--x1) > edge(hasParent) > node(*):as(--x2),
  node(*):as(--x2) > edge(hasSibling) > node(*):as(--x3),
  node(*):as(--x3) > edge(hasSex) > node(#female)
)
{
  hasAunt: var(--x3);
}
```

CSS-based notations are being explored [here](/Notes/Objects%20and%20Iteration%20with%20Style.md) for expressing object-based property values and sets and iterables for properties' values.

```css
and(
  ?node(*):as(--x1) > edge(hasParent) > node(*):as(--x2),
  node(*):as(--x2) > edge(hasSibling) > node(*):as(--x3),
  node(*):as(--x3) > edge(hasSex) > node(#female)
)
{
  *hasAunt: yield(var(--x3));
}
```

Or, more succinctly:

```css
?node(*) > edge(hasParent) > node(*) > edge(hasSibling) > node(*):as(--x) > edge(hasSex) > node(#female)
{
  *hasAunt: yield(var(--x));
}
```

## Selected Previous Works
* [CSS Selectors](https://www.w3.org/TR/selectors-4/)
* [Fresnel Selector Language for RDF](https://www.w3.org/2005/04/fresnel-info/fsl/)
* [Graph Stylesheets](https://www.w3.org/2001/11/IsaViz/gss/gssmanual.html)
* [RDF/XML](https://www.w3.org/TR/rdf12-xml/)
* [RDF-star](https://w3c.github.io/rdf-star/cg-spec/editors_draft.html)
* [RuleML](https://www.w3.org/submissions/FOL-RuleML/)
* [SPARQL](https://www.w3.org/TR/sparql12-query/)
* [SPARQL-star](https://w3c.github.io/rdf-star/cg-spec/editors_draft.html)
* [SWRL](https://www.w3.org/submissions/SWRL/)
