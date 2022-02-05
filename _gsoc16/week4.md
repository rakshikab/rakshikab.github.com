---
layout: page
title: Week 4
week: 4
---

One main concern was the determining of the closest edge for a vertex v. Checking whether a line intersects a face geometrically might not yield accurate results. So I came up with an approach.While considering an edge for the position of the closest edge, if it is still eligible (after checking for the unbounded face incidence and non-incidence on the vertex), we check if the edge's incident face contains the vertex v. If not check check for the same with the edge's twin. If either of the conditions fail, make this edge ineligible and move on to the next edge. If the 2-D projection of the line joining the vertex v to the edge intersects any face, it has to intersect another edge of the face as well. Otherwise it would mean that the vertex is inside the face, which is not possible. Thus, now we check if the 2-D projection of the line joining the vertex v to the edge intersects any of the other two edges in the triangle. If yes, then make it ineligible and move to the next edge. If the line joining the vertex doesn't intersect either of the other two edges, it is an eligible edge. So, calculate the shortest distance and update as necessary. Setting the unbounded face id to the number of faces gave rise to problems while adding and deleting faces, so it was set to zero and all the functions were updated accordingly. I will be testing my code with the 'heal' command.