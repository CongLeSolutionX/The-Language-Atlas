---
created: 2025-05-11 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY-SA 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Syntax Terrain: Defining Edges in DOT
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---



Edges represent the connections or relationships between nodes in a graph. DOT provides distinct syntax for edges in directed (`digraph`) and undirected (`graph`) graphs, along with attributes to customize their appearance and behavior.

## Edge Definition Syntax

*   **Directed Edges (`digraph`):** Use `->` (an arrow) to indicate direction from a source node to a target node.
```dot
/*
 * title: Edge Definition Syntax
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY-SA 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 */
digraph DirectedEdges {
    A -> B // Edge from A to B
    B -> C
    A -> C // Another edge from A
}
```

*   **Undirected Edges (`graph`):** Use `--` (a double dash) to indicate a connection without inherent direction.

```dot
/*
 * title: Undirected Edges
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY-SA 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 */
graph UndirectedEdges {
    A -- B // Edge between A and B
    B -- C
    A -- C
}
```

*   **Chaining Edges:** You can chain edge definitions for brevity:

```dot
/*
 * title: Chaining Edges
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY-SA 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 */
digraph ChainedEdges {
    A -> B -> C -> D // Equivalent to A->B; B->C; C->D;
}
graph ChainedUndirected {
    X -- Y -- Z    // Equivalent to X--Y; Y--Z;
}
```

----

## Edge Attributes

Similar to nodes, edges can have attributes specified in square brackets `[]` immediately following the edge definition.

```dot
/*
 * title: Edge Attributes
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY-SA 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 */
digraph EdgeAttributes {
    node [shape=box] // Default node shape for clarity

    A -> B [label="Process 1", color=blue, style=dashed]
    B -> C [label="Final Step", color=red, arrowhead=vee, penwidth=2.0]
    C -> A [label="Feedback Loop", style=dotted, constraint=false] // constraint=false means edge doesn't affect layout ranking
}
```

```mermaid
---
title: "Graphviz Processing Pipeline"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY-SA 4.0"
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
    subgraph Edge_Definition_Syntax["Edge Definition Syntax"]
    direction LR
      S[SourceNode] --> Arrow["(-> or --)"]
      Arrow --> T[TargetNode]
      T --> AL["[AttributeList<br/>(Optional)]"]
      AL --> SC[";"]
    end

    subgraph Example_Edge_with_Attributes["Example Edge with Attributes"]
        N1["A -> B [label=\'Connects To\', color=green, style=bold];"]
    end

    subgraph Common_Edge_Attributes["Common Edge Attributes"]
        LAE["label<br/>(display text for the edge)"]
        COE["color<br/>(edge line color)"]
        STE["style<br/>(solid, dashed, dotted, bold)"]
        PWE["penwidth<br/>(thickness of the edge line)"]
        AHE["arrowhead<br/>(normal, dot, vee, curve, inv, diamond, etc.)"]
        ATE["arrowtail<br/>(same options as arrowhead, for start of edge)"]
        ARS["arrowsize<br/>(multiplier for arrowhead/tail size)"]
        DIE["dir<br/>(forward, back, both, none - for custom arrow display)"]
        CSE["constraint<br/>(true/false - whether edge influences node ranking/layout)"]
        LNE["len<br/>(preferred edge length in inches - for neato/fdp)"]
        WTE["weight<br/>(higher weight often means shorter, straighter edges)"]
        FOE["fontname, fontsize, fontcolor<br/>(for edge labels)"]
        URE["URL<br/>(for clickable edges in SVG output)"]
    end
```

----

## Connecting to Node Ports or Compass Points

For nodes with specific connection points (like 'record' shapes or using compass points), you can specify these in the edge definition using a colon `:`.

*   **Record Shapes:** If a node is defined with a `record` shape and has labeled fields (ports), edges can connect to these ports.

```dot
/*
 * title: Record Shapes
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY-SA 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 */
digraph RecordPorts {
    nodeA [shape=record, label="<f0> Field 0 | <f1> Field 1 | <f2> Field 2"]
    nodeB [shape=box]
    nodeA:f1 -> nodeB [label="From Field 1"] // Connects from port f1 of nodeA
}
```

*   **Compass Points:** Nodes can be targeted at logical compass points (`n`, `ne`, `e`, `se`, `s`, `sw`, `w`, `nw`, `c` for center).

```dot
/*
 * title: Compass Points
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY-SA 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 */
digraph CompassPoints {
    A
    B
    A:e -> B:w [label="East of A to West of B"] // Connect A's east side to B's west side
}
```

The actual visual effect depends on the layout engine and node shapes.

Edges are the lifelines of your graph, and effectively styling them greatly enhances the communication of relationships within your diagrams.




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