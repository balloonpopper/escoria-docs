Create a second room
====================
So a one room game is a good start, but your adventure game will be a lot more
interesting when there are other rooms to travel to. Let's create a park scene
and link it to the pub scene so we can walk between them.

As we've already created the first scene, follow the same steps you used on the
:doc:`create a room <3_create_room>` page to create this scene.

* Create a new folder in your rooms folder and call it "park"
* Create a new Godot scene named "room02" and set ``ESCRoom`` as its root node.
  * Note that you could call it something other than room02, we're just being
  consistent with the first room.
* Give the room a global id (``park``)
* We still want to play as Graham in this scene, so select it as the
  ``player scene`` parameter.
* Add an ESCBackground node for the room graphics as a child of the root node.
* From ``backgrounds.zip``, copy the ``park_bg.png`` file to the **rooms**
  directory and set it as the ``texture`` parameter in the ``ESCBackground``
  node.
* Create a walkable area for the character. Add an ``ESCTerrain``
  node to the ``ESCRoom`` node. Add a
  ``NavigationPolygonInstance`` node as a child of the new ``ESCTerrain`` node.
* Create a NavigationPolygonInstance resource for the Navpoly parameter.

.. image:: img/create_room_terrain_navpoly2.png
   :alt: Adding a NavPoly

* Use the editor window to draw a polygon. This polygon is the area in which
  the character can move around freely.

.. image:: img/create_room_terrain_createdpoly2.png
   :alt: View of the completed polygon on the background

Creating a light map
--------------------

For this room we're going to use a light map. As mentioned previously, light
maps are used to shade different areas of the room differently. In this room,
we have a lamp, so we want the player to be brightly lit when under it, and
less brightly lit when away from the light source.

The example light map provided is a very simple one with just 3 colours to make
it easier to demonstrate how the light map changes how the game character
looks, but you could replace it with one that uses a gradient to fade nicely
from white to mid-grey. Coloured ones can also be used to simulate things like
concert or traffic lights.

Copy the park_lightmap.png asset (link on the main step-by-step page) to the
room02 folder.

In the Godot GUI, select the ``ESCTerrain`` node, and set its light map to the
`park_lightmap.png` texture.

Room exits in Escoria
---------------------

To link room 2 (the park) to room 1 (the pub), you will need an exit node. When
the player clicks this, it tells Escoria that you want to change rooms. Each
Escoria room can have multiple exits.

There are 2 different nodes for creating exits in Escoria. The first is an
:doc:`ESCItem </api/ESCItem>`. By selecting the "Is Exit" checkbox when you
create an ``ESCItem`` node, Escoria will look for a ":exit_scene" event in the
attached script file. Any commands you place in the ":exit_scene" event will be
run when the player chooses to "use" the exit - for example, saying a goodbye,
or running a cutscene. Place a "change_scene" command as part of this event to
move the character to the next room.

For exits that don't require scripts, the :doc:`ESCExit </api/ESCExit>` node is
provided. The only things you will need to configure on the node are the
"target_scene" to change to, and optionally, a "switch sound" (the sound to
play when changing rooms).

For both ``ESCExit`` and ``ESCItem`` nodes:
* A child ``CollisionPolygon2D`` node is used to define where the player needs
to click to activate the exit.
* When the exit is activated, the character will automatically walk to a
``ESCLocation`` node that is a child of the ``ESCItem`` / ``ESCExit`` node.

Create a doorway back to the pub room
-------------------------------------

* Create an ``ESCExit`` node as a child of the room and give it a "Global ID"

Under the ESCroom node, create an ESCexit node.

.. image:: img/create_room_esc_exit.png
   :alt: The ESC exit node.

Set its Global ID to "exit_to_pub".

* Create a CollisionPolygon2D for the exit

Create a CollisionPolygon2D as a child of the ESCexit. Use the editor window to
draw a rectangle covering the left-hand-edge of the park background. This
polygon is the area which will act like a "door" for the player to click on to
change rooms. (If the room had a doorway, you'd draw the polygon around the
door instead).

.. image:: img/create_room_park_exit.png
   :alt: The ESCexit polygon.

* Create an ESCLocation

When the player clicks on the exit's collision polygon, Escoria needs to know
where to make the character walk to in order to leave the room.

Create an ``ESCLocation`` as a child of the ``ESCexit``. Give this location the
``Global ID`` of "park_exit".
Move the ``ESCLocation`` to the left hand side of the park somewhere on the
road/path. This will be where the character walks to to leave the park.

.. hint::

   Make sure the ESClocation is inside the walkable area navigation polygon.

.. image:: img/create_room_exit_location.png
   :alt: The doorways exit point.

* Set up the tooltip for the exit

When you put the mouse over the exit, you want the tooltip in the UI to tell
you what object your mouse is over. Additionally you want to set the
interaction with this exit that will happen by default to make the experience
better for the player. Under ``Tooltip name`` put "Exit to pub", and under
``Default Action`` put "use".

