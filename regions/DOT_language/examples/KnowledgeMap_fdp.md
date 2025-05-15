---
created: 2025-05-11 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# An advanced example using fdp engine
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.

---


Alright, Fellow Explorer, let's craft an advanced example for the `fdp` engine. 

This example will aim to showcase several features working together:
*   **Node clustering** (visual, not structural like `dot`'s `subgraph cluster_...`) by using similar attributes.
*   **Varying node sizes** based on a conceptual "importance" or "degree."
*   **Varying edge weights** to influence spring stiffness slightly.
*   **Using `K` and `iterations`** for layout tuning.
*   **Labels and different shapes.**
*   **Purpose:** To visualize a conceptual "knowledge graph" or "concept map" where related concepts cluster together, and more central/connected concepts are larger.

---

## KnowledgeMap 

```dot
graph KnowledgeMap {
    // --- FDP Specific Layout Control ---
    layout = fdp;          // Explicitly state, though -Kfdp on CLI is preferred
    K = 0.9;               // Optimal distance - higher spreads out more
    iterations = 600;      // More iterations for potentially better layout
    overlap = prism;       // Sophisticated overlap removal (try 'scale' or 'true' if prism not available/slow)
    sep = "+8";            // Extra separation between nodes
    splines = true;        // Allow edges to curve if they cross nodes (can be slow)
    // start = random;     // Uncomment for different initial placements across runs
    // seed = 42;          // Use with start=random for reproducible random starts

    // --- Default Node Attributes ---
    node [
        style="filled,rounded",
        fontname="Helvetica",
        fontsize=10,
        width=0.6, height=0.6 // Base size, will be overridden
    ];

    // --- Default Edge Attributes ---
    edge [
        color="#606060",
        penwidth=1.0
    ];

    // --- Define Concept Groups (Visual Grouping via Attributes) ---
    // Group 1: Core Concepts (Larger, distinct color)
    node [group="core", fillcolor="#FFD700", shape=doublecircle, width=1.2, height=1.2, fontsize=14];
    CoreAI [label="Artificial\nIntelligence"];
    MachineLearning [label="Machine\nLearning"];
    DeepLearning [label="Deep\nLearning"];

    // Group 2: Sub-Fields (Medium size, different color)
    node [group="subfield", fillcolor="#ADD8E6", shape=ellipse, width=0.9, height=0.9, fontsize=11];
    NLP [label="NLP"];
    ComputerVision [label="Computer\nVision", id="CV"]; // Using 'id' in case label changes
    ReinforcementLearning [label="RL"];
    ExpertSystems [label="Expert\nSystems"];

    // Group 3: Applications/Techniques (Smaller size, another color)
    node [group="application", fillcolor="#90EE90", shape=box, style="filled,rounded", width=0.7, height=0.7, fontsize=9];
    Chatbots;
    ImageRecognition;
    Robotics;
    NeuralNetworks [label="ANN"];
    DecisionTrees;
    RecommenderSystems [label="Recommender\nSystems"];
    GenerativeAI [label="Generative\nAI"];


    // --- Define Relationships (Edges) with Varying Strengths ---
    // Core Relationships (Stronger springs)
    edge [penwidth=2.5, color="#404040"];
    CoreAI -- MachineLearning [weight=5, len=1.5];
    MachineLearning -- DeepLearning [weight=5, len=1.2];
    MachineLearning -- ReinforcementLearning [weight=3, len=1.5];
    MachineLearning -- NLP [weight=3, len=1.8];
    MachineLearning -- ComputerVision [weight=3, len=1.8];
    CoreAI -- ExpertSystems [weight=2, len=2.0, style=dashed]; // Older connection

    // Sub-field to Application Relationships
    edge [penwidth=1.5, color="#707070"];
    DeepLearning -- NeuralNetworks [weight=4, len=1.0];
    DeepLearning -- GenerativeAI [weight=3, len=1.2];
    NLP -- Chatbots [weight=2, len=1.5];
    NLP -- GenerativeAI [weight=2, len=1.5];
    ComputerVision -- ImageRecognition [weight=2, len=1.5];
    ComputerVision -- Robotics [weight=1, len=1.8];
    ReinforcementLearning -- Robotics [weight=2, len=1.5];
    ExpertSystems -- DecisionTrees [weight=2, len=1.2, style=dashed];

    // Technique to Application Relationships
    edge [penwidth=1.0, color="#909090"];
    NeuralNetworks -- ImageRecognition [weight=3, len=1.0];
    NeuralNetworks -- Chatbots [weight=2, len=1.2, comment="Via Sequence-to-Sequence models"];
    DecisionTrees -- RecommenderSystems [weight=1, len=1.5, style=dotted];
    MachineLearning -- RecommenderSystems [weight=2, len=1.8];


    // Add a few more inter-group connections to show complex structure
    GenerativeAI -- ImageRecognition [label="e.g., GANs\nfor image synth", fontsize=7, fontcolor=darkgreen];
    Chatbots -- Robotics [label="Interaction", fontsize=7, style=dotted];

    // --- A small, somewhat isolated concept ---
    node [group="other", fillcolor="#E6E6FA", shape=septagon, width=0.8, height=0.8];
    QuantumComputing [label="Quantum\nComputing"];
    CoreAI -- QuantumComputing [weight=0.5, len=3.0, style=dashed, color=purple, label="Future Potential", fontsize=8];

    NetworkSecurity [label="Network\nSecurity", fillcolor="#FFCCCB", shape=octagon];
    CoreAI -- NetworkSecurity [len=2.5, style=dashed, color=maroon, label="AI in Security", fontsize=8];
    ExpertSystems -- NetworkSecurity [len=2.0, style=dotted, color=maroon];

}
```

---

## To Compile This Example

Save the code above as `advanced_fdp_example.dot`. Then run from your terminal:
```bash
dot -Kfdp -Tsvg advanced_fdp_example.dot -o advanced_fdp_example.svg
# Or for PNG:
# dot -Kfdp -Tpng advanced_fdp_example.dot -o advanced_fdp_example.png
```
Open `advanced_fdp_example.svg` (or `.png`) in a suitable viewer. SVG is recommended for scalability and clarity.


---


## What This Example Tries to Achieve with `fdp`

1.  **Visual Clustering:**
    *   Nodes representing "Core Concepts", "Sub-Fields", and "Applications" are given distinct colors, shapes, and sizes. `fdp` will naturally try to keep connected nodes together, and these visual cues will reinforce the groupings.
2.  **Centrality and Importance:**
    *   `CoreAI` and `MachineLearning` are larger and have more strong connections, so `fdp` should naturally place them more centrally within their connected components.
3.  **Edge Influence:**
    *   `weight` and `len` attributes on edges attempt to influence the "springs." Stronger weights/shorter desired lengths might pull nodes closer (though `K` is a global factor).
    *   Different `penwidth` and `color` for edges can also visually denote connection strength or type.
4.  **Layout Parameters (`K`, `iterations`, `overlap`, `sep`):**
    *   `K=0.9` attempts to give nodes a bit more breathing room than the default.
    *   `iterations=600` provides more time for the layout to settle.
    *   `overlap=prism` uses a more advanced method for untangling nodes. If it's too slow or not available in your Graphviz build, try `overlap=scale` or `overlap=true`.
    *   `sep="+8"` provides a bit of extra padding.
5.  **Organic Structure:**
    *   The resulting layout should feel more "organic" than a strict `dot` hierarchy, showing the interconnectedness of AI concepts.
6.  **Labels and Readability:**
    *   Newline characters (`\n`) are used in labels for better formatting on nodes. Edge labels are also used.
    *   Different `fontsize` values are used to match node "importance."
7.  **Isolated/Peripheral Concepts:**
    *   `QuantumComputing` and `NetworkSecurity` have fewer or weaker connections to the main cluster, so `fdp` should position them more peripherally.

---


## Experimentation Encouraged

*   **Change `K`:** Try `K=0.5` (tighter) or `K=1.5` (much looser).
*   **Adjust `iterations`:** See if more or fewer iterations make a noticeable difference.
*   **Modify `edge` weights and `len` values:** Observe their subtle impact on local node arrangements.
*   **Toggle `splines`:** See the difference between `splines=true` and `splines=false` (or not setting it, which often defaults to straight lines for `fdp`).
*   **Different `overlap` methods:** `scale`, `scalexy`, `compress`, `false`.
*   Add/remove nodes and edges to see how the "physical system" rebalances.


---


This example demonstrates that while `fdp` offers a different layout philosophy, you still have many levers through attributes to guide and refine the final visualization. It often requires more iterative tuning than `dot` to get the desired aesthetic and clarity for complex, non-hierarchical data.


---


<!-- 
```mermaid
%% Current Mermaid version
info
```
-->


```mermaid
---
title: "CongLeSolutionX"
author: "Cong Le"
version: "1.0"
license(s): "MIT, CC BY 4.0"
copyright: "Copyright (c) 2025 Cong Le. All Rights Reserved."
config:
  theme: base
---
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
>- **Creative Commons Attribution 4.0 International:** [![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)](LICENSE-CC-BY) - Legal details in [LICENSE-CC-BY](LICENSE-CC-BY) and at [Creative Commons official site](http://creativecommons.org/licenses/by/4.0/).
>
---