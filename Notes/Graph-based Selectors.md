## Introduction

A new syntax is described here for selecting nodes and edges in graphs for purposes of styling.

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

### Datasets

Datasets may contain multiple graphs. The following examples show how graph-based selection can be expressed. The descendent combinator, a blank space, is used between selected graphs and their descendent nodes or edges.

```css
graph(...) node(...) > edge(...) > node(...) { property: value; }
```
```css
graph(...) edge(...) > node(...) > edge(...) { property: value; }
```

The following example makes concrete the parenthesized CSS-based selectors:

```css
graph(#id123) node([attr="value"]) > edge(*) > node(.has-selection) { color: blue; }
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

Let us expand the path syntax by adding a question-mark with which to indicate which component to select.

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

A `:as(--variable-name)` syntax can be used to bind graphs, nodes, and edges to named variable instances.

## The Semantic Web

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

Here is another example:

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

which would map to a SPARQL query:

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

Here is a more complex SPARQL query which involves containing graphs:

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

This possibly could be expressed more succinctly:

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

## Selected Previous Works
* [CSS Selectors](https://www.w3.org/TR/selectors-4/)
* [Fresnel Selector Language for RDF](https://www.w3.org/2005/04/fresnel-info/fsl/)
* [Graph Stylesheets](https://www.w3.org/2001/11/IsaViz/gss/gssmanual.html)
* [SPARQL](https://www.w3.org/TR/sparql12-query/)
