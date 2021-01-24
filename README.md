<h1>CUDA GPU-parallelized BFS to cache all possible gene insertions.</h1>
<p>In metabolic engineering, we want to find optimal ways to add or delete genes to microorganisms to achieve our goal for production of a certain compound.
One way to achieve this is to cache all possible shortest appendable reaction sequences, indexing them by the sequence's first and final compounds, as they both will be present in the network.
There is also usually a maximum on gene insertions (i.e. 3), meaning that caching can feasible in terms of RAM usage.</p>
<p>To complete this caching, one can use a shortest-path graph algorithm on a graph of all possible relevant reactions with metabolites as nodes.
As such graphs are usually very sizeable, we may speed up the process by paralellizing the algorithm with a GPU. Since the algorithm can find the minimum
distance for all metabolites at once, we can simply run computation on each metabolite of a network in parallel.</p>
<p>Let us assume that we don't need to weight the graph (which we most probably won't). That way, with N being the metabolites of a metabolic network,
and V and E being the metabolites and reactions of the reaction database, assuming a connected graph, we can drop the time complexity
from O(N^2*(V + E)) to O(kN*(V+E)), where k is N / num. of CUDA cores. In the case of Google Colab with their Nvidia Tesla T4 GPU with 2560 CUDA cores, k could very well be less than 1.</p>