.. image:: img/create_room_esc_exit2.png
   :alt: Settings for the ESCExit node.


* Set the destination scene for the exit

Further down in the ESCExit's settings, select the Target scene. Clicking this
will take you to a file explorer where you can choose the room you want the
character to be sent to when the player clicks on this exit. Locate the
pub scene and select that. (If you had a noise to play like a door closing when
the player used this exit, you would use the "Switch sound" parameter to set
it).

.. image:: img/create_room_esc_exit3.png
   :alt: Scene setting for the ESCExit node.

Set up a doorway in the pub room
--------------------------------
If you played the game now, you'd find it was a bit broken. The game would
start in the pub room, but you'd have no way to leave it to get to the park.
If you were somehow able to get to the park and tried to get back, the game
wouldn't know where in the pub to place your character.

Lets fix this by creating a doorway in the pub and make it so that using it
takes you to the park, and clicking on the edge of the park brings you back to
the pub's doorway.

The process here will be the same process we followed in the park.

Load your pub.tscn scene in the Godot editor.

Create an ESCexit as a child of the ESCRoom. Give it a Global ID of
"pub_door". Set its ``Target scene`` to park.tscn. This will send the player to
the park when they click the door.

Create a CollisionPolygon2D as a child of the ESCExit. Draw the
polygon around the doorway. This defines where you can click to
activate the exit to leave the pub and go to the park.

.. image:: img/create_room_pub_door.png
   :alt: The polygon you click to leave the room.

When you created the pub room you set an ESClocation for the characters
starting point (e.g. at the bottom of the stairs). If the player comes back
into the pub from the park scene, they should be at the doorway rather than
appear at the bottom of the stairs. We therefore need an ``ESCLocation`` at the
doorway that we can send them to.

Create a new ESClocation as a child of the pub's ESCExit. Set its
``Global ID`` to "pub_exit". This will be where the user appears
when they come into the pub from the park. Place its marker
just under the doorway. This wil also be where the character walks to
when you click the door to leave the pub.

.. hint::

   Make sure the ESClocation is inside the walkable area polygon.

.. image:: img/create_room_pub_door_location.png
   :alt: The location the player will appear at when they come in the door.

Configure the change between rooms
----------------------------------
What we now need is to tell Escoria to move the character to the correct
location when they change between rooms. For this we will use a script that
will run when the room first loads. It will check which room the player has
come from and immediately send them to the correct ``ESCLocation``.

Create a new ESC script "room_pub.esc" and attach it as
the ``ESC script`` on the pub room's ``ESCRoom`` node. This is the script the
room will open when it starts.

.. image:: img/create_room_pub_script.png
   :alt: The script the room will open when it starts.

Add the following code to room_pub.esc

.. code-block::

    > [eq ESC_LAST_SCENE room_park]
       teleport player pub_exit
       # Set player look left
       set_angle player 180

This code says
1) Check (">") if the last room you were in (ESC_LAST_SCENE) is (eq) "room_park"
2) If so, "teleport" the "player" to the ``ESClocation`` called "pub_exit"
3) Then make the player face left

Now follow the same process to create an ESC script called "room_park.esc".
Load the park scene and configure "room_park.esc" as the ``ESC script`` on the
park room's ``ESCRoom`` node. This is the script the park room will open when
it starts.

Add the following code

.. code-block::

    > [eq ESC_LAST_SCENE pub]
       teleport player park_exit
       # Set player look right
       set_angle player 90

Test the scene. You should now be able to click on the door to leave the pub -
you will appear in the park. If you click on the left hand side of the park
you will appear in the doorway of the pub.

Additionally, due to the light map configured for the park scene, you should be
in shadows when you walk in the park, and get lighter when you walk under the
light.

Creating an exit using an ESCItem instead of an ESCExit
-------------------------------------------------------
As mentioned earlier, for more complex exit sequences, an ``ESCItem`` is used
rather than an ``ESCExit``.

If you wanted to create the pub door using an ``ESCItem`` you would:
* Create an ``ESCItem`` as a child of the ``ESCRoom``. Give it a Global ID of
"pub_door_item".
* Create a new ESC script file
and call it "pub_exit.esc". Where you place this file is up to you and how
it makes sense with your project. You might choose to store it with the
room, or keep all your game's scripts together in a "scripts" folder.
* In pub_exit.esc, add an ``:exit_scene`` event to our ESC file and within it,
use the ``change_scene`` command to make the game switch from this pub room to
the  park room when the player "uses" the exit. You would add any other
animation / dialog / etc to this script that you want to be played when
the player activates the exit. e.g.

.. code-block::

    :exit_scene`
    say player "I'm leaving now."
    change_scene "res:///rooms/park.tscn"

* Change the "Esc Script" of the ESCItem to point to your script so Escoria
  runs the code you've just written when the user exits the scene using this
  node.

