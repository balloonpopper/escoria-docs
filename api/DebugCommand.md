<!-- Auto-generated from JSON by GDScript docs maker. Do not edit this document directly. -->

# DebugCommand

**Extends:** [ESCBaseCommand](../ESCBaseCommand) < [Node](../Node)

## Description

`debug string [string2 ...]`

Prints a DEBUG-level message to the log.

**Parameters**

- *string*: One or more strings to log

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