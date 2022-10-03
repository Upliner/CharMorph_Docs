Character editing
==================

Base
------------
Apart from character creating CharMorph also has editing tools
that helps to integrate new characters to CharMorph.

Rigging
------------
While morphing, your character can sufficiently change proportions
so bone locations need to be adjusted too. In CharMorph this is
implemented by binding bone locations to vertex groups.

Each bone joint has a special vertex group named
"joint_{bone name}_{head|tail}". Joint location is calculated as
weighted average of locations of vertices included in the group,
optionally offseted by some constant location.
These vertex groups can be created manually using Edit mode or
weight painting, or then can be created by CharMorph rigging tools.

To use CharMorph rigging tools you need to select character mesh in
"Char" property of Rigging panel and have metarig in edit mode.

"Selected joints to VG" button moves selected joints to their
final positions according to their vertex groups.

"Recalc vertex groups" button calculates vertex group for selected
joint according to selected calculation algorighm.
If "Auto snap" option is enabled it also move the joint to
the calculated position

There are different calculation algorighms for different types of
joints. Hsually we have 3 types of joints:

* **interior joints:** the most common type of joints.
  They are located inside character mesh.
  They include limbs, spine, neck and head.

* **surface joints:** located on the surface of character mesh
  They are usually used for face expression bones

* **outer joints:** located outside of character mesh
  They are usually used for helper bones like Rigify heel bone
  You need to use offsets to make CharMorph correctly place such bones.


Calculation methods for surface joints:

* **n nearest vertices:**
  This method is usually used to snap joint to nearest vertex. In rare cases
  it also can be used to bind joint to multiple vertices also for interior joints.
* **nearest face:** snaps joint to surface of nearest face.
  It also has "snap distance" option that allows optionally to snap joint to nearest
  edge or vertex if it is within specified distance.
* **nearest edge:** snaps joint to nearest edge
* **by distance:** searches vertices within selected distance and snaps joint to them


Calculation methods for interior bones:

* **Raycast:**
  Idea of this method consists of casting of rays from joint location to 2 opposite directions
  When rays hit face surface, we calculate vertex groups for hit faces and then we assign
  certain weights to these counterpart faces to match joint location as close as possible.
  Several such ray pairs can be casted at once.
  "Raycast bone axes" uses bone axes to cast such ray pairs.
  "Raycast global" can either use global axes or use axes of selected object (usually empty)

* **Cross lines:**
  This method takes certain amount of nearest vertices and iterates over all possible lines
  that can be drawn through every pair of vertices. Then it takes n lines that are nearest
  to the joints and assigns to each pair of vertices weights to match joint location as close
  as possible.

* **Bounding box:**
  Tries to find 8 vertices that consist smallest bounding box of the joint and assign them
  weights according to joint location. Currenly this method doesn't work very good so it is
  considered experimental


Other calculation methods:

* **Current:**
  This method doesn't change vertices consisting vertex group, it only recalculates weights of
  these vertices. It works well if there is not more than 4 vertices in current vertex group.

* **n nearest joints:**
  Takes vertex groups of n already calculated joints and mixes them to match joint location
  as close as possible

* **Nearest bone:**
  Takes vertex groups of 2 joints of nearest already calculated bone and mix their vertex
  groups to snap selected joint to middle of existing bone as close as possible to current
  joint location.

* **Neighbors equal:**
  Snaps joint exactly to the center of neighbor joints (parent and child bones)
* **Neighbors weighted:**
  Snaps joints to the middle of parent and child joints as close to current joint location
  as possible

When all vertex groups are calculated you can either use these groups directly in char.blend
or you can export them to npz file and place them to
"data/characters/{your character}/joints/{rig name}.npz".
You need to use "joint\_" regular expression for exporting.
