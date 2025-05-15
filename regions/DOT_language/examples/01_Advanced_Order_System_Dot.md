---
created: 2025-05-11 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY-SA 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# A Simplified Order Processing System
> This content is dual-licensed under your choice of the following licenses:
> 1.  **MIT License:** For the code implementations in Swift and Mermaid provided in this document.
> 2.  **Creative Commons Attribution 4.0 International License (CC BY 4.0):** For all other content, including the text, explanations, and the Mermaid diagrams and illustrations.

---

Let's craft an advanced example using the `dot` engine, incorporating many of the concepts we've discussed: clusters, record shapes, HTML-like labels, ranking, port connections, and default attributes.


This example will depict a simplified **Order Processing System** with different services communicating via a message queue.



```dot
digraph AdvancedOrderSystem {
    // --- Graph Defaults ---
    graph [
        layout=dot, // Explicitly state, though it's default
        rankdir=TB, // Top-to-Bottom hierarchy
        label="Simplified Order Processing System",
        fontsize=20,
        fontname="Arial",
        bgcolor="azure2", // Light background for the whole graph
        nodesep=0.6,      // Increase separation between nodes on the same rank
        ranksep=1.0,      // Increase separation between ranks
        splines=ortho,    // Use orthogonal edges for a cleaner look
        compound=true     // Allow edges to connect to clusters
    ];

    // --- Node Defaults ---
    node [
        shape=box,
        style="filled,rounded",
        fontname="Helvetica",
        fontsize=12,
        margin="0.1,0.05" // Reduce internal margin slightly
    ];

    // --- Edge Defaults ---
    edge [
        fontname="Helvetica",
        fontsize=9,
        color=darkslategray,
        arrowhead=normal,
        arrowsize=0.8
    ];

    // --- Main Application Components ---
    WebApp [
        label=<
            <TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0" CELLPADDING="5" BGCOLOR="lightyellow">
                <TR><TD COLSPAN="2"><B>Web Application</B></TD></TR>
                <TR><TD ALIGN="LEFT">UI/UX Layer</TD><TD PORT="api_out" ALIGN="CENTER">🛒</TD></TR>
                <TR><TD ALIGN="LEFT" COLSPAN="2"><FONT POINT-SIZE="8">User places order</FONT></TD></TR>
            </TABLE>
        >,
        shape=plaintext, // Let HTML define the shape
        fillcolor=lightyellow // Redundant due to HTML BGCOLOR, but for consistency
    ];

    MobileApp [
        label="Mobile App\n(React Native)",
        shape=mobile, // Assuming 'mobile' is a custom shape or using a standard one.
                      // If not, use a rectangle with an icon.
                      // For this example let's use a box.
        shape=box,
        fillcolor=lightgoldenrodyellow,
        group=clients         // Group client apps
    ];

    // --- Align client apps on the same rank ---
    subgraph {
        rank=same;
        WebApp; MobileApp;
    }

    // --- API Gateway ---
    APIGateway [
        label="API Gateway\n(Kong / Traefik)",
        fillcolor=thistle,
        width=2.5,
        height=1.0
    ];

    // --- Microservices Cluster ---
    subgraph cluster_Microservices {
        label="Backend Microservices";
        bgcolor="lightblue";
        style="filled,rounded";
        color="blue";
        fontname="Arial";
        fontsize=14;

        OrderService [
            label="{ <header> Order Service | + PlaceOrder() \l + GetOrderStatus() \l | <msg_out> Produces OrderCreatedEvent \l }",
            shape=record,
            fillcolor=aliceblue
        ];

        InventoryService [
            label="{ <header> Inventory Service | + CheckStock() \l + ReserveItem() \l | <msg_in> Consumes OrderCreatedEvent \l }",
            shape=record,
            fillcolor=aliceblue
        ];

        PaymentService [
            label="Payment Service\n(Stripe Integration)",
            fillcolor=lightcyan
        ];

        NotificationService [
            label="Notification Service\n(Email/SMS)",
            fillcolor=lightcyan
        ];

        // Align services that might interact sequentially or are at similar stages
        subgraph {
            rank=same; InventoryService; PaymentService;
        }
    }

    // --- Data Stores Cluster ---
    subgraph cluster_DataStores {
        label="Data Stores";
        bgcolor="lightgrey";
        style="filled,rounded";
        color="dimgray";
        fontname="Arial";
        fontsize=14;

        OrderDB [
            shape=cylinder,
            label="Order Database\n(PostgreSQL)",
            fillcolor=whitesmoke,
            width=1.5
        ];

        InventoryDB [
            shape=cylinder,
            label="Inventory DB\n(MongoDB)",
            fillcolor=whitesmoke,
            width=1.5
        ];
    }

    // --- Message Queue ---
    MessageQueue [
        label=<
            <TABLE BORDER="1" CELLBORDER="0" CELLSPACING="0" CELLPADDING="5" BGCOLOR="peachpuff">
              <TR><TD PORT="mq_logo"><IMG SRC="path/to/your/kafka_or_rabbitmq_logo.png" SCALE="TRUE"/></TD></TR>
              <TR><TD><B>Message Queue</B></TD></TR>
              <TR><TD>(Kafka / RabbitMQ)</TD></TR>
            </TABLE>
        >,
        shape=plaintext,
        // If no image:
        // label="Message Queue\n(Kafka / RabbitMQ)",
        // shape=cds, // Or a standard shape
        // fillcolor=peachpuff,
        width=2.0,
        height=1.2
    ];


    // --- External Systems ---
    ExternalPaymentGateway [
        label="External Payment\nGateway (Stripe)",
        shape=cds, // Using cds to represent external service or storage conceptually
        fillcolor=moccasin,
        group=external
    ];

    ShippingProviderAPI [
        label="Shipping Provider\nAPI (FedEx/UPS)",
        shape=cds,
        fillcolor=moccasin,
        group=external
    ];


    // --- Edge Definitions ---

    // Client to API Gateway
    WebApp:api_out             -> APIGateway [label="REST/GraphQL", weight=5];
    MobileApp                  -> APIGateway [label="REST/GraphQL", weight=5];

    // API Gateway to Services
    APIGateway                 -> OrderService [label="PlaceOrder Req", weight=3];
    APIGateway                 -> InventoryService:header [label="CheckStock Req", style=dashed, constraint=false]; // Example of non-constraining secondary path
    APIGateway                 -> PaymentService [label="ProcessPayment Req", weight=2];

    // Order Service Flow
    OrderService:msg_out       -> MessageQueue [label="OrderCreated Event", arrowhead=open, color=firebrick, style=bold, weight=4];
    OrderService               -> OrderDB [label="Save Order", dir=both, arrowhead=normal, arrowtail=odot]; // Read/Write

    // Message Queue Consumers
    MessageQueue               -> InventoryService:msg_in [label="Consume Event", color=firebrick, style=bold, weight=4, ltail=cluster_Microservices];
    MessageQueue               -> NotificationService [label="Consume Event", color=firebrick, style=dashed, weight=2, ltail=cluster_Microservices];

    // Inventory Service Flow
    InventoryService           -> InventoryDB [label="Update Stock", dir=both];

    // Payment Service Flow
    PaymentService             -> ExternalPaymentGateway [label="Authorize/Capture", weight=3];
    ExternalPaymentGateway     -> PaymentService [label="Payment Status", style=dotted];

    // Notification and Shipping
    NotificationService        -> WebApp [label="Order Confirmed Email", style=dashed, constraint=false, port=_]; // Edge to a port implicitly named by the node
    NotificationService        -> MobileApp [label="Push Notification", style=dashed, constraint=false];
    OrderService               -> ShippingProviderAPI [label="Shipment Request", style=dashed];


    // Invisible edges for layout refinement (Example - use sparingly)
    // To ensure MessageQueue is below OrderService but above Inventory/Payment
    // OrderService -> MessageQueue [style=invis, weight=10]; // Already connected, this would be if MQ wasn't directly connected.
    // MessageQueue -> InventoryService [style=invis, weight=10];


    // --- Final Ranking Adjustments if needed (often iterative) ---
    // Example: Ensure external systems are at the bottom
    subgraph {
       rank=max; // Could also use 'sink'
       ExternalPaymentGateway; ShippingProviderAPI;
    }
}

```

