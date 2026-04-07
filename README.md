# GodotDebugMenu
A basic menu which can be added to any Godot project to perform monitoring and basic changes to variables while running

# Installation
1. Copy all files to a folder of your choosing
2. Add an autoload named DebugMenu using script debug_menu.gd with global variable enabled
3. Add a custom input map with any name or input desired that will be used to toggle the menu's visibility
4. Open debug_menu.gd and edit the following variables:
  - TOGGLE_INPUT_MAP  :  put the name of the action created in step 3 here
  - DEFAULT_MENU_VISIBLE  :  set to true if you don't want the menu to be hidden by default when the project runs
  - DEFAULT_FPS_COUNTER  :  set to false if you don't want the menu to contain an FPS counter by default
  - _loaded_ui_scene  :  update the preload path to debug_menu_ui.tscn
  - _loaded_item_scene  :  debug_menu_item.tscn

# Use in Code
The only thing that needs to be done in code is to run one of four commands targeting the autoload. For example if you had a node with a "var walking_speed: float" and wanted the menu to show a live update of that value, you run the following anywhere you like (though I recommend in _ready())
  - DebugMenu.add_viewing_item("Walking Speed", self, "walk_speed")

And that's it, the menu will be instantiated and take things from there. Some items you may want to categorize into groups which can be done by adding a group_id to any of the four main commands like
  - DebugMenu.add_viewing_item("Walking Speed", self, "walk_speed", "Player")

# Methods
add_viewing_item(id, target_node, property, group_id)
  - Creates a simple item which displays a name (id) with the updated value (property) from the node (target_node). This supports any variable which can be converted to a string

add_range_item(id, target_node, property, min, max, step, group_id)
  - Works as the viewing item but a slider can be used to change the value on the target_node, the slider will be built with the min, max, and step provided. Only supports int and float variables

add_toggle_item(id, target_node, property, group_id)
  - Works as the viewing item but a check button can be used to swap the variable between false and true. Only supports bool variables

add_trigger_item(id, target_node, method, group_id)
  - Creates an item which displays a name (id) and a button that can be used to activate the callable (method) for the targeted node (target_node). Only supports functions without any mandatory variables, and cannot pass variables to the function.

show_fps_counter()
  - If the FPS counter is not visible, show it

hide_fps_counter()
  - If the FPS counter is visible, hide it

# Modification
- debug_menu_theme.tres can be updated as desired to change the look and feel of all the items that will be contained in the menu including things like font speed.
- The menu spawns on the top-left corner, you can easily modify this by going into debug_menu_ui.tscn and changing the root node's Anchors Preset. I attempted to change this in code, but it never produced the same results as changing it in the editor did
