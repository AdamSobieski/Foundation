## Introduction

An approach is described here for selecting nodes and edges in graphs for purposes of styling.

Let us consider an alternating node and edge pseudo-class-like syntax. For examples:
```
:node(...):edge(...) { color: blue; }
```
or
```
:edge(...):node(...) { color: blue; }
```
The contents in the parentheses are a subset of the CSS selector syntax.

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

Logical operators, `:not()`, `:and()`, and `:or()`, can be utilized for indicating logical combinations of nodes, edges, and paths.

```
:node([attr="value"]):edge(*):or(:node(.txt-selection):?edge(.right-click),:node(.img-selection):?edge(.right-click))
{
  color: blue;
}
```

## Selected Previous Works
* [CSS Selectors](https://www.w3.org/TR/selectors-4/)
* [Fresnel Selector Language for RDF](https://www.w3.org/2005/04/fresnel-info/fsl/)
