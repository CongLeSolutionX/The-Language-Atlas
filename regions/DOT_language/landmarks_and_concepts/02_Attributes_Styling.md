---
created: 2025-05-11 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY-SA 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Landmark: Attributes and Styling in DOT
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.



Attributes are the primary mechanism in DOT for controlling the appearance and layout of graph elements (graphs, nodes, and edges). They allow for customization of labels, colors, shapes, styles, fonts, and much more.

## Attribute Scope

Attributes can be set at different levels, establishing defaults that can be overridden:

1.  **Graph Attributes (`graph [...]`)**: Apply to the graph as a whole (e.g., background color, layout direction, default node/edge styles).
2.  **Default Node Attributes (`node [...]`)**: Set default properties for all nodes defined subsequently.
3.  **Default Edge Attributes (`edge [...]`)**: Set default properties for all edges defined subsequently.
4.  **Individual Node/Edge Attributes**: Set properties for a specific node or edge, overriding defaults.

```mermaid
---
title: "CHANGE_ME_DADDY"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%{
  init: {
    'fontFamily': 'Monaco',
    'themeVariables': {
      'primaryColor': '#D5E3',
      'primaryTextColor': '#F8B229',
      'primaryBorderColor': '#27AE60',
      'secondaryColor': '#EEF2',
      'secondaryTextColor': '#6C3483',
      'secondaryBorderColor': '#A569BD',
      'fontSize': '20px'
    }
  }
}%%
mindmap
root(("DOT Attributes"))
    Graph_Attributes("Graph Attributes")
    ::icon(fa fa-project-diagram)
        layout["layout<br/>(e.g., dot, neato)"]
        rankdir["rankdir<br/>(LR, TB, RL, BT)"]
        bgcolor["bgcolor<br/>(background color)"]
        label["label<br/>(graph title)"]
        fontname
        fontsize
        splines["splines<br/>(edge routing style)"]
        concentrate["concentrate<br/>(merge parallel edges)"]
    Default_Node_Attributes("Default Node Attributes")
    ::icon(fa fa-circle)
        shape["shape<br/>(box, ellipse, circle, diamond, record, etc.)"]
        style["style<br/>(filled, solid, dashed, dotted)"]
        color["color<br/>(outline color)"]
        fillcolor["fillcolor<br/>(fill color, if style=filled)"]
        fontname
        fontsize
        fontcolor
        label["label<br/>(node text)"]
    Default_Edge_Attributes("Default Edge Attributes")
    ::icon(fa fa- condividi-alt)
        style["style<br/>(solid, dashed, dotted, bold)"]
        color["color<br/>(edge color)"]
        styles_of_arrow_ends["styles of arrow ends:<br/>arrowhead,<br/> arrowtail"]
        arrowsize
        label["label<br/>(edge text)"]
        fontname
        fontsize
        fontcolor
        constraint["constraint<br/>(whether edge affects ranking)"]
    Individual_Element_Attributes("Individual Element Attributes")
    ::icon(fa fa-paint-brush)
        Overrides defaults
        Syntax["Syntax:<br/> 'elementName [attr1=value1, attr2=value2]'"]
        Example["Example:<br/> 'NodeA [label='Start Node', shape=box, style=filled, fillcolor=lightblue]'"]
        Example["Example:<br/> 'NodeA -> NodeB [label='Connects to', color=red, style=dashed]'"]
      
```

---


## Common Attributes

Here's a table of some frequently used attributes:

