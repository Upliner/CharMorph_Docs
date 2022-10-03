Best Practices
======================

.. Best Practices

Import/Export
------------

You might not like how the character you've created,
But maybe you really like other parts of it, such as the jaw and lips.
You can iterate on the same character indefinitely if you use the export morphs option.
Once you're ready to finalize your character you can use the ``export morphs`` option, and it will create a YAML file that will contain all the options you've set and can be loaded in at any time.
This allows for easy collaboration and improving the same character by tweaking values after everything is done.


Eevee & Real Time Rendering
------------

In Eevee, Some Characters such as Reom will require Refractions in order to work. 


Cycles & Offline Rendering
----------------

For Offline Renderers such as Cycles, Low polycounts can cause issues with the shading. It's advised to use the subdivision modifier.

.. image:: images/ReomSubD0.png
  :width: 480
  :alt: Reom at Subdiv 0
Reom at Subdivision Level 0, Nobody is going to be convinced by this mesh.

.. image:: images/ReomSubD1.png
  :width: 480
  :alt: Reom at Subdiv 1
Reom at Subdivision Level 1, There are some obvious shading issues on the Neck and Forehead.

.. image:: images/ReomSubD2.png
  :width: 480
  :alt: Reom at Subdiv 2
Reom at Subdivision Level 2, There are less Obvious issues but a keen eye can still notice the forehead and Chin.

.. image:: images/ReomSubD3.png
  :width: 480
  :alt: Reom at Subdiv 3
Reom at Subdivision Level 3, There are Little to No Shading Issues and everything is working as intended.
