<!-- Auto-generated from JSON by GDScript docs maker. Do not edit this document directly. -->

# ESCStatement

**Extends:** [Object](../Object)

## Description

A statement in an ESC file

## Property Descriptions

### statements

```gdscript
var statements: Array
```

The list of ESC commands

### is\_finished

```gdscript
var is_finished: bool = false
```

Indicates whether this event was finished.

## Method Descriptions

### is\_valid

```gdscript
func is_valid() -> bool
```

Check whether the statement should be run based on its conditions

### run

```gdscript
func run() -> var
```

Execute this statement and return its return code

### interrupt

```gdscript
func interrupt()
```

Interrupt the statement in the middle of its execution.

### reset\_interrupt

```gdscript
func reset_interrupt()
```

Resets an interrupted event

## Signals

- signal finished(event, return_code): Emitted when the event did finish running
- signal interrupted(return_code): Emitted when the event was interrupted
