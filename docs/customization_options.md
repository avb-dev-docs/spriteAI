---
title: Customization Options
description: A comprehensive guide to customizing sprite generation using the SpriteAI library
---

# Customization Options for SpriteAI

The SpriteAI library offers a wide range of customization options to help you generate diverse and unique sprites for your game projects. This guide will walk you through the available options and provide examples of how to use them effectively.

## Table of Contents

1. [Character Spritesheet Options](#character-spritesheet-options)
2. [Environment Sprite Options](#environment-sprite-options)
3. [Common Customization Options](#common-customization-options)
4. [Best Practices](#best-practices)

## Character Spritesheet Options

The `generateCharacterSpritesheet` function allows you to create character spritesheets with various animation states. Here are the available options:

### Animation States

You can specify the animation states for your character using the `states` option. By default, the following states are included:

- idle
- walk
- run
- attack

Example:

```javascript
const options = {
  states: ['idle', 'walk', 'run', 'attack', 'jump', 'fall']
};
```

To fetch all available animation states, use the `fetchAvailableAnimationStates` function:

```javascript
const availableStates = await fetchAvailableAnimationStates();
console.log(availableStates);
```

### Frames Per State

You can control the number of frames for each animation state using the `framesPerState` option. The default is 6 frames per state.

```javascript
const options = {
  framesPerState: 8
};
```

### Character Direction

Specify the base direction of the character using the `direction` option. The default is 'right'.

```javascript
const options = {
  direction: 'left'
};
```

## Environment Sprite Options

The `generateEnvironmentSprites` function allows you to create tileset sprites for game environments. Here are the specific options:

### Number of Elements

Control the number of distinct environment pieces in the tileset using the `elements` option. The default is 4.

```javascript
const options = {
  elements: 6
};
```

### Theme

Specify the theme of the environment using the `theme` option. The default is 'fantasy'.

```javascript
const options = {
  theme: 'sci-fi'
};
```

## Common Customization Options

These options are available for both character spritesheets and environment sprites:

### Image Size

Set the output size of the generated image using the `size` option. The default is '1024x1024'.

```javascript
const options = {
  size: '2048x2048'
};
```

### Art Style

Choose the art style for your sprites using the `style` option. The default is 'pixel-art'.

To fetch all available sprite styles, use the `fetchAvailableSpriteStyles` function:

```javascript
const availableStyles = await fetchAvailableSpriteStyles();
console.log(availableStyles);
```

Example usage:

```javascript
const options = {
  style: 'vector'
};
```

### Padding

Adjust the padding between sprites or tileset elements using the `padding` option. The default is 1.

```javascript
const options = {
  padding: 2
};
```

### Save Option

Set the `save` option to `true` to automatically save the generated spritesheet or tileset to the `assets` folder.

```javascript
const options = {
  save: true
};
```

## Best Practices

1. **Be specific in your descriptions**: Provide clear and detailed descriptions for your sprites to get the best results from the AI generation.

2. **Experiment with styles**: Try different art styles to find the one that best fits your game's aesthetic.

3. **Adjust frame count**: Increase or decrease the `framesPerState` option based on the complexity of your animations.

4. **Combine options**: Mix and match different options to create unique and diverse sprites.

5. **Use appropriate sizes**: Choose image sizes that balance quality and performance for your target platforms.

6. **Leverage themes**: For environment sprites, select themes that complement your game's setting.

7. **Post-processing**: Consider using the `removeBackgroundColor` function to refine your sprites after generation.

By utilizing these customization options and following the best practices, you can generate a wide variety of sprites tailored to your specific game requirements using the SpriteAI library.