## Toy Design Solution

Let us process pins one by one from $1$ to $n$, and after processing pin $k$ we will know the connected components of pins $1, 2, ..., k$, as well as have designs where the first $i$ connected components are merged into one, for each $i$.

Suppose we have **u** connected components from pins $1, 2, \dots, k$ and are processing pin $k+1$. Let's denote as $f(i)$ the following boolean function: is pin $k$ connected to pin $1$ if we merge the first $i$ connected components of the first $k$ pins together. Since we already have designs for all prefix merges, we can evaluate $f(i)$ in one operation.

It's also clear that $f(i)$ is monotonic, so we can use binary search to find the smallest value of $i$ such that $f(i)$ is true, or to determine that there is no such value. There are $u+1$ possible outcomes of this binary search, so we need $\lceil \log_{2}(u+1) \rceil$ operations for it.

It's not hard to see that this value of i will be exactly the number of the connected component that the vertex $k+1$ is connected to in design $0$ (and if there is no such $i$, then it starts a new connected component). In case there is no such $i$, we will also get a new design where this new component is merged to pin $1$ as a side effect, so we need no additional operations for that.

And since $u+1 \le k+1$, the total number of operations is at most:
$$\sum_{i=1}^{n} \lceil \log_{2}i \rceil$$

