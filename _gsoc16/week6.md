---
layout: page
title: Week 6
week: 6
---

I continued testing this week. Quite a few modifications had to be made to the vertex contraction and edge contraction procedures. Checking and setting twins for edges that have been modified. This function takes in a vertex and gets the two edges containing this vertex, with the unbounded face incident on them. For both edges, it is checked whether the edge and its other neighbour need to be squeezed out from the boundary chain. So essentially we delete either 0/2/4 edges. By squeezing out, what is meant is removing the edge from the boundary chain and setting the references of the affected edges properly. This function was called from the previous function, after checking whether that would be needed. While deleting any record (vertex/edge/face), the references of the other affected records needs to be set right. And the IDs of the vertex list and face list need to be updated too.