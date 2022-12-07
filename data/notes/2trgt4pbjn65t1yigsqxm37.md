
## Summary

This page outlines visual styling workarounds with Mermaid.

## Flowchart Font Size

Change the font size of Flowchart content. Note that the Mermaid client or other renderings may not strictly obey the changed font-sizes, sometimes resulting in unchanged image exports.

_Original (small font)_

```mermaid
flowchart LR
    subgraph sub_graph1[Subgraph]
        direction LR
        Start --> Stop
    end
```

_Updated with Font Size Adjusted_

```mermaid
flowchart LR
    subgraph sub_graph1[<font size=5>Subgraph]
        direction LR
        Start[<font size=5>Start] --> Stop[<font size=5>Stop]
    end
```

## Flowchart Subgraph Padding or Margin

Add padding or margin within subgraphs for readability or design aesthetic improvements.

_Original (subgraph readability challenges)_

```mermaid
flowchart LR
    subgraph sub_graph1[Subgraph]
        direction LR
        subgraph sub_graph2[A]
            Start --> Stop
        end
        subgraph sub_graph3[B]
            Outlier --> Stop
        end
    end
```

_Updated with Padding or Margin Added_

```mermaid
flowchart LR
    subgraph sub_graph1[Subgraph]
        subgraph subgraph_padding1[ ]
            direction LR
            subgraph sub_graph2[A]
                Start --> Stop
            end
            subgraph sub_graph3[B]
                Outlier --> Stop
            end
        end
    end

classDef subgraph_padding fill:none,stroke:none;
class subgraph_padding1 subgraph_padding
```
