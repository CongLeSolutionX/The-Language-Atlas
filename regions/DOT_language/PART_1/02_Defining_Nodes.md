---
created: 2025-05-11 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY-SA 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Syntax Terrain: Defining Nodes in DOT
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.

---


Nodes are the fundamental building blocks of any graph, representing entities or objects. In DOT, defining a node is straightforward, and its appearance can be heavily customized using attributes.

## Basic Node Definition

The simplest way to define a node is by stating its identifier (ID):

```dot
/*
 * title: CHANGE_ME_DADDY
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 * 
 */
digraph NodeDefinition {
    nodeA; // Defines a node with the ID "nodeA"
    nodeB;
    "Node with Spaces"; // Node IDs with spaces or special characters must be quoted
    "another_node_1.0"; // Quotes are also good for IDs with punctuation or starting with numbers
}
```

If a node ID is used in an edge definition (e.g. `nodeX -> nodeY;`) but not explicitly defined beforehand, it is implicitly created with default attributes. However, explicit definition is clearer and allows for attribute assignment.

---

## Node Attributes

Attributes are assigned to nodes in square brackets `[]` immediately following the node ID.

```dot
/*
 * title: CHANGE_ME_DADDY
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 * 
 */
digraph NodeAttributes {
    nodeA [label="Start Point", shape=box, color=blue, style=filled, fillcolor=lightblue]
    nodeB [shape=ellipse, label="Process\nStep", fontsize=10]
    nodeC [label="End", shape=diamond, style=bold, color=red]

    nodeA -> nodeB -> nodeC
}
```

```mermaid
---
title: "Basic Terminology"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  layout: elk
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%%%%%%% Available curve styles include the following keywords:
%% basis, bumpX, bumpY, cardinal, catmullRom, linear, monotoneX, monotoneY, natural, step, stepAfter, stepBefore.
%%{
  init: {
    'flowchart': { 'htmlLabels': true, 'curve': 'linear' },
    'fontFamily': 'Monaco',
    'themeVariables': {
      'primaryColor': '#D5E3',
      'primaryTextColor': '#F8B229',
      'lineColor': '#F8B229',
      'primaryBorderColor': '#27AE60',
      'secondaryColor': '#EBDEF0',
      'secondaryTextColor': '#6C3483',
      'secondaryBorderColor': '#A569BD',
      'fontSize': '15px'
    }
  }
}%%
graph LR
    subgraph Node_Definition_Syntax["Node Definition Syntax"]
    direction LR
      A["NodeID"] --> B["[AttributeList<br/>(Optional)]"]
      B --> C[";"]
    end

    subgraph "Example Node with Attributes"
      N1["nodeA [label=\'My Label\', shape=box, style=filled, fillcolor=yellow]"]
    end

    subgraph Common_Node_Attributes["Common Node Attributes"]
        SA["shape<br/>(box, ellipse, circle, diamond, triangle, plaintext, record, Mrecord, etc.)"]
        LA["label<br/>(display text, can use \\n for newlines)"]
        CO["color<br/>(border color)"]
        FI["fillcolor<br/>(fill color, requires style=filled)"]
        ST["style<br/>(filled, dashed, dotted, bold, rounded)"]
        FO["fontname, fontsize, fontcolor"]
        WD["width, height (in inches, can be fixedsize=true)"]
        IM["image<br/>(path to image file to display in node)"]
        UR["URL<br/>(for clickable nodes in SVG output)"]
    end
```

----

## Node Labels

*   **Simple Text:** `label="My Node"`
*   **Multi-line Text:** `label="Line 1\nLine 2"` (The `\n` sequence creates a newline). Graphviz will automatically break long labels based on node size if not explicitly formatted.

----

## Node Shapes

DOT provides a rich set of built-in shapes. Some common ones:

*   `box`, `rectangle`, `square`
*   `ellipse`, `oval`, `circle`
*   `diamond`
*   `triangle`, `point`
*   `plaintext` (no visible shape, just the label)
*   `record`, `Mrecord` (for complex, multi-part nodes, see "Advanced Features")
*   `polygon` (allows specifying sides, skew, distortion)
*   `underline`, `cylinder`, `note`, `tab`, `folder`, `box3d`

The default shape is often `ellipse`.

----

## Implicit Node Creation

Nodes are automatically created if they appear in an edge statement and haven't been explicitly defined. They will use default node attributes.

```dot
/*
 * title: CHANGE_ME_DADDY
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 * 
 */
digraph ImplicitNodes {
    configuredNode [shape=box]
    configuredNode -> implicitNodeA // implicitNodeA created with defaults
    implicitNodeA -> implicitNodeB [label="Edge creates B"] // implicitNodeB also created
}
```

It's generally better practice to define nodes explicitly if you need to set specific attributes for them.

Mastering node definition and styling is crucial for creating understandable and visually appealing graph diagrams.







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