**To Generate this Diagram:**

1.  **Save:** Save the code above as `advanced_order_system.gv` (or `.dot`).
2.  **Image for Message Queue (Optional):**
    *   Find a small logo for Kafka or RabbitMQ (e.g., a PNG).
    *   Save it as `kafka_or_rabbitmq_logo.png` in a directory named `path/to/your/` relative to where you run the `dot` command, or provide an absolute path. If you don't have an image, comment out the `<IMG>` tag and uncomment the alternative `MessageQueue` definition.
3.  **Run Graphviz:**
    ```bash
    dot -Tpng advanced_order_system.gv -o advanced_order_system.png
    ```
    Or for SVG:
    ```bash
    dot -Tsvg advanced_order_system.gv -o advanced_order_system.svg
    ```

**Key Advanced Features Used in this Example:**

1.  **Global Defaults (`graph`, `node`, `edge`):** Establishes a consistent base style.
2.  **HTML-Like Labels (`WebApp`, `MessageQueue`):** Allows for rich formatting, tables, and embedding images (conceptually).
3.  **Record Shapes (`OrderService`, `InventoryService`):** Structures node content into logical sections with named ports.
4.  **Clusters (`subgraph cluster_...`):** Visually groups related services (Microservices, DataStores). `compound=true` is essential.
5.  **`rankdir=TB`:** Defines the overall flow from top to bottom.
6.  **`rank=same`:** Aligns `WebApp` and `MobileApp`, and also `InventoryService` and `PaymentService`.
7.  **`rank=max` (or `sink`):** Pushes external systems towards the "end" of the graph.
8.  **Port Connections (e.g., `OrderService:msg_out`, `WebApp:api_out`):** Ensures edges connect to specific parts of nodes.
9.  **`splines=ortho`:** Uses right-angle edges, often good for system diagrams.
10. **`weight` on Edges:** Influences the "straightness" and importance of edges in the layout (e.g., main flow vs. secondary).
11. **`constraint=false`:** For edges that shouldn't dictate the primary layout ranking.
12. **`dir=both`, `arrowhead`, `arrowtail`:** For bidirectional data flow indication on edges.
13. **`group` Attribute (on nodes):** Hints to keep client apps and external services somewhat grouped during node ordering.
14. **Comments:** To explain different sections.
15. **`nodesep`, `ranksep`:** To adjust spacing.

This example is fairly dense, but it showcases how these features can be combined to create a detailed and informative diagram using the `dot` layout engine. You'd typically build such a diagram iteratively, generating it frequently to see how changes affect the layout.



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