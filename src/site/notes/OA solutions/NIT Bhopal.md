---
{"dg-publish":true,"permalink":"/oa-solutions/nit-bhopal/"}
---

# Q1 (Useful Extra Edges)
Given a graph of $A$ nodes. Also given the weighted edges in the form of array $B$.
You are also given starting point $C$ and destination point $D$.
Also given are some extra edges in the form of vector $E$.
You need to find the length of the shortest path from $C$ to $D$ if you can use maximum one road from the given roads in $E$.
**Problem Constraints**
$1 {\le} A {\le} 10^5$ 
$1 {\le} |B| {\le} 10^5$
$1 {\le} C, D {\le} A$
$1 {\le} |E| {\le} 300$
All lengths of the roads lie between 1 and 100.
## Intuition

**Central Idea:** Dijkstra from $C, D$ and check ${\forall}(u,v,d){\in}E$`

Run two instances of Dijkstra, one each from $C$, $D$.  Now, we know the shortest distance b/w every vertex and $C, D$(store them in arrays $dc, dd$ respectively). So, basically ${\forall}(u, v, d) {\in} E$, all we have to check for is that, if using this edge decreases the distance b/w $C, D$ or not, which can easily be checked by comparing the shortest distance b/w $C, D$ with $min(dc[u]+dd[v], dc[v]+dd[u])+d$, so we can just check this ${\forall}(u, v, d) {\in} E$, and give the minimum possible distance as the answer.

**Time Complexity**: $O(|B|logA)$ for each dijkstra, and $O(|E|)$ for iterating and finding the minima.

# Q2 (Hungry Policemen)
You are given a graph $G$ of $N$ nodes and $M$ edges and each edge has some time associated with it.
There is a policeman standing on each node except Node $N$.
All of then get a report that there is a thief on Node $N$ and the policemen start moving towards it, but all of them have been hungry for days, so they are looking to visit a few restaurants as well, before reaching node $N$.
There are $K$ restaurants present on some nodes, and each restaurant has some satisfaction.
Now, a policeman will only go to a restaurant if and only if the satisfaction he receives by reaching the restaurant is greater than the time he has invested in reaching there and going to the Node $N$. 
Find and return the number of policemen who will have a meal at a restaurant.
## Intuition
**Central Idea:** Dijkstra on alt graph s.t. ${\exists}(N, u, d){\in}B$ iff restaurant at $u$ and ${\not\exists} (u, N, d){\in}B$.

Simply speaking create another graph s.t ${\exists}(N, u, d){\in}B$ iff there is a restaurant at $u$ and ${\not\exists} (u, N, d){\in}B$, and $d = dist[u]-sat[u]$, here $dist[u]$ is the shortest distance b/w $N$ and $u$ and $sat[u]$ is the satisfaction of restaurant at node $u$, which can easily be found by an instance of Dijkstra. Now, this new graph can contain negative edges since it is possible that $sat[u]>dist[u]$, but it wouldn't contain negative cycles since the only edges with negative weights are leading out of node $N$, but there is no edge leading into $N$, so the negative edges can't be part of any cycle, $\implies$ there exists no negative cycle, so we can safely use Dijkstra again, and now the question is pretty simple, we just have to check if there is no additional time invested in going to a restaurant, simply speaking ${\forall}u{\in}A$, if $dist2[u]{\le}dist[u]$ then the police can stop at a restaurant else can not.
