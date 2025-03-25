# SpriteAI API Reference

This document provides a comprehensive API reference for the SpriteAI module, detailing all public functions, their parameters, return values, and usage examples.

## Table of Contents

1. [generateCharacterSpritesheet](#generatecharacterspritesheet)
2. [generateLandscapeSprite](#generatelandscapesprite)
3. [fetchAvailableAnimationStates](#fetchavailableanimationstates)
4. [fetchAvailableSpriteStyles](#fetchavailablespritestyles)
5. [generateEnvironmentSprites](#generateenvironmentsprites)

## generateCharacterSpritesheet

Generates a character spritesheet based on a given description and options.

### Parameters

- `description` (string): A description of the character to generate.
- `options` (object, optional): Configuration options for the spritesheet generation.
  - `states` (array of strings, default: `['idle', 'walk', 'run', 'attack']`): Animation states to generate.
  - `framesPerState` (number, default: 6): Number of frames per animation state.
  - `size` (string, default: '1024x1024'): Output size of the spritesheet.
  - `style` (string, default: 'pixel-art'): Art style of the spritesheet.
  - `padding` (number, default: 1): Padding between sprites in pixels.
  - `direction` (string, default: 'right'): Base direction of the character.
  - `save` (boolean, default: false): Whether to save the generated image to disk.

### Returns

An object containing:
- `original` (string): URL of the original generated image.
- `spritesheet` (string): Base64-encoded PNG data of the processed spritesheet.
- `metadata` (object): Metadata about the generated spritesheet, including:
  - `states` (array): List of animation states.
  - `framesPerState` (number): Number of frames per state.
  - `totalFrames` (number): Total number of frames in the spritesheet.
  - `dimensions` (object): Width and height of the spritesheet.
  - `frameData` (object): Detailed information about each animation state.

### Example Usage

```javascript
const spriteAI = require('spriteai');

const characterSprite = await spriteAI.generateCharacterSpritesheet('A brave knight in shining armor', {
  states: ['idle', 'walk', 'attack', 'defend'],
  framesPerState: 8,
  size: '2048x2048',
  style: 'pixel-art',
  direction: 'left',
  save: true
});

console.log(characterSprite.metadata);
// Use characterSprite.spritesheet for the base64 encoded PNG data
```

## generateLandscapeSprite

Generates a landscape sprite based on a given description and options.

### Parameters

- `description` (string): A description of the landscape to generate.
- `options` (object, optional): Configuration options for the landscape generation.
  - `size` (string, default: '1024x1024'): Output size of the sprite.
  - `style` (string, default: 'pixel-art'): Art style of the sprite.
  - `timeOfDay` (string, default: 'day'): Time of day setting (day, night, sunset, dawn).
  - `weather` (string, default: 'clear'): Weather conditions (clear, rainy, foggy, snowy).
  - `perspective` (string, default: 'side-scrolling'): Perspective of the landscape (side-scrolling, top-down, isometric).
  - `save` (boolean, default: false): Whether to save the generated image to disk.
  - `removeBackground` (boolean, optional): Whether to remove the background.
  - `backgroundColor` (string, optional): Background color to remove (if removeBackground is true).
  - `colorThreshold` (number, optional): Threshold for background color removal.

### Returns

An object containing:
- `original` (string): URL of the original generated image.
- `landscape` (string): Base64-encoded PNG data of the processed landscape sprite.
- `metadata` (object): Metadata about the generated landscape, including:
  - `description` (string): Original description.
  - `style` (string): Art style used.
  - `timeOfDay` (string): Time of day setting.
  - `weather` (string): Weather conditions.
  - `perspective` (string): Perspective used.
  - `dimensions` (object): Width and height of the sprite.

### Example Usage

```javascript
const spriteAI = require('spriteai');

const landscapeSprite = await spriteAI.generateLandscapeSprite('A mystical forest with glowing mushrooms', {
  size: '2048x1024',
  style: 'pixel-art',
  timeOfDay: 'night',
  weather: 'foggy',
  perspective: 'side-scrolling',
  save: true,
  removeBackground: true,
  backgroundColor: '#000000',
  colorThreshold: 0.1
});

console.log(landscapeSprite.metadata);
// Use landscapeSprite.landscape for the base64 encoded PNG data
```

## fetchAvailableAnimationStates

Retrieves a list of available animation states for character sprites.

### Parameters

None

### Returns

An array of strings representing available animation states.

### Example Usage

```javascript
const spriteAI = require('spriteai');

const availableStates = await spriteAI.fetchAvailableAnimationStates();
console.log(availableStates);
// Output: ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

## fetchAvailableSpriteStyles

Retrieves a list of available sprite styles.

### Parameters

None

### Returns

An array of strings representing available sprite styles.

### Example Usage

```javascript
const spriteAI = require('spriteai');

const availableStyles = await spriteAI.fetchAvailableSpriteStyles();
console.log(availableStyles);
// Output: ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

## generateEnvironmentSprites

Generates a tileset of environment sprites based on a given description and options.

### Parameters

- `description` (string): A description of the environment to generate.
- `options` (object, optional): Configuration options for the environment generation.
  - `elements` (number, default: 4): Number of distinct environment pieces to generate.
  - `size` (string, default: '1024x1024'): Output size of the tileset.
  - `style` (string, default: 'pixel-art'): Art style of the sprites.
  - `padding` (number, default: 1): Padding between sprites in pixels.
  - `theme` (string, default: 'fantasy'): Theme of the environment.
  - `save` (boolean, default: false): Whether to save the generated image to disk.

### Returns

An object containing:
- `original` (string): URL of the original generated image.
- `tileset` (string): Base64-encoded PNG data of the processed environment tileset.
- `metadata` (object): Metadata about the generated environment, including:
  - `elements` (number): Number of distinct environment pieces.
  - `theme` (string): Theme of the environment.
  - `dimensions` (object): Width and height of the tileset.
  - `tileData` (object): Information about the tileset layout.

### Example Usage

```javascript
const spriteAI = require('spriteai');

const environmentSprites = await spriteAI.generateEnvironmentSprites('A cyberpunk city with neon lights', {
  elements: 6,
  size: '2048x2048',
  style: 'pixel-art',
  theme: 'cyberpunk',
  save: true
});

console.log(environmentSprites.metadata);
// Use environmentSprites.tileset for the base64 encoded PNG data
```

This completes the API reference for the SpriteAI module. For more detailed information on implementation and advanced usage, please refer to the source code and additional documentation.