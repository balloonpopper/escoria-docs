<!-- Auto-generated from JSON by GDScript docs maker. Do not edit this document directly. -->

# PrintCommand

**Extends:** [ESCBaseCommand](../ESCBaseCommand) < [Node](../Node)

## Description

`debug string [string2 ...]`

Prints a message to the Godot debug window.
Use this for debugging game state.

**Parameters**

- *string*: The string to log

@ESC

## Method Descriptions

### configure

```gdscript
func configure() -> ESCCommandArgumentDescriptor
```

Return the descriptor of the arguments of this command

### run

```gdscript
func run(command_params: Array) -> int
```

Run the command