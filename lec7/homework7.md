# Lecture 7
### 吴昊 2016K8009929015

###1.1 Acyclic subgraph
Give a factor 1/2 algorithm for the following. Given a directed graph G = (V, E), pick a maximum cardinality set of edges from E so that the resulting subgraph is acyclic.
**Solve**:
Arbitrarily number the vertices and devide the edges into two sets, the forward-going edges F and the backward-going edges B. Pick the bigger set, denoted by S.
Obviously, edges in F or B will not form a cycle, because a cycle needs at least a forward-going edge and a backward-going edge. 
$$|F|+|B|=|E|\\S=max\{F,B\}\ge \frac{1}{2}|E|$$
And we have $OPT<|E|$, hence
$$|S|\ge \frac{1}{2}OPT$$

### Vertex Cover and DFS tree
1.3 (R. Bar-Yehuda) Consider the following factor 2 approximation algorithm for the cardinality vertex cover problem. Find a depth first search tree in the given graph, G, and output the set, say S, of all the nonleaf vertices of this tree. Show that S is indeed a vertex cover for G and |S| ≤ 2 · OPT
**Solve**
First we prove that S is a vertex cover. Assume that there exists an edge $<u,v>$ in G and not covered by S. Since all nonleaf vertices in DFS tree are in S, u and v must be leaf vertices. This is contradictory to the definition of DFS tree, hence S is indeed a vertex cover.
Then we show the ratio is $\frac{1}{2}$. Construct a matching set T in the following way.
```{.line-numbers}
initialize T = NULL
denote by D the nonleaf vertices in DFS tree
while D is not empty do
    choose vertex v in D closest to root
    if v has a nonleaf child u in DFS tree
        add match <v,u> to T
        remove u,v from D
    else
        (then v's children are leaf vertices)
        add <v> to T as unmatched single vertex
endwhile
return T
```
Note that the match T is different from maximum match problem, here we allow unmatched single vertex because we have ignore leaf vertices from the origin graph G. To cover edges joint with leaf vertices, we have to include all unmatched single vertices in T. For all matches in T,at least one of its endpoint is included in vertex cover. Therefore the ratio is $\frac{1}{2}$.


