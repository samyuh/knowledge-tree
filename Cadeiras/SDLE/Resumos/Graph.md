
# Graph
**A simple graph** is an undirected graph with no loops and more than one edge between two vertices.
**A complete graph** is one that each pair of vertices has an edge connected than (the star graph)
**A connected graph** is one that there’s a path between every two nodes.
**A star** graph is the one that has a central vertice and many leaf nodes connected to the center.
**A tree** is a graph with no cycles.
**A planar graph** is a graph that can be drawn without two edges intercepting each other.
**Degree:** number of adjavent vertices to vi. In directed graphs we also have the in-degree and the out-degree.
The **distance $d(v_i,v_j)$** between two vertices is the length of the shortest path between these.
The **eccentricity** is the **maximum distance** that a vertice might have between every point in the graph ⇒ $\max(\{d(v_i,v_j)|v_j\in V\})$
The **diameter,** on the other hand, is the maximum eccentricity that can be found in the graph ⇒ $\max(\{\texttt{ecc}(v_i) | v_i \in V\})$
The **radius** is the minimum eccentricity ⇒ $\min(\{\texttt{ecc}(v_i) | v_i \in V\})$
The **center** is a node that has the eccentricity equals to the **radius ⇒ $\{v_i | \texttt{ecc}(v_i) == R\}$**
The **periphery** is a node that has the maximum **eccentricity** in the graph. $\{v_i | \texttt{ecc}(v_i) == D\}$
In a **walk** edges and vertices can be repeated.
In a **trail** only vertices can be repeated
In a **path** no edges and no vertices are repeated.