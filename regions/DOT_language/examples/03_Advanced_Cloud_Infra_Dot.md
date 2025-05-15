---
created: 2025-05-11 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY-SA 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



#  A Simplified Cloud Infrastructure Diagram for a Web Application
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.

---

Fellow Explorer! Let's tackle another practical, advanced example using the `dot` engine.

This time, we'll model a **Simplified Cloud Infrastructure Diagram for a Web Application**, including networking components like VPCs, subnets, load balancers, and different tiers of services. This will allow us to focus on grouping, network flow, and showing different zones of responsibility.





```dot
digraph Advanced_Cloud_Infrastructure {
    // --- Graph Defaults ---
    graph [
        layout=dot,
        rankdir=TB, // Top-to-Bottom flow, typical for network diagrams
        label="Simplified Cloud Web Application Infrastructure (AWS Example)",
        fontsize=24,
        fontname="Arial",
        bgcolor="azure", // Light blue background
        nodesep=0.6,
        ranksep=1.5,      // More space between layers
        splines=ortho,    // Orthogonal lines are good for network diagrams
        concentrate=true, // Try to merge parallel edges
        compound=true     // Essential for cluster edges
    ];

    // --- Node Defaults ---
    node [
        shape=box,
        style="filled,rounded",
        fontname="Helvetica",
        fontsize=10,
        width=1.8,
        height=0.7,
        fixedsize=true,
        margin="0.2,0.1"
    ];

    // --- Edge Defaults ---
    edge [
        fontname="Helvetica",
        fontsize=9,
        color=darkslategray,
        arrowhead=normal,
        arrowsize=0.8,
        penwidth=1.5
    ];

    // --- Internet / User ---
    User [
        shape=circle,
        label="Users\n🌍",
        fillcolor=lightblue,
        width=1.0,
        height=1.0,
        fontsize=12
    ];

    // --- AWS Region Cluster (Conceptual Boundary) ---
    subgraph cluster_AWS_Region {
        label="AWS Region (e.g., us-east-1)";
        bgcolor="lightgrey";
        style="filled,rounded";
        fontname="Arial Black";
        fontsize=16;
        color="grey";
        margin=25; // More padding around region

        // --- VPC (Virtual Private Cloud) ---
        subgraph cluster_VPC {
            label="VPC (10.0.0.0/16)";
            bgcolor="ivory";
            color="darkgoldenrod";
            style="filled,rounded,dashed";
            fontsize=14;
            margin=20;

            InternetGateway [
                label="Internet Gateway\n(IGW)",
                shape=house, // Symbolizing entry point
                fillcolor=khaki,
                width=1.5
            ];

            NATGateway [
                label="NAT Gateway",
                shape=cds,
                fillcolor=khaki,
                width=1.5
            ];

            // --- Public Subnets ---
            subgraph cluster_PublicSubnets {
                label="Public Subnets (DMZ)";
                bgcolor="lightyellow";
                color="orange";
                style="filled,rounded";
                fontsize=12;

                ALB [
                    label="Application\nLoad Balancer\n(ALB)",
                    shape=doubleoctagon, // Distinct load balancer shape
                    fillcolor=lightgoldenrodyellow,
                    width=2.2, height=1.0,
                    fontsize=11
                ];

                BastionHost [
                    label="Bastion Host\n(SSH Access)",
                    shape=parallelogram,
                    fillcolor=moccasin,
                    width=1.8
                ];

                // Align ALB and Bastion if desired, though they serve different purposes
                // {rank=same; ALB; BastionHost;}
            }


            // --- Private Subnets: Application Tier ---
            subgraph cluster_PrivateSubnets_App {
                label="Private Subnets - App Tier";
                bgcolor="lightcyan";
                color="dodgerblue";
                style="filled,rounded";
                fontsize=12;

                ASG_WebApp [
                    label="Web App Auto Scaling Group (ASG)",
                    shape=component, // Represents a group of instances
                    fillcolor=aliceblue,
                    width=3.0, height=1.5,
                    fontsize=11,
                    margin="0.3,0.2" // More internal margin for ASG box
                ];

                // Nodes within ASG (conceptual, not individual instances)
                // For simplicity, ASG_WebApp represents the group
                // WebAppInstance1 [label="WebApp EC2", color=transparent, fontcolor=transparent, style=dotted, width=0.1, height=0.1];
                // WebAppInstance2 [label="WebApp EC2", color=transparent, fontcolor=transparent, style=dotted, width=0.1, height=0.1];
                // ASG_WebApp -> WebAppInstance1 [style=invis];
                // ASG_WebApp -> WebAppInstance2 [style=invis];


                CachingService [
                    label="Caching Service\n(ElastiCache / Redis)",
                    shape=cylinder, // Often represented as cylinder storage
                    fillcolor=azure,
                    width=2.0
                ];
            }

            // --- Private Subnets: Data Tier ---
            subgraph cluster_PrivateSubnets_Data {
                label="Private Subnets - Data Tier";
                bgcolor="lavenderblush";
                color="deeppink";
                style="filled,rounded";
                fontsize=12;

                RDS_Primary [
                    label="RDS Primary DB\n(PostgreSQL / MySQL)",
                    shape=cylinder,
                    fillcolor=mistyrose,
                    width=2.0, height=1.0
                ];
                RDS_Replica [
                    label="RDS Read Replica",
                    shape=cylinder,
                    fillcolor=seashell,
                    width=1.8
                ];
            }
        } // End VPC

        // --- External AWS Services (Outside VPC but in Region) ---
        S3_Bucket [
            label="S3 Bucket\n(Static Assets, Logs)",
            shape=folder, // Box shape for S3
            fillcolor=palegoldenrod,
            width=2.0
        ];

        CloudWatch [
            label="CloudWatch\n(Monitoring, Alarms)",
            shape=tab,
            fillcolor=thistle,
            width=2.0
        ];

        WAF_Shield [
            label="AWS WAF & Shield\n(Security)",
            shape=shield,
            fillcolor=lightcoral,
            width=2.0, height=1.0
        ];

    } // End AWS Region


    // --- Third-Party Services (External to AWS) ---
    subgraph cluster_ThirdParty {
        label="Third-Party Services";
        bgcolor="honeydew";
        color="forestgreen";
        style="filled,rounded";
        fontsize=14;
        // rank=sink; // Try to place this group lower

        PaymentGateway_Ext [
            label="Payment Gateway\n(Stripe/PayPal)",
            shape=cds, fillcolor=palegreen,
            width=2.2
        ];
        CDN_Service [
            label="CDN Provider\n(Cloudflare/Akamai)",
            shape=cds, fillcolor=palegreen,
            width=2.2
        ];
    }


    // --- Edge Definitions: Network Flow ---

    // User Traffic
    User -> CDN_Service [label="Request (via CDN)", weight=10, style=bold];
    CDN_Service -> ALB [label="Origin Pull / Cached", weight=8, lhead=cluster_PublicSubnets, ltail=cluster_ThirdParty];
    User -> WAF_Shield [label="Direct Traffic (some)", style=dashed, constraint=false]; // Some traffic might hit WAF directly
    WAF_Shield -> ALB [label="Filtered Traffic", weight=9, style=bold, lhead=cluster_PublicSubnets];

    // Public Subnet Flow
    InternetGateway -> ALB [label="Ingress Traffic", weight=7, lhead=cluster_PublicSubnets, ltail=cluster_VPC, style=bold, color=blue];
    InternetGateway -> BastionHost [label="Management Access", style=dashed, color=darkorange];

    ALB -> ASG_WebApp [label="HTTP/S Traffic", weight=10, style=bold, color=green, lhead=cluster_PrivateSubnets_App];

    // App Tier Flow
    ASG_WebApp -> CachingService [label="Cache Read/Write", weight=3];
    ASG_WebApp -> RDS_Primary [label="DB Queries", weight=5, lhead=cluster_PrivateSubnets_Data, color=purple];
    ASG_WebApp -> PaymentGateway_Ext [label="Payment API", style=dashed, color=firebrick, ltail=cluster_PrivateSubnets_App, lhead=cluster_ThirdParty];
    ASG_WebApp -> NATGateway [label="Outbound Internet\n(e.g., 3rd party APIs)", weight=2, style=dotted, color=sienna]; // For services needing to reach out
    NATGateway -> InternetGateway [style=invis]; // Nat uses IGW

    // Data Tier Flow
    RDS_Primary -> RDS_Replica [label="Replication", dir=both, arrowtail=normal, arrowhead=none, style=dashed, color=deeppink];

    // Logging and Monitoring
    ASG_WebApp -> S3_Bucket [label="App Logs", style=dotted, color=dimgray];
    ALB -> S3_Bucket [label="Access Logs", style=dotted, color=dimgray];
    ASG_WebApp -> CloudWatch [label="Metrics, Logs", style=dotted, color=indigo];
    RDS_Primary -> CloudWatch [label="DB Metrics", style=dotted, color=indigo];

    // Static Assets
    ASG_WebApp -> S3_Bucket [label="Reads Static Content (sometimes)", style=dashed, constraint=false, color=darkgoldenrod];
    CDN_Service -> S3_Bucket [label="Origin for CDN", style=solid, color=darkgoldenrod, weight=4, ltail=cluster_ThirdParty];

    // Ordering constraints if needed (often dot gets this with cluster flow)
    // Example: Ensure AWS region elements are generally above third-party
    // CloudWatch -> PaymentGateway_Ext [style=invis, weight=100];
    // S3_Bucket -> CDN_Service [style=invis, weight=100];
}
```

