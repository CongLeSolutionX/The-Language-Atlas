---
created: 2025-05-11 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY-SA 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---


# Scenic Visual Tour: Gallery of DOT & Graphviz Concepts
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.


This gallery provides a quick visual summary of key concepts related to the DOT language and its use with Graphviz, primarily using Mermaid diagrams to illustrate the ideas as discussed throughout this regional guide.

## 1. Basic Graph Components

```mermaid
---
title: "Basic Graph Components"
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
    B -- Undirected --- C["Node C"]
    A --> C
    D["Node D /<br/> Vertex"]

    subgraph Elements["Elements"]
        N(("Node/Vertex"))
        DE("--- Directed Edge --->")
        UE("--- Undirected Edge ---")
    end
    style A fill:#87CB,stroke:#333
    style B fill:#87CB,stroke:#333
    style C fill:#87CB,stroke:#333
    style D fill:#87CB,stroke:#333
```
*Caption: Fundamental building blocks: nodes (entities) and edges (relationships).*

----

## 2. DOT Attribute Scopes

```mermaid
---
title: "DOT Attribute Scopes"
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
      'primaryColor': '#D511E3',
      'primaryTextColor': '#F8B229',
      'primaryBorderColor': '#27AE60',
      'secondaryColor': '#EBD3',
      'secondaryTextColor': '#6C3483',
      'secondaryBorderColor': '#A569BD',
      'fontSize': '20px'
    }
  }
}%%
mindmap
root(("DOT Attributes Scope"))
  Graph_Global("Graph Global<br/>('graph [...]')")
  ::icon(fa fa-globe)
    Default_Node("Default Node<br/>('node [...]')")
    Default_Edge("Default Edge<br/>('edge [...]')")
    
  Subgraph_Cluster("Subgraph /<br/> Cluster<br/>('subgraph cluster_X [...]')")
  ::icon(fa fa-object-group)
    Overrides_Global_for_elements_within["Overrides Global for elements within"]
    
  Individual_Element("Individual Element<br/>('node_id [...]',<br/> 'A->B [...]')")
  ::icon(fa fa-paint-brush)
    Highest_precedence_overrides_all_defaults["Highest precedence, overrides all defaults"]
```
*Caption: Attributes can be defined at graph, default node/edge, subgraph/cluster, or individual element levels, with specific overrides.*

---

## 3. Subgraphs vs. Clusters

```mermaid
---
title: "Subgraphs vs. Clusters"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  layout: elk
  theme: base
---
%%%%%%%% Mermaid version v11.4.1-b.14
%%{
  init: {
    'fontFamily': 'Monaco',
    'themeVariables': {
      'primaryColor': '#568D',
      'primaryTextColor': '#F8B229',
      'primaryBorderColor': '#E622',
      'secondaryColor': '#E22F',
      'secondaryTextColor': '#6C3483',
      'secondaryBorderColor': '#A569BD',
      'lineColor': '#F8B229',
      'fontSize': '15px'
    }
  }
}%%
graph TD
    A["Main Graph"] --> SB1{"subgraph sg1<br/>(Logical)"}
    A --> SB2{"subgraph cluster_c1<br/>(Visual Box)"}

    subgraph Key_Differences["Key Differences"]
    style Key_Differences fill:#2D22,stroke:#333,stroke-width:2px
        SGS["'subgraph name {...}'<br/>Logical Grouping, Affects Rank"]
        CLS["'subgraph cluster_name {...}'<br/>Visual Box, Hierarchy"]
    end

    subgraph sg1_Visual["sg1"]
    style sg1_Visual fill:#f221,stroke:#333,stroke-width:2px
      N1["Node A"]
      N2["Node B"]
    end

    subgraph cluster_c1_Visual["cluster_c1"]
    style cluster_c1_Visual fill:#f922,stroke:#333,stroke-width:2px
        C1["Node C"]
        C2["Node D"]
        C1 --> C2
    end
    
```
*Caption: `subgraph` for logical grouping and rank control; `subgraph cluster_...` for visual encapsulation with a bounding box.*

