---
layout: page
title: Week 12
week: 12
---

This week i started with making a few small but essential changes to the code, like taking in the tolerance as a user input rather than hard-coding it, etc. I ran into a few build errors for a while, but resolved them soon. When i had been testing my code with a torus, it hung even before the healing started - precisely in the function to find the free edge chain. This was slightly unusual, i'd run into errors before only after at least one round of healing. So when i was debugging, as per Daniel's suggestion i looked into the init functions for the previous and the next edge. As Daniel had pointed out, they needed to be done in the same function, but i had done them separately. So after modifying that, the previous and next edge references were being set wrong because of errors with the incident face references. And that came because of orientation inconsistencies. This was because of the inside-outside orientation inconsistency. With a torus, if the orientation is being calculated with respect to the origin, this error will arise. To this Daniel suggested that i take a different approach to setting the DCEL, by starting with a triangle and moving on to other triangles and just flipping the common edges. He also added that the issue would be when there are multiple connected components. Another error that i had come across was that, when a mesh was healed using the heal command and if the command was called again on the mesh, the algorithm hung. This i noticed arose due to the presence of singular vertices. And singular vertices were introduced because the meshes were not being healed completely. There seems to be some floating point precision error while computing the orientation. As a temporary fix, since this case is prevalent with triangles (thin ones - needles/caps), a separate case for triangles has been added where the vertex which can be orthogonally projected on to the opposite edge and has the least distance to the opposite edge is taken as the vertex (with the opposite edge as the feature edge) and edge contraction is performed. As this does not extend to free edge chains with four or more vertices, those might still be not healed.