# Character Spritesheet Generation with SpriteAI

This guide provides a comprehensive overview of generating character spritesheets using SpriteAI. Learn how to create custom character animations for your game development projects with ease.

## Table of Contents

1. [Introduction](#introduction)
2. [Function Overview](#function-overview)
3. [Parameters and Options](#parameters-and-options)
4. [Best Practices for Prompts](#best-practices-for-prompts)
5. [Examples](#examples)
6. [Using Generated Spritesheets](#using-generated-spritesheets)
7. [Advanced Topics](#advanced-topics)

## Introduction

SpriteAI's `generateCharacterSpritesheet` function allows you to create detailed character spritesheets for various animation states. This powerful tool leverages AI to generate pixel art character animations based on your descriptions and specifications.

## Function Overview

The `generateCharacterSpritesheet` function is the core of character spritesheet generation. Here's its basic usage:

```javascript
import { generateCharacterSpritesheet } from 'spriteAI';

const result = await generateCharacterSpritesheet(description, options);
```

## Parameters and Options

### Main Parameters

- `description` (string): A detailed description of the character you want to generate.

### Options Object

The `options` parameter is an object that can include the following properties:

- `states` (array of strings): Animation states to generate. Default: `['idle', 'walk', 'run', 'attack']`
- `framesPerState` (number): Number of frames per animation state. Default: `6`
- `size` (string): Output size of the spritesheet. Default: `'1024x1024'`
- `style` (string): Art style of the character. Default: `'pixel-art'`
- `padding` (number): Padding between sprites. Default: `1`
- `direction` (string): Base direction of the character. Default: `'right'`
- `save` (boolean): Whether to save the generated image locally. Default: `false`

## Best Practices for Prompts

Crafting effective prompts is crucial for getting the desired results. Here are some tips:

1. Be specific about the character's appearance, including clothing, accessories, and distinctive features.
2. Mention the character's overall style or theme (e.g., "fantasy warrior," "sci-fi robot").
3. Include any specific color schemes or visual elements you want to emphasize.
4. Consider the character's personality and how it might reflect in their animations.

Example prompt:
```
"A fierce orc warrior with green skin, wearing rugged leather armor and brandishing a large battle axe. The character should have a bulky build and an aggressive stance."
```

## Examples

Here's an example of generating a character spritesheet:

```javascript
import { generateCharacterSpritesheet } from 'spriteAI';

const description = "A nimble elven archer with long blonde hair, wearing a green tunic and brown leather boots. The character should have a slender build and carry a wooden longbow.";

const options = {
  states: ['idle', 'walk', 'run', 'attack', 'jump'],
  framesPerState: 8,
  size: '2048x2048',
  style: 'pixel-art',
  direction: 'right',
  save: true
};

const result = await generateCharacterSpritesheet(description, options);

console.log(result.metadata);
console.log(result.spritesheet); // Base64 encoded spritesheet
```

## Using Generated Spritesheets

After generating a spritesheet, you can use it in your game development project. Here's a basic example of how to use the spritesheet in a game engine:

1. Load the spritesheet image into your game engine.
2. Use the `metadata` from the result to set up your animation system:

```javascript
const { frameData, framesPerState, dimensions } = result.metadata;

// Set up animations for each state
Object.entries(frameData).forEach(([state, data]) => {
  const { startFrame, endFrame } = data;
  game.addAnimation(state, result.spritesheet, startFrame, endFrame, framesPerState);
});

// Set sprite dimensions
const frameWidth = dimensions.width / framesPerState;
const frameHeight = dimensions.height / Object.keys(frameData).length;
game.setSpriteSize(frameWidth, frameHeight);
```

## Advanced Topics

### Custom Animation States

You can fetch available animation states using the `fetchAvailableAnimationStates` function:

```javascript
import { fetchAvailableAnimationStates } from 'spriteAI';

const availableStates = await fetchAvailableAnimationStates();
console.log(availableStates);
```

### Different Art Styles

Explore different art styles using the `fetchAvailableSpriteStyles` function:

```javascript
import { fetchAvailableSpriteStyles } from 'spriteAI';

const availableStyles = await fetchAvailableSpriteStyles();
console.log(availableStyles);
```

By leveraging these advanced features, you can create more diverse and customized character spritesheets for your game development projects.