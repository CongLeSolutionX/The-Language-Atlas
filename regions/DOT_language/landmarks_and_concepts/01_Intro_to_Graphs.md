---
created: 2025-05-11 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY-SA 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---


# Landmark: Understanding Graphs in DOT
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---



The DOT language is fundamentally about describing **graphs**. Before diving into DOT syntax, it's crucial to understand the core components of what constitutes a graph in this context.

## Basic Terminology

At its heart, a graph is a collection of **nodes** (also called vertices) connected by **edges** (also called links or arcs).

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
    A["Node A"] --> B["Node B"]
    B --> C["Node C"]
    A --> C
    D["Node D"]

    subgraph Graph_Elements["Graph Elements"]
    direction LR
        N(("Node/Vertex"))
        E("--- Edge/Arc ---")
    end

    style A fill:#87CB,stroke:#333,stroke-width:2px
    style B fill:#87CB,stroke:#333,stroke-width:2px
    style C fill:#87CB,stroke:#333,stroke-width:2px
    style D fill:#87CB,stroke:#333,stroke-width:2px
    
```

*   **Nodes:** Represent entities or objects. In DOT, nodes can have names (identifiers) and various attributes like labels, shapes, colors, etc.
*   **Edges:** Represent relationships or connections between nodes. Edges can also have attributes, such as labels, colors, styles (dashed, solid), and directionality.

---

## Types of Graphs

DOT can describe several types of graphs:

1.  **Undirected Graphs (`graph`)**: Edges have no inherent direction. A connection between A and B is the same as B to A. Defined using the `graph` keyword.
    *   Edge syntax: `A -- B;`

2.  **Directed Graphs (`digraph`)**: Edges have a specific direction, from a source node to a target node. A connection from A to B is distinct from B to A. Defined using the `digraph` keyword. This is the most common type.
    *   Edge syntax: `A -> B;`

3.  **Strict Graphs**: In a strict graph (either directed or undirected, specified with the `strict` keyword), multiple edges between the same pair of nodes (in the same direction for digraphs) are forbidden or merged. If an attribute is redefined for an existing edge, it's updated.

---

## Core Declaration

A DOT file typically starts by declaring the type of graph:

````
```dot
/*
 * title: Core Declaration
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY-SA 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 */
// Example of a simple directed graph
digraph MyFirstGraph {
    // Nodes and edges will be defined here
}

// Example of a simple undirected graph
graph MySecondGraph {
    // Nodes and edges will be defined here
}
```
````

This foundational understanding of graph theory elements is key to effectively using the DOT language to describe and, subsequently, visualize complex structures.






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