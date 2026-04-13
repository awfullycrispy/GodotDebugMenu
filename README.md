# DebugMenu for Godot
DebugMenu is a simple add-on that allows you to easily create a menu in runtime using a single line of code that allows you to live monitor and edit variables

Created by awfullycrispy for Godot 4.6 in 2026. CC0-1.0 license

# Setup
1. Make an "addons" folder and copy the "debug_menu" folder to it
2. Create a gloabl autoload named DebugMenu with debug_menu.gd as its script
3. If you stored the debug_menu folder anywhere other than the addons folder, edit the constant FOLDER_PATH at the top of debug_menu.gd

# Customization
1. Change the look of your menu by editing debug_menu_theme.tres
2. Change which corner the menu loads in at by changing the Anchors Preset at the root node on debug_menu_ui.tscn
3. To change the key used to toggle the menu, edit the constant TOGGLE_INPUT_MAP at the top of debug_menu.gd
4. To have the menu be visible by default, edit the constantant DEFAULT_MENU_VISIBLE at the top of debug_menu.gd
5. To disable the FPS counter, edit the constantant DEFAULT_FPS_COUNTER at the top of debug_menu.gd

# Usage
In any script, usually in a node's _ready() function, run any of the following commands. Any instance of group_id is optional and will categorize items in the menu under specific named sections

--

	add_viewing_item(id, target_node, property, group_id)
Creates a simple item which displays a name (id) with the updated value (property) from the node (target_node). This supports any variable which can be converted to a string 

--

	add_range_item(id, target_node, property, min, max, step, group_id)
Works as the viewing item but a slider can be used to change the value on the target_node, the slider will be built with the min, max, and step provided. Only supports int and float variables

--

	add_toggle_item(id, target_node, property, group_id)
Works as the viewing item but a check button can be used to swap the variable between false and true. Only supports bool variables

--

	add_trigger_item(id, target_node, method, group_id)
Creates an item which displays a name (id) and a button that can be used to activate the callable (method) for the targeted node (target_node). Only supports functions without any mandatory variables, and cannot pass variables to the function.

--

	show_fps_counter()
If the FPS counter is not visible, show it

--

	hide_fps_counter()
If the FPS counter is visible, hide it


# Examples
you haved a node with a "var walking_speed: float"  and wanted the menu to show a live update of that value, you would run the following line in the code of the object itself

	DebugMenu.add_viewing_item("Walking Speed", self, "walk_speed")

--

after instantiating a new scene, you want to run code from the instantiating script and add an item to edit the boolean variable "can_run" live, and want it organized in a "Player" category

	var new_player = player.instantiate()
	$node.add_child(player)
	DebugMenu.add_toggle_item("Can Run", player, "can_run", "Player")