----

## 4. DOT Syntax Core Structure

```mermaid
---
title: "DOT Syntax Core Structure"
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
    A["Graph Type Keyword<br/>(digraph/graph)"] --> B["Optional 'strict'"]
    B --> C["Optional Graph Name"]
    C --> D["{"]
    D --> E["Statement List<br/>(Nodes, Edges, Attrs, Subgraphs)"]
    E --> F["}"]
```
*Caption: The basic syntax for a DOT file: type, optional name, and statements within curly braces.*

---

## 5. Record Shapes and Ports

```mermaid
---
title: "Record Shapes and Ports"
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
      'lineColor': '#F8B229',
      'fontSize': '15px'
    }
  }
}%%
graph TD
    subgraph Record_Node_Example["Record Node Example"]
        R1["nodeR[shape=record,<br/> label=\'<f0> Data | <f1> Pointer | { SubA | <sB> SubB }\']"]
    end
    subgraph Edge_to_Port["Edge to Port"]
        E1["nodeR:f1 -> anotherNode"]
        E2["nodeR:sB -> thirdNode"]
    end
```
*Caption: Record shapes allow structured nodes with fields (ports) that edges can connect to specifically.*

---

## 6. HTML-Like Labels

```mermaid
---
title: "HTML-Like Labels"
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
    A["Node with HTML Label"] --> B["'shape=plaintext' (often)<br/>'label=<...HTML content...>'"]
    B --> C["'<TABLE>', '<FONT>', '<BR/>', '<IMG>', etc.<br/>(Subset of HTML)"]
    C --> D["Allows rich text, tables, colors within a single node label."]
    TD["Example:<br/> 'label=<TABLE BORDER='0'><TR><TD BGCOLOR='yellow'>Cell1</TD><TD>Cell2</TD></TR></TABLE>'"]
```
*Caption: HTML-like labels provide advanced formatting capabilities for node content.*

---

## 7. Graphviz Processing Pipeline

```mermaid
---
title: "Graphviz Processing Pipeline"
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
flowchart TD
    Input[".dot File"] --> Parser{"Parser"}
    Parser --> LE_Select{"Layout Engine Select"}
    LE_Select --> Layout["Layout Engine<br/>(dot, neato, etc.)"]
    Layout --> Renderer{"Renderer<br/>(SVG, PNG, etc.)"}
    Renderer --> Output["Output Image"]
```
*Caption: The journey of a DOT file through Graphviz: Parsing, Layout, and Rendering.*

----

## 8. Common Graphviz Layout Engines

```mermaid
---
title: "Common Graphviz Layout Engines"
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
      'secondaryColor': '#EBDEF0',
      'secondaryTextColor': '#6C3483',
      'secondaryBorderColor': '#A569BD',
      'fontSize': '20px'
    }
  }
}%%
mindmap
root(("Layout Engines"))
  dot("dot")
  ::icon(fa fa-sitemap)
    Hierarchical
    DAGs
  neato("neato")
  ::icon(fa fa-project-diagram)
    Spring model
    Undirected
  fdp("fdp")
  ::icon(fa fa-share-alt-square)
    Force-directed
    Undirected
  twopi("twopi")
  ::icon(fa fa-bullseye)
    Radial
  circo("circo")
  ::icon(fa fa-circle-notch)
    Circular
```
*Caption: Key Graphviz layout engines and their typical applications.*

This concludes our scenic tour. These visualizations aim to reinforce the core concepts explored in the DOT Language Region.

---

And with that, Fellow Explorer, the initial charting of the **DOT Language Region** is largely complete according to the Atlas's structure!

Each file aims to be a "map" or "guide" for its respective topic, employing `Mermaid.js` for visual aids directly within the Markdown, fulfilling the cartographic goals set out in the README. This structure allows for both deep dives into specific landmarks and a broader overview of the linguistic terrain.




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