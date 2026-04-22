## Solution

Let's say that vertices adjacent to `1` are *special*.  
Consider the graph we get if vertex `1` is removed. It will consist of multiple connected components.

If one of those components contains an odd number of special vertices, then Maria has a winning strategy, because she can just keep challenging that component to eventually force the player to get stuck. Actually, she doesn't even need any particular strategy — just making arbitrary moves will work.

On the other hand, if every component has an even number of special vertices, then the player has a winning strategy. What will happen is that Maria will challenge some special vertex, and then the player will choose some path inside the same component to another special vertex, and challenge Maria. So what we want to do is to first find a matching of special vertices with edge-disjoint paths. Then we just use these paths when Maria challenges, and we will win.

It is always possible to find a matching of special vertices with edge-disjoint paths if every connected component contains an even number of special vertices. One way to see it is to first match them arbitrarily with paths that are not edge-disjoint. Then, as long as there are two paths `s1–t1` and `s2–t2` that intersect, we can reroute the paths as:

```

s1–s2,  t1–t2

```

to make them edge-disjoint. Since the total number of used edges goes down, this can only happen at most `M` times, so eventually we will get a valid matching. However, implementing this directly will be quite slow.

To speed it up, we use a common trick: finding a matching in a general graph is equivalent to finding it in a tree. The reason is that our solution must work for trees (since it should work for any graph). If it works for trees, we can just pick any spanning tree of the graph and ignore the other edges.

So the solution is:

1. Take a spanning tree of each connected component and ignore the other edges.
2. Root each tree arbitrarily.
3. Find a matching with a simple recursive strategy.

The recursive algorithm:

- If a subtree contains an even number of special vertices, it finds a valid matching inside it.
- Otherwise, it matches as many as possible and leaves **one unmatched special vertex**, connecting it with a path to the root.

To do this:

- Run the algorithm recursively for each subtree.
- This creates unmatched vertices for each subtree with an odd number of special vertices, and possibly one at the root.
- Pair up as many of these as possible.
- This will always leave at most one unmatched vertex.

The complexity is $O(n + m)$.

Implementation is actually quite simple: we do not need to explicitly build a spanning tree and then recurse — the whole thing can be done in a single DFS.


