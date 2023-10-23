## Introduction

An approach is described here for selecting nodes and edges in graphs for purposes of styling.

Let us consider an alternating node and edge pseudo-class-like syntax. For examples:
```css
:node(...):edge(...) { property: value; }
```
or
```css
:edge(...):node(...) { property: value; }
```

The contents in the parentheses, above, are to be drawn from a subset of the CSS selector syntax.

The following example intends to clarify:
```css
:node([attr="value"]):edge(*):node(.has-selection) { color: blue; }
```

It appears that this syntax matches entire paths of nodes and edges and not single nodes or edges to apply styling to.

A solution, in these regards, involves utilization of a question-mark.

```css
:?node([attr="value"]):edge(*):node(.has-selection) { color: blue; }
:node([attr="value"]):?edge(*):node(.has-selection) { color: blue; }
:node([attr="value"]):edge(*):?node(.has-selection) { color: blue; }
```

Above, all three selectors match the same set of paths and the question-mark symbol, limited to one per path, indicates which thing, which node or edge, to select for styling.

## Logical Operations

Logical operators, `:not()`, `:and()`, and `:or()`, can be utilized.

```css
:node([attr="value"]):edge(*):or(:node(.txt-sel):?edge(.rt-clk), :node(.img-sel):?edge(.rt-clk)):node(.context-menu)
{
  color: blue;
}
```

## Repetition

`:repeat(min, max, pattern)` could be a shorthand notation for describing repetition.

```css
:node([attr="value"]):repeat(0, 9, :edge(.key-press):node(*)):edge(.key-press):?node(*)
{
  color: blue;
}
```

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

:node([rdf|about="http://www.w3.org/TR/rdf-syntax-grammar"]):edge(ex|editor):node(*):edge(ex|fullName):?node(*)
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

## A Work In Progress
This selector syntax is a work in progress. Techniques for providing a fuller portion of SPARQL's expressiveness are being explored.

### Alternate Syntaxes
Alternate syntaxes are under consideration including ones utilizing the `>` combinator:

```css
@namespace rdf url(http://www.w3.org/1999/02/22-rdf-syntax-ns#)
@namespace ex  url(http://example.org/stuff/1.0/)

node([rdf|about="http://www.w3.org/TR/rdf-syntax-grammar"]) > edge(ex|editor) > node(*) > edge(ex|fullName) > ?node(*)
{
   color: blue;
}
```

Towards providing a fuller portion of SPARQL's expressiveness with a CSS-based selector syntax, a possiblity is shown:

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

which would be intended to map to a SPARQL query:

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

## Selected Previous Works
* [CSS Selectors](https://www.w3.org/TR/selectors-4/)
* [Fresnel Selector Language for RDF](https://www.w3.org/2005/04/fresnel-info/fsl/)
* [Graph Stylesheets](https://www.w3.org/2001/11/IsaViz/gss/gssmanual.html)
* [SPARQL](https://www.w3.org/TR/sparql11-query/)
