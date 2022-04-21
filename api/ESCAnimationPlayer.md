<!-- Auto-generated from JSON by GDScript docs maker. Do not edit this document directly. -->

# ESCAnimationPlayer

**Extends:** [Node](../Node)

## Description

An abstraction class to expose the same animation methods for noth
AnimatedSprite and AnimationPlayer

## Method Descriptions

### \_init

```gdscript
func _init(node: Node)
```

Create a new animation player

#### Parameters

- node: The actual player node

### get\_animation

```gdscript
func get_animation() -> String
```

Return the currently playing animation
**Returns** the currently playing animation name

### get\_animations

```gdscript
func get_animations() -> PoolStringArray
```

Returns a list of all animation names
**Returns** A list of all animation names

### is\_playing

```gdscript
func is_playing() -> bool
```

Whether the animation is playing
**Returns: Whether the animation is playing**

### stop

```gdscript
func stop()
```

Stop the animation

### play

```gdscript
func play(name: String, backwards: bool = false)
```

Play the animation

#### Parameters

- name: The animation name to play
- backwards: Play backwards

### play\_backwards

```gdscript
func play_backwards(name: String)
```

Play the given animation backwards

#### Parameters

- name: Animation to play

### has\_animation

```gdscript
func has_animation(name: String) -> bool
```

Check if the given animation exists

#### Parameters

- name: Name of the animation to check
**Returns** Whether the animation player has the animation

### seek\_end

```gdscript
func seek_end(name: String)
```

Play an animation and directly skip to the end

#### Parameters

- name: Name of the animation to play

### get\_length

```gdscript
func get_length(name: String) -> float
```

Get the length of the specified animation

#### Parameters

- name: Name of the animation
**Returns** The length of the animation in seconds

### is\_valid

```gdscript
func is_valid() -> bool
```

Return true if the ESCAnimationPlayer node is valid, ie. it has a valid player
node.
**Returns: true if the ESCAnimationPlayer has a valid player node,
else false**

## Signals

- signal animation_finished(name): Emitted when the animation finsihed playing