**To Generate this Diagram:**

1.  Save the code above as `advanced_cloud_infra.gv` (or `.dot`).
2.  Run Graphviz:
    ```bash
    dot -Tpng advanced_cloud_infra.gv -o advanced_cloud_infra.png
    ```
    Or for SVG:
    ```bash
    dot -Tsvg advanced_cloud_infra.gv -o advanced_cloud_infra.svg
    ```

**Key Advanced Features Used in this Example:**

1.  **Nested Clusters:** `cluster_AWS_Region` contains `cluster_VPC`, which in turn contains `cluster_PublicSubnets`, `cluster_PrivateSubnets_App`, and `cluster_PrivateSubnets_Data`. This is powerful for showing hierarchical containment.
2.  **`compound=true`:** Absolutely essential for drawing edges *to* and *from* clusters (`lhead`, `ltail` implicitly used sometimes, or explicitly if needed).
3.  **`concentrate=true`:** Attempts to merge parallel edge paths, which can reduce clutter in network diagrams.
4.  **`splines=ortho`:** Good choice for structured diagrams like infrastructure, making connections clear.
5.  **Semantic Shapes:** Different shapes (`house` for IGW, `doubleoctagon` for ALB, `cylinder` for DBs/Caching, `component` for ASG, `shield` for WAF) to visually distinguish component types.
6.  **`rankdir=TB`:** Typical for showing layers of an infrastructure from user/internet down to backend services.
7.  **Logical Grouping for Flow:** Edges attempt to show typical request/data flow directions.
8.  **Different Line Styles/Colors for Edges:** To differentiate types of traffic or interaction (e.g., main traffic bold green, management access dashed orange, DB queries purple).
9.  **Varying `nodesep` and `ranksep`:** To provide adequate spacing between elements and layers.
10. **Using `margin` within cluster definitions and for the main graph:** To control padding.
11. **Fixed Size Nodes with Margins:** Ensures nodes have a consistent appearance.
12. **HTML-like labels are not heavily used here**, but could be for more detailed node information (e.g., IP addresses, instance types within a node). This example prioritizes component shapes and connections.

This cloud infrastructure example highlights how `dot` can be used to represent complex, layered systems with clear boundaries and relationships between components. Iteration and fine-tuning of spacing, edge weights, and sometimes invisible edges (though not heavily used here) are often part of creating a polished final diagram.




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