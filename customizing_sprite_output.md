---
title: Customizing Sprite Output in SpriteAI
description: Learn how to customize sprite output using various options and parameters in SpriteAI.
---

# Customizing Sprite Output in SpriteAI

SpriteAI provides powerful customization options for generating sprite sheets and environment sprites. This guide will walk you through the various ways you can adjust your sprite output to meet your specific needs.

## Customizing Character Spritesheets

When using the `generateCharacterSpritesheet` function, you can customize several aspects of the output. Let's explore the available options:

### Adjusting Animation States

By default, SpriteAI generates sprites for four animation states: idle, walk, run, and attack. You can customize this by providing your own array of states:

```javascript
const options = {
  states: ['idle', 'jump', 'crouch', 'swim'],
  // other options...
};

const result = await generateCharacterSpritesheet('ninja character', options);
```

This will generate a spritesheet with the specified animation states instead of the default ones.

### Modifying Sprite Dimensions

You can adjust the size of the generated spritesheet using the `size` option:

```javascript
const options = {
  size: '2048x2048', // Generates a larger spritesheet
  // other options...
};
```

### Changing Art Style

SpriteAI supports different art styles. You can specify the style using the `style` option:

```javascript
const options = {
  style: 'vector', // Changes the art style to vector graphics
  // other options...
};
```

Available styles include 'pixel-art', 'vector', '3d', 'hand-drawn', and 'anime'.

### Fine-tuning Generation Parameters

Other parameters you can adjust include:

- `framesPerState`: Number of frames for each animation state
- `padding`: Padding between sprites
- `direction`: Base direction of the character

Example:

```javascript
const options = {
  framesPerState: 8,
  padding: 2,
  direction: 'left',
  // other options...
};
```

## Customizing Environment Sprites

For environment sprites, you can use the `generateEnvironmentSprites` function with various customization options:

### Adjusting Number of Elements

Control the number of distinct environment pieces:

```javascript
const options = {
  elements: 6, // Generates 6 different environment elements
  // other options...
};

const result = await generateEnvironmentSprites('forest scene', options);
```

### Changing Theme

Specify a theme for your environment:

```javascript
const options = {
  theme: 'sci-fi', // Changes the theme to science fiction
  // other options...
};
```

## Examples of Customization Effects

Here are some examples of how different options can affect the final output:

1. Default character spritesheet:
   ```javascript
   const result = await generateCharacterSpritesheet('warrior');
   ```
   This will generate a 1024x1024 pixel art spritesheet with 4 animation states and 6 frames per state.

2. Customized character spritesheet:
   ```javascript
   const result = await generateCharacterSpritesheet('mage', {
     states: ['cast', 'teleport', 'shield', 'meditate'],
     style: 'anime',
     size: '2048x2048',
     framesPerState: 8
   });
   ```
   This will create a larger, anime-style spritesheet with custom animation states and more frames per state.

3. Detailed environment tileset:
   ```javascript
   const result = await generateEnvironmentSprites('underwater city', {
     elements: 8,
     style: '3d',
     theme: 'futuristic',
     size: '2048x2048'
   });
   ```
   This generates a high-resolution 3D tileset with 8 distinct elements for a futuristic underwater city theme.

By leveraging these customization options, you can fine-tune SpriteAI's output to perfectly match your game's visual style and technical requirements.