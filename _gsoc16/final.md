---
layout: page
title: GSoC ’16 final submission
week: 13
---

Automatic Polygonal Mesh Healing
The first part of the project was to come up with the methodology of the portable module for the mesh healing that can be used by not just BRL-CAD. After discussions with the BRL-CAD and OpenSCAD mentors, it was decided that there’d be an abstract class that would behave as a geometry storage structure, directly accessing the native structures, and a geometry processing structure – Doubly Connected Edge List that would help with the healing operations.

Coming up with this idea took a long time as it needed clarity on the kind of operations that would be performed. Discussions with the organization helped tremendously.

The next step was implementing the zippering module. This module would take care of gaps and T-joints.

![Gaps in a mesh](/assets/gsoc/gapsinamesh.png)

**Fig: Gaps in a mesh**

A priority queue was used to maintain which vertex would be healed next in a given free edge (an edge with just a single face incident on it) chain. 

Initially the unbounded face was given the index equal to the number of faces in the mesh. But as the mesh would keep changing, this proved cumbersome, hence it was set to zero.

The main challenge of this module was a routine, that aims to find the closest edge to a vertex, which is valid. A valid edge has a lot of properties that include:

Not being incident on the vertex for which closest edge is being calculated
Not disrupting any of the existing orientations of the other triangles
Not intersecting the interiors of the edges of other triangles, etc.
Any small mishap in the function, and you would get a distorted mesh as a result. This routine needed a lot of time and precision. As the weeks progressed, new validity conditions kept coming up and they had to be added.

Checking and setting references properly in the DCEL proved quite tougher than expected. They had been overlooked initially as they seemed quite trivial. But when invalid memory reads started occurring, those were taken care of.

A lot of memory issues arose that took quite some time to resolve. The function signatures initially made the caller responsible for the deallocation of memory. They were changed and made better by performing the deallocation inside the function itself.

The routines had to be modified very frequently. This would happen when some degenerate case popped up that would put the DCEL out of place and hence make the algorithm hang.

Special cases needed to be identified and handled separately. One such instance is a square hole. For more information, check the Week 9 entry in the blog. Initially, the intersection of lines was checked by checking for the intersection the lines projected onto the x-y plane, but that proved erroneous. So intersections were checked in 3-D and they were checked for co-planarity as well (essentially taking care of skewed lines).

One issue is the consistency of the orientation of the triangles. The origin needs to be inside the object for the orientation of all the triangles to be consistent. As my mentor, Daniel had suggested, initially while setting the DCEL, it can be done by starting with a triangle and moving on to neighbouring ones while just flipping the common edges. He also added that this will have issues when there are more than one connected components. Also, the orientation routine in the function is used in other places as well, like finding if two lines intersect, etc. Those will have issues too, then.

Code yet to be merged. The stitching, overlaps, holes modules are left to be implemented.

# Related links:

Project proposal: [GSoC ’16 Project Proposal](https://drive.google.com/file/d/0B7N8x571Yp6VNnlPQXRvMEk0VmM/view?usp=sharing)

The complete algorithms for all the modules can be found at: [Project plan](https://docs.google.com/document/d/1rz8FbiISoFTnqXcAF5JDX6kjhK7XRHgzLFL3ZCaOYbU/edit?usp=sharing)

My daily development logs: [Development Logs](http://brlcad.org/wiki/User:Tandoorichick/GSoC2016/Logs#Development_Logs)

Ticket thread of patches I maintained on Sourceforge (includes the latest one): [Zippering module](https://sourceforge.net/p/brlcad/patches/448/)

Public folder of all the patches: [Patches](https://drive.google.com/drive/folders/0B7N8x571Yp6VNGtEcVZyazJpSjg?usp=sharing)

Folder with screenshots of the results obtained: [Results’ screenshots](https://drive.google.com/drive/u/0/folders/0B7N8x571Yp6VY0xIdUdFSVE0blk)

Final patch: [Zipper Module Patch](https://drive.google.com/file/d/0B7N8x571Yp6VeE1HbVBhR0p6M00/view?usp=sharing)

Mail to the BRL-CAD mailing list: [Mail to the organization](https://sourceforge.net/p/brlcad/mailman/message/35295497/)