| Attribute   | Applies To      | Description                               | Example Value(s)                 |
|-------------|-----------------|-------------------------------------------|---------------------------------|
| `label`     | Graph, Node, Edge | Text displayed for the element.             | `"My Node"`, `"Process Data"`   |
| `shape`     | Node            | Visual shape of the node.                 | `box`, `ellipse`, `record`, `plaintext` |
| `style`     | Node, Edge      | Visual style.                             | `filled`, `dashed`, `dotted`, `bold` |
| `color`     | Node (border), Edge | Color of the border or edge line.       | `red`, `blue`, `#FF0000`         |
| `fillcolor` | Node            | Fill color (if `style=filled`).         | `lightgrey`, `yellow`           |
| `fontname`  | Graph, Node, Edge | Font used for labels.                     | `Arial`, `Helvetica`            |
| `fontsize`  | Graph, Node, Edge | Size of the font for labels.              | `12`, `10`                      |
| `rankdir`   | Graph           | Layout direction (`TB`, `LR`, `BT`, `RL`). | `LR` (Left to Right)            |
| `arrowhead` | Edge            | Style of the arrow at the target node.    | `normal`, `dot`, `vee`, `empty` |
| `arrowtail` | Edge            | Style of the arrow at the source node.    | `normal`, `inv`                 |
| `width`     | Node            | Minimum width of a node in inches.        | `0.75`                          |
| `height`    | Node            | Minimum height of a node in inches.       | `0.5`                           |
| `URL`       | Graph, Node, Edge | Hyperlink for clickable diagrams (SVG).   | `"https://example.com"`         |



*(Note: Numerical values for attributes like `fontsize`, `width`, `height` often do not need quotes unless they contain special characters. String values always need quotes.)*

**HTML-Like Labels:** For more complex node labels, DOT supports a subset of HTML-like syntax within the `label` attribute, allowing for tables, font specifications, and structured content within a node. This is specified by surrounding the label value with `<` and `>`.

Example:
```dot
/*
 * title: HTML-Like Labels
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 * 
 */
digraph HtmlLabel {
    nodeA [label=<
        <TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0">
            <TR><TD COLSPAN="2" BGCOLOR="lightblue"><B>Header</B></TD></TR>
            <TR><TD>Field 1</TD><TD PORT="f1">Value 1</TD></TR>
            <TR><TD>Field 2</TD><TD PORT="f2">Value 2</TD></TR>
        </TABLE>
    >]
    nodeB [label="Simple Node"]
    nodeA:f1 -> nodeB // Connect from a port in the HTML table
}
```

Mastering attributes is key to producing clear, aesthetically pleasing, and informative graph visualizations with DOT and Graphviz.







---

<!-- 
```mermaid
%% Current Mermaid version
info
```  -->


```mermaid
---
title: "CongLeSolutionX"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY-SA 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%{
  init: {
    'flowchart': { 'htmlLabels': false },
    'fontFamily': 'Bradley Hand',
    'themeVariables': {
      'primaryColor': '#fc82',
      'primaryTextColor': '#F8B229',
      'primaryBorderColor': '#27AE60',
      'secondaryColor': '#81c784',
      'secondaryTextColor': '#6C3483',
      'lineColor': '#F8B229',
      'fontSize': '20px'
    }
  }
}%%
flowchart LR
    My_Meme@{ img: "https://raw.githubusercontent.com/CongLeSolutionX/MY_GRAPHIC_ASSETS/refs/heads/Designing_graphic_syntax/MY_MEME/My-meme-icon-design.png", label: "Ăn uống gì chưa ngừi đẹp?", pos: "b", w: 200, h: 150, constraint: "on" }

    Closing_quote@{ shape: braces, label: "I'll leave this Earth empty-handed anyway!<br/>YOLO" }

My_Meme ~~~ Closing_quote


```

---
>**Licenses:**
>
>- **MIT License:**  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) - Full text in [LICENSE](LICENSE) file.
>- **Creative Commons Attribution-ShareAlike 4.0 International**: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) [![CC BY-SA 4.0](https://licensebuttons.net/l/by-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-sa/4.0/) - Legal details in [LICENSE-CC-BY-SA-4.0](LICENSE-CC-BY-SA-4.0) and at [Creative Commons official site](https://creativecommons.org/licenses/by-sa/4.0/).
>
---