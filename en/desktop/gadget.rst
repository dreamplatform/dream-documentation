
Gadgets
*******

This document describes how to create gadgets for your service.

Gadget is basically an iframe which is shown in the Desktop.
User can enable or disable the gadgets she wants to use on her
desktop.

Each service can publish multiple gadgets for the user to use.
The gadget should be fairly simple and do only one thing. Then
the user can combine multiple gadgets the way she wants to use
them.

.. image:: gadget.png


Visibility
==========

Gadgets can be restricted to be visible only on certain
organisations or publicly to all users.


Design requirements
===================

Take these requirements into consideration when you are designing
your gadgets.

The size
--------

Gadgets live on a grid of 100x100 pixels and dimensions should be
multiples of this grid. All sizes are in grid units.

Gadget can have size restrictions:

* minimun size
* maximum size
* default size

If all three restrictions are the same then user cannot change the
size of the gadget.

Common sizes are ``3 x 4`` and ``6 x 4`` units.

Background and loading
----------------------

The desktop backround can be any color. Design your gadget accordingly.
The gadget is visible on the desktop only after it has been completely
loaded, so no progress indicator is necessary.

