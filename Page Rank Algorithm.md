# PageRankAlgorithm
Page rank algorithm is developed by Google and used when we would like to calculate the frequency of visiting pages. Each pages may connected to each other, but not always. It involves markov chain and linear algebra.
## Rank
Let R be the total number of web pages, P $\in \mathbb{R}^{R\times R}$

$$
P_{ij} = 
\begin{cases}
  \frac{1}{deg(j)} & \text{if node j links to node i}\\
  0 & \text{otherwise}
\end{cases}
$$

where $deg(j)$ is the total number of outgoing connections (outlinks) from j, $P_{ij}$ is the probability of following a link to node i, given that you are in node j.

If a user starts from node 2, the initial state is $\overrightarrow{x}=\[0, 1, 0, 0\]$, we multiply the P matrix and $\overrightarrow{x}$, which is a transition matrix to get the next state.
## Terminal nodes

If there is a node that have no outlinks, there is a probality that we are stucked in this page and never go to another pages.

We instead assume that we go to a random node, which means we assign a equal probaility to the node j, where j does not have outlinks.

$$
P_{'} = P + \frac{1}{R} \overrightarrow{e}\ \overrightarrow{d}^T
$$

where $\overrightarrow{e}$ = $\[1, 1, ..., 1 \]^T$ ,

$$
d_{j} = 
\begin{cases}
  1 & \text{if node j has no outlinks}\\
  0 & \text{otherwise}
\end{cases}
$$

and $\overrightarrow{e}$, $\overrightarrow{d}$ $\in \mathbb{R}^{R}$, R is the total number of web pages

## Markov Transition Matrix
We may add some randomness: At any node, we may go to a random node with probability $\alpha$

So our new transition matrix is M = $\alpha P^{'} + (1-\alpha) \frac{1}{R} \overrightarrow{e}\ \overrightarrow{e}^T$, where $\overrightarrow{e}$ = $\[1, 1, ..., 1 \]^T$ and R is the total number of web pages.
## Steady State
When surfers keep clicking, they may or may not enter a steasy state, $\overrightarrow{p} = M \overrightarrow{p}$. We can solve it using eigen value. If M has a eigen value equals to 1, it shows that the steady state exists and $\overrightarrow{p}$

We show that through Girshgorin Circle Theorem, if M is a positive Markov matrix, then we can find the solution.
