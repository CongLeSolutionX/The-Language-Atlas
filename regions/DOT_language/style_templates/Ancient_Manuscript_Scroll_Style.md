---
created: 2025-05-17 05:31:26
author: Cong Le
version: "1.0"
license(s): MIT, CC BY-SA 4.0
copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
---



# Ancient Manuscript - Scroll Style
> **Disclaimer:**
>
> This document contains my personal notes on the topic,
> compiled from publicly available documentation and various cited sources.
> The materials are intended for educational purposes, personal study, and reference.
> The content is dual-licensed:
> 1. **MIT License:** Applies to all code implementations (Swift, Mermaid, and other programming languages).
> 2. **Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0):** Applies to all non-code content, including text, explanations, diagrams, and illustrations.
---

This DOT script attempts to create a genealogical chart in an "Ancient Manuscript / Scroll" theme.
This DOT code aims to be a single-file, comprehensive example. The success of the "look" will heavily depend on the Graphviz renderer and the availability of the specified fonts on the system where it's processed. If specific fonts like "Blackletter" or "Blackadder ITC Std" are unavailable, Graphviz will fall back to a default, which might alter the intended aesthetic somewhat but the core structure and color scheme will remain.


---


## Ancient Manuscript - Scroll Style


![Ancient Manuscript - Scroll Style](https://g.gravizo.com/source/svg/rendered_code_ancient_manuscript_template?https%3A%2F%2Fraw.githubusercontent.com%2FCongLeSolutionX%2FThe-Language-Atlas%2Frefs%2Fheads%2Fmain%2Fregions%2FDOT_language%2Fstyle_templates%2FAncient_Manuscript_Scroll_Style.md)


<details>

<summary>Rendered code for the Ancient Manuscript - Scroll Style</summary>

rendered_code_ancient_manuscript_template
digraph ancient_scroll_genealogy_of_houses {
    graph [
        rankdir=TB,
        bgcolor="#F5DEB3",
        fontname="Garamond",
        fontsize=10,
        fontcolor="#5C4033",
        nodesep=0.6,
        ranksep=1.2,
        splines=ortho,
        label="Chronicles of the Exalted Houses\nAbridged Lineage & Alliances\nCirca Third Age, Year of the Crimson Moon",
        labelloc=t,
        fontnames="Times New Roman Italic"
    ];
    node [
        fontname="Garamond",
        fontsize=9,
        fontcolor="#4A2C2A",
        shape=rect,
        style="filled,rounded",
        color="#8B4513",
        fillcolor="#FAF0E6",
        penwidth=1,
        margin="0.15,0.08"
    ];
    edge [
        fontname="Garamond Italic",
        fontsize=8,
        fontcolor="#704214",
        color="#A0522D",
        penwidth=1.2,
        arrowhead=none,
        arrowtail=none
    ];
    subgraph cluster_title_illumination {
        label="";
        style=invis;
        bgcolor="transparent";
        TITLE_ORNAMENT_TOP [
            shape=plaintext,
            label="PLACEHOLDER FOR TITLE_ORNAMENT_TOP"
        ];
        TITLE_SEPARATOR [ shape=rect, style=filled, fillcolor="#C19A6B", color="#C19A6B", height=0.02, width=5, label=""];
    }
    subgraph cluster_house_sunstone {
        label="The Noble House of Sunstone";
        fontname="Blackletter";
        fontsize=12;
        fontcolor="#800000";
        color="#B8860B";
        style="filled,rounded";
        bgcolor="#FFF8DC";
        Elara_Sunstone [label="Lady Elara 'the Radiant'\n(Matriarch, d. 2A 876)", shape=ellipse, style="filled,bold", fillcolor="#FFD700", color="#DAA520"];
        Corin_Sunstone [label="Lord Corin 'Stonehand'\n(Son of Elara, Current Head)"];
        Lyra_Sunstone [label="Lady Lyra\n(Daughter of Corin)"];
        Torvin_Sunstone [label="Ser Torvin 'the Steadfast'\n(Brother of Corin)"];
    }
    subgraph cluster_house_shadowvale {
        label="The Ancient House of Shadowed Vale";
        fontname="Blackletter";
        fontsize=12;
        fontcolor="#2F4F4F";
        color="#556B2F";
        style="filled,rounded";
        bgcolor="#F0FFF0";
        Malakor_Shadowvale [label="Lord Malakor 'the Old'\n(Patriarch, Est. Age 230)", shape=octagon, style="filled,bold", fillcolor="#A9A9A9", color="#696969"];
        Seraphina_Shadowvale [label="Lady Seraphina\n(Granddaughter of Malakor)"];
        Kael_Shadowvale [label="Kael 'the Silent'\n(Son of Seraphina)"];
    }
    Aella_Whisperwind [label="Aella of the Whispering Reeds\n(Vassal to Sunstone)", style="filled", fillcolor="#E0FFFF"];
    Roric_Whisperwind [label="Roric, son of Aella"];
    Marriage_Corin_Seraphina_Link [shape=point, style=invis, width=0.01, height=0.01];
    Marriage_Torvin_Aella_Link [shape=point, style=invis, width=0.01, height=0.01];
    subgraph cluster_colophon {
        label="Scribal Attestations & Marginalia";
        fontname="Garamond Italic";
        fontsize=9;
        fontcolor="#704214";
        color="#C19A6B";
        style="rounded,dashed";
        bgcolor="#FAF0E6";
        SCRIBE_NOTES [
            shape=note,
            style="filled",
            fillcolor="#FFFACD",
            color="#BDB76B",
            fontname="Segoe Print",
            fontsize=7,
            fontcolor="#5C3317",
            label="PLACEHOLDER FOR SCRIBE_NOTES"
        ];
        WATERMARK_SYMBOL [shape=plaintext, label="📜", fontcolor="#D2B48C90", fontsize=24];
    }
    TITLE_ORNAMENT_TOP -> TITLE_SEPARATOR [style=invis, minlen=0.1];
    TITLE_SEPARATOR -> Elara_Sunstone [style=invis, minlen=1.5];
    Elara_Sunstone -> Corin_Sunstone [label="child", dir=none];
    Elara_Sunstone -> Torvin_Sunstone [label="child", dir=none];
    {rank=same; Corin_Sunstone; Torvin_Sunstone;}
    Corin_Sunstone -> Lyra_Sunstone [label="child", dir=none];
    Malakor_Shadowvale -> Seraphina_Shadowvale [label="descendant (grandchild)", dir=none, style=dashed, color="#666666"];
    Seraphina_Shadowvale -> Kael_Shadowvale [label="child", dir=none];
    Aella_Whisperwind -> Roric_Whisperwind [label="child", dir=none];
    Corin_Sunstone -> Marriage_Corin_Seraphina_Link [dir=none, constraint=false, style=dotted, color="#4682B4"];
    Seraphina_Shadowvale -> Marriage_Corin_Seraphina_Link [dir=none, constraint=false, style=dotted, color="#4682B4"];
    Marriage_Corin_Seraphina_Link -> Lyra_Sunstone [style=invis, label="Parents of Lyra", minlen=0.1];
    Torvin_Sunstone -> Marriage_Torvin_Aella_Link [dir=none, constraint=false, style=dotted, color="#8FBC8F"];
    Aella_Whisperwind -> Marriage_Torvin_Aella_Link [dir=none, constraint=false, style=dotted, color="#8FBC8F"];
    Aella_Whisperwind -> Corin_Sunstone [label="Vassalage", style="bold,dashed", color="#CD853F", constraint=false, dir=forward, arrowhead=empty];
    Lyra_Sunstone -> SCRIBE_NOTES [style=invis, weight=10, minlen=2.5];
    Kael_Shadowvale -> SCRIBE_NOTES [style=invis, weight=10, minlen=2.5];
    Roric_Whisperwind -> SCRIBE_NOTES [style=invis, weight=10, minlen=2.5];
    {rank=sink; SCRIBE_NOTES; WATERMARK_SYMBOL;}
}
rendered_code_ancient_manuscript_template

</details>
  




<details open>
<summary>Click to show/hide the full native DOT implementation with comment documentation.</summary>

```dot
/*
 * title: Ancient Manuscript - Scroll Style
 * author: Cong Le
 * version: 1.0
 * license(s): MIT, CC BY-SA 4.0
 * copyright: Copyright (c) 2025 Cong Le. All Rights Reserved.
 * 
 */
digraph ancient_scroll_genealogy_of_houses {
    // === Graph Gloal Attributes - Scroll Aesthetic ===
    graph [
        rankdir=TB,
        bgcolor="#F5DEB3", // Wheat - old paper / faded parchment
        fontname="Garamond", // Classic, readable serif, good for "old text"
        fontsize=10,
        fontcolor="#5C4033", // Dark Sepia for text
        nodesep=0.6,
        ranksep=1.2, // More vertical spacing for a scroll-like unfurling
        splines=ortho, // Gives a structured, almost charted feel
        label="Chronicles of the Exalted Houses\nAbridged Lineage & Alliances\nCirca Third Age, Year of the Crimson Moon",
        labelloc=t,
        fontnames="Times New Roman Italic" // Title font style
    ];

    // === Default Node Style - Aged Ink on Parchment ===
    node [
        fontname="Garamond",
        fontsize=9,
        fontcolor="#4A2C2A", // Darker Sepia/Brown for node text
        shape=rect, // Simple rectangles for names/houses
        style="filled,rounded", // Slightly rounded corners, filled
        color="#8B4513", // SaddleBrown - for drawn borders
        fillcolor="#FAF0E6", // OldLace/Linen - lighter than background, like fresher parchment patch
        penwidth=1,
        margin="0.15,0.08"
    ];

    // === Default Edge Style - Ink Lines of Connection ===
    edge [
        fontname="Garamond Italic",
        fontsize=8,
        fontcolor="#704214", // Sepia for relationship labels
        color="#A0522D", // Sienna - for ink lines
        penwidth=1.2,
        arrowhead=none, // Genealogies often don't use arrowheads for parent-child
        arrowtail=none
    ];

    // === HEADER / TITLE AREA - Simulating an Illuminated Title Block ===
    // Using an HTML-like label cluster for more control over the title presentation
    subgraph cluster_title_illumination {
        label=""; // Cluster label itself is not displayed
        style=invis; // Invisible cluster, for grouping only
        bgcolor="transparent";

        TITLE_ORNAMENT_TOP [
            shape=plaintext,
            label=<
            <TABLE BORDER="0" CELLBORDER="0" CELLSPACING="0">
            <TR><TD ALIGN="CENTER"><FONT POINT-SIZE="18" COLOR="#6A0DAD" FACE="Blackadder ITC Std">G</FONT><FONT POINT-SIZE="14" COLOR="#4A2C2A" FACE="Blackletter">enealogia </FONT><FONT POINT-SIZE="18" COLOR="#6A0DAD" FACE="Blackadder ITC Std">D</FONT><FONT POINT-SIZE="14" COLOR="#4A2C2A" FACE="Blackletter">omorum </FONT><FONT POINT-SIZE="18" COLOR="#6A0DAD" FACE="Blackadder ITC Std">N</FONT><FONT POINT-SIZE="14" COLOR="#4A2C2A" FACE="Blackletter">obilium</FONT></TD></TR>
            <TR><TD><FONT POINT-SIZE="3" COLOR="transparent"> </FONT></TD></TR> {/* Spacer */}
            <TR><TD ALIGN="CENTER"><FONT POINT-SIZE="8" COLOR="#704214" FACE="Garamond Italic">(Scroll Fragment - Scholar's Attestation)</FONT></TD></TR>
            </TABLE>
            >
        ];
         // Decorative line - simple for DOT, but suggestive
        TITLE_SEPARATOR [ shape=rect, style=filled, fillcolor="#C19A6B", color="#C19A6B", height=0.02, width=5, label=""];
    }


    // === MAIN HOUSES & INDIVIDUALS ===
    // House of the Sunstone (Major House)
    subgraph cluster_house_sunstone {
        label="The Noble House of Sunstone";
        fontname="Blackletter"; // Or "Old English Text MT"
        fontsize=12;
        fontcolor="#800000"; // Maroon, like an important rubric
        color="#B8860B"; // DarkGoldenrod - rich border for the house section
        style="filled,rounded";
        bgcolor="#FFF8DC"; // Cornsilk - slightly different parchment tone

        Elara_Sunstone [label="Lady Elara 'the Radiant'\n(Matriarch, d. 2A 876)", shape=ellipse, style="filled,bold", fillcolor="#FFD700", color="#DAA520"]; // Gold fill
        Corin_Sunstone [label="Lord Corin 'Stonehand'\n(Son of Elara, Current Head)"];
        Lyra_Sunstone [label="Lady Lyra\n(Daughter of Corin)"];
        Torvin_Sunstone [label="Ser Torvin 'the Steadfast'\n(Brother of Corin)"];
    }

    // House of the Shadowed Vale (Another Major House)
    subgraph cluster_house_shadowvale {
        label="The Ancient House of Shadowed Vale";
        fontname="Blackletter";
        fontsize=12;
        fontcolor="#2F4F4F"; // DarkSlateGray - for a more somber house
        color="#556B2F"; // DarkOliveGreen border
        style="filled,rounded";
        bgcolor="#F0FFF0"; // HoneyDew - cool parchment

        Malakor_Shadowvale [label="Lord Malakor 'the Old'\n(Patriarch, Est. Age 230)", shape=octagon, style="filled,bold", fillcolor="#A9A9A9", color="#696969"]; // DarkGray fill
        Seraphina_Shadowvale [label="Lady Seraphina\n(Granddaughter of Malakor)"];
        Kael_Shadowvale [label="Kael 'the Silent'\n(Son of Seraphina)"];
    }

    // House of the Whispering Reeds (Minor Vassal House)
    Aella_Whisperwind [label="Aella of the Whispering Reeds\n(Vassal to Sunstone)", style="filled", fillcolor="#E0FFFF"]; // LightCyan - subtle difference
    Roric_Whisperwind [label="Roric, son of Aella"];


    // === MARRIAGES & ALLIANCES ===
    // Use invisible nodes to connect marriage lines cleanly
    Marriage_Corin_Seraphina_Link [shape=point, style=invis, width=0.01, height=0.01];
    Marriage_Torvin_Aella_Link [shape=point, style=invis, width=0.01, height=0.01];


    // === FOOTER - SCRIBE'S COLOPHON / NOTES ===
    subgraph cluster_colophon {
        label="Scribal Attestations & Marginalia";
        fontname="Garamond Italic";
        fontsize=9;
        fontcolor="#704214";
        color="#C19A6B"; // Faded Brass/Camel border
        style="rounded,dashed"; // Dashed to look like an appended note section
        bgcolor="#FAF0E6"; // Main parchment, but slightly distinct by border

        SCRIBE_NOTES [
            shape=note, // To look like a different piece of parchment or annotation
            style="filled",
            fillcolor="#FFFACD", // LemonChiffon - a slightly different paper color
            color="#BDB76B", // DarkKhaki - for note border
            fontname="Segoe Print", // Or "Lucida Handwriting" if available, for a "handwritten" feel
            fontsize=7,
            fontcolor="#5C3317", // Baker's Chocolate - dark ink for notes
            label=<
            <TABLE BORDER="0" CELLPADDING="3" CELLSPACING="0" BGCOLOR="transparent" ALIGN="LEFT">
            <TR><TD ALIGN="LEFT"><B>Scribe:</B> Brother Alaric of the Silent Quill Monastery.</TD></TR>
            <TR><TD ALIGN="LEFT"><B>Source Material:</B> Fragments from the Great Library of Eldoria,</TD></TR>
            <TR><TD ALIGN="LEFT">     & Royal Archives of the Sunstone Keep.</TD></TR>
            <TR><TD ALIGN="LEFT"><B>Date of Transcription:</B> This seventh cycle of the Waxing Moon,</TD></TR>
            <TR><TD ALIGN="LEFT">     in the Year of Our Forebears, Three Thousand and Twelve.</TD></TR>
            <TR><TD ALIGN="LEFT"><I><FONT COLOR="#8B0000">(Nota Bene: Certain lines are obscured by time or deliberate erasure.)</FONT></I></TD></TR>
            </TABLE>
            >
        ];
        WATERMARK_SYMBOL [shape=plaintext, label="📜", fontcolor="#D2B48C90", fontsize=24]; // Faded scroll symbol, requires UTF-8 support
    }


    // === RELATIONSHIP LINES ===
    // Title block elements
    TITLE_ORNAMENT_TOP -> TITLE_SEPARATOR [style=invis, minlen=0.1]; // ensure very close
    TITLE_SEPARATOR -> Elara_Sunstone [style=invis, minlen=1.5]; // Space after title

    // Sunstone Lineage
    Elara_Sunstone -> Corin_Sunstone [label="child", dir=none];
    Elara_Sunstone -> Torvin_Sunstone [label="child", dir=none];
    {rank=same; Corin_Sunstone; Torvin_Sunstone;} // Siblings on same rank

    Corin_Sunstone -> Lyra_Sunstone [label="child", dir=none];

    // Shadowvale Lineage
    Malakor_Shadowvale -> Seraphina_Shadowvale [label="descendant (grandchild)", dir=none, style=dashed, color="#666666"]; // Dashed for indirect or less certain
    Seraphina_Shadowvale -> Kael_Shadowvale [label="child", dir=none];

    // Whispering Reeds Lineage
    Aella_Whisperwind -> Roric_Whisperwind [label="child", dir=none];


    // Marriages / Alliances (visual connection through the link node)
    Corin_Sunstone -> Marriage_Corin_Seraphina_Link [dir=none, constraint=false, style=dotted, color="#4682B4"]; // SteelBlue for alliance
    Seraphina_Shadowvale -> Marriage_Corin_Seraphina_Link [dir=none, constraint=false, style=dotted, color="#4682B4"];
    Marriage_Corin_Seraphina_Link -> Lyra_Sunstone [style=invis, label="Parents of Lyra", minlen=0.1]; // connect children to marriage link if desired. Often marriage is implied.

    Torvin_Sunstone -> Marriage_Torvin_Aella_Link [dir=none, constraint=false, style=dotted, color="#8FBC8F"]; // DarkSeaGreen for alliance
    Aella_Whisperwind -> Marriage_Torvin_Aella_Link [dir=none, constraint=false, style=dotted, color="#8FBC8F"];
    // No children explicitly shown from Torvin/Aella in this example

    // Vassalage (Less direct than lineage, so perhaps a different style/placement)
    // This is harder to show in pure treelike genealogy without clutter. Can be a note or separate diagram.
    // For this example, Aella's house cluster implies connection to Sunstone via label & proximity if desired.
     Aella_Whisperwind -> Corin_Sunstone [label="Vassalage", style="bold,dashed", color="#CD853F", constraint=false, dir=forward, arrowhead=empty]; // Peru - earthy tone for fealty

    // Connections to Footer
    // Ensure major lines somewhat "end" before the colophon
    Lyra_Sunstone -> SCRIBE_NOTES [style=invis, weight=10, minlen=2.5];
    Kael_Shadowvale -> SCRIBE_NOTES [style=invis, weight=10, minlen=2.5];
    Roric_Whisperwind -> SCRIBE_NOTES [style=invis, weight=10, minlen=2.5];
    {rank=sink; SCRIBE_NOTES; WATERMARK_SYMBOL;}
}
```

</details>


---

## Theme Implementation Choices

1.  **Documentation Type - Genealogy Chart:** Genealogies are common in historical manuscripts and fit the "chronicles" aspect of a scroll. They allow for structured relationships while offering space for stylistic "flourishes."

2.  **Colors & Background:**
    *   `bgcolor="#F5DEB3"` (Wheat) for the overall scroll.
    *   Node `fillcolor="#FAF0E6"` (OldLace/Linen) for individual entries, slightly lighter to stand out.
    *   Ink colors are various shades of brown/sepia (`#5C4033`, `#4A2C2A`, `#704214`, `#A0522D`), with touches of maroon (`#800000`) or dark gold (`#B8860B`) for house titles/borders, simulating different inks or minor illuminations.

3.  **Fonts:**
    *   `Garamond` as the primary readable serif.
    *   `Blackletter` (or "Old English Text MT" etc., if available) for major house titles, evoking a more formal script. `Blackadder ITC Std` for the very ornate capital letters in the main title (requires font availability).
    *   `Garamond Italic` or `Times New Roman Italic` for incidental text (like the graph label, edge labels).
    *   `Segoe Print` (or "Lucida Handwriting") for the "handwritten" scribe notes in the footer.

4.  **Shapes & Borders:**
    *   `shape=rect` with `style="filled,rounded"` for most individuals, giving a slightly softened, hand-drawn box feel.
    *   Important figures get distinct shapes (`ellipse`, `octagon`) or styles (`style="filled,bold"`) and symbolic fill colors (e.g., gold for "Radiant" matriarch).
    *   Clusters (`subgraph cluster_...`) are used to group Houses, with their own descriptive labels and slightly different background/border colors to demarcate sections.
    *   `penwidth` is generally kept thin, like ink lines.

5.  **Layout & Structure (`splines=ortho`, `rankdir=TB`):**
    *   `rankdir=TB` for a top-down genealogical flow (typical of scrolls unfurling vertically).
    *   `splines=ortho` creates right-angled connection lines, contributing to a structured, charted look common in older documents.
    *   Invisible nodes (`Marriage_..._Link`) are used to allow marriage lines to connect "horizontally" without disrupting the primary parent-child ranking.
    *   `{rank=same; ...}` is used for siblings.

6.  **HTML-Like Labels:**
    *   Extensively used for the main `TITLE_ORNAMENT_TOP` to achieve a more elaborate, multi-font title block, simulating an illuminated manuscript heading.
    *   Also used for the `SCRIBE_NOTES` in the footer to create a formatted block of text that looks like an appended note.

7.  **Edge Styling:**
    *   `arrowhead=none` for parent-child relationships is common in genealogies.
    *   `style=dotted` for marriage/alliance lines, often with a different color.
    *   `style=dashed` for less certain or indirect lineage.

8.  **Thematic Content:**
    *   Names ("Lady Elara 'the Radiant'"), house titles ("House of the Sunstone"), and descriptive labels ("Matriarch, d. 2A 876") all contribute to the ancient chronicle feel.
    *   The graph label sets the scene.
    *   The "Scribe's Colophon" in the footer adds a significant layer of authenticity, with details about the (fictional) transcription process. The use of "<I>(Nota Bene:...)</I>" is a classic manuscript annotation.

9.  **Subtleties for "Ancient" Feel:**
    *   Slight variations in parchment color for different sections (e.g., `bgcolor` of clusters).
    *   Use of Latin-esque title in the header (`Genealogia Domorum Nobilium`).
    *   The "📜" watermark (requires good UTF-8 font support in the renderer) is a direct visual cue.

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