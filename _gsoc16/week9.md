---
layout: page
title: Week 9
week: 9
---

The square was being handled separately because when the gap is a square, none of the vertices would get any features, and thus the gap would not be healed. Even with the square case, care needs to be taken such that the outer boundary (if it is a square) is not detected. So the condition to check if the external boundary is the square detected, was added. While finding the closest edge for the feature, we have routines that check if two lines intersect. It was decided earlier that the 2-D projections of the lines will be checked so as to deal with skewed lines. But this was causing the mesh to be healed incompletely. This was identified while testing with a sphere that is broken along its equator. Two opposite vertices on the equator didn't get valid feature pairs because their adjacent vertices had the same 2-D coordinates as these vertices and a feature could not be assigned. So that option was removed. Intersections are checked with the 3-D coordinates itself and skewed lines will be handled separately. Case where the mesh is already healed was tested and seen to give right results. Most dead code was cleared out. Includes were refined. Tested on different meshes modeled through Blender and exported and then imported. Code produced healed meshes, although with certain thin triangles. Testing with other models as well is going on.