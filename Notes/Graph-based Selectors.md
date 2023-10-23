## Introduction

An approach is described here for selecting nodes and edges in graphs for purposes of styling.

Let us consider an alternating node and edge pseudo-class-like syntax. For examples:
```
:node(...):edge(...) { property: value; }
```
or
```
:edge(...):node(...) { property: value; }
```

The contents in the parentheses, above, are to be drawn from a subset of the CSS selector syntax.

The following example intends to clarify:
```
:node([attr="value"]):edge(*):node(.has-selection) { color: blue; }
```

It appears that this syntax matches entire paths of nodes and edges and not single nodes or edges to apply styling to.

A solution, in these regards, is to utilize a single question-mark in the selector.

```
:?node([attr="value"]):edge(*):node(.has-selection) { color:blue; }
:node([attr="value"]):?edge(*):node(.has-selection) { color:blue; }
:node([attr="value"]):edge(*):?node(.has-selection) { color:blue; }
```

All three selectors match the same set of paths, and the question-mark symbol, limited to one per path, indicates which thing, which node or edge, to select for styling.

## Logical Operations

Logical operators, `:not()`, `:and()`, and `:or()`, can be utilized.

```
:node([attr="value"]):edge(*):or(:node(.txt-sel):?edge(.rt-clk), :node(.img-sel):?edge(.rt-clk)):node(.context-menu)
{
  color: blue;
}
```

## Repetition

`:repeat(min, max, pattern)` could be a shorthand notation for describing repetition.

```
:node([attr="value"]):repeat(0, 9, :edge(.key-press):node(*)):edge(.key-press):?node(*)
{
  color: blue;
}
```

## Resource Description Framework

Towards providing the expressiveness to select and style nodes and edges from RDF graphs, the following example select and styles from RDF/XML markup.

```xml
<rdf:Description rdf:about="http://www.w3.org/TR/rdf-syntax-grammar">
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

Using the syntax under discussion, one could form a selection of a node and style it:

```css
@namespace rdf url(http://www.w3.org/1999/02/22-rdf-syntax-ns#)
@namespace ex  url(http://example.org/terms/)

:node(rdf|Description[rdf|about="http://www.w3.org/TR/rdf-syntax-grammar"]):edge(ex|editor):node(rdf|Description):edge(ex|fullName):?node(*)
{
   color: blue;
}
```

## Selected Previous Works
* [CSS Selectors](https://www.w3.org/TR/selectors-4/)
* [Fresnel Selector Language for RDF](https://www.w3.org/2005/04/fresnel-info/fsl/)
