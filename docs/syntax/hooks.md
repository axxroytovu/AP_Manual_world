# Using Hooks to Modify your Games

## Overview

Removing locations should be done in [after_create_regions](#after_create_regions)

## Hook info by file

### World.py

The most common hooks to edit are in the `World.py` file.

#### before_create_regions

This hook allows you to interact with the set of regions and locations before they are created.

There are no common use cases for this hook.

#### after_create_regions

This hook allows you to interact with the regions and locations after they are created.

This is the correct point to remove or modify a location in the multiworld.

Regions can be accessed in the list `multiworld.regions`. Each region's player can be checked using `region.player == player`.

Inside each region, you can access locations inside the `region.locations` list. Removing a location from this list removes it completely from the multiworld.

#### before_create_items_starting

This hook allows you to interact with the item pool before starting items are processed.

#### before_create_items_filler

This hook allows you to interact with the item pool after starting items are processed, but before filler items are created.

This is the best place to remove items from the multiworld, since the `add_filler` function will correctly replace the removed items with filler.

#### after_create_items

This hook provides the final item pool after filler items are added and starting items are removed.

#### before_set_rules

This hook is called before rules are created.

There are no common use cases for this hook.

#### after_set_rules

This hook happens after the rules for each location are created.

Use this hook to modify the access rules for a given location

```
def Example_Rule(state: CollectionState) -> bool:
    # Calculated rules take a CollectionState object and return a boolean
    # True if the player can access the location
    # CollectionState is defined in BaseClasses
    return True
```

Common functions:
- `location = world.get_location(location_name, player)`
- `location.access_rule = Example_Rule`

Combine rules:
`old_rule = location.access_rule`
`location.access_rule = lambda state: old_rule(state) and Example_Rule(state)`
`location.access_rule = lambda state: old_rule(state) or Example_Rule(state)`

## Json File Hooks

## Options Hooks
