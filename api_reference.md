# SpriteAI API Reference

This document provides a comprehensive reference for all public functions in the SpriteAI module. It covers functions from both the main `index.js` file and the SDK version in `spriteAI/index.js`.

## Table of Contents

1. [removeBackgroundColor](#removebackgroundcolor)
2. [generateCharacterSpritesheet](#generatecharacterspritesheet)
3. [generateLandscapeSprite](#generatelandscapesprite)
4. [fetchAvailableAnimationStates](#fetchavailableanimationstates)
5. [fetchAvailableSpriteStyles](#fetchavailablespritestyles)
6. [generateEnvironmentSprites](#generateenvironmentsprites)

## removeBackgroundColor

Removes a specified background color from an image.

**Location**: `index.js`, `spriteAI/index.js`

### Syntax

```javascript
async function removeBackgroundColor(inputPath, outputPath, targetColor, colorThreshold = 0, options = {})
```

### Parameters

- `inputPath` (string): Path to the input image file.
- `outputPath` (string): Path where the processed image will be saved.
- `targetColor` (string): CSS color string representing the background color to remove.
- `colorThreshold` (number, optional): Threshold for color difference. Default is 0.
- `options` (object, optional): Additional options (currently unused).

### Returns

- `Promise<object>`: A promise that resolves with the result of the image processing.

### Example

```javascript
await removeBackgroundColor('input.png', 'output.png', '#FFFFFF', 0.1);
```

## generateCharacterSpritesheet

Generates a character spritesheet based on a description.

**Location**: `index.js`, `spriteAI/index.js`

### Syntax

```javascript
async function generateCharacterSpritesheet(description, options = {})
```

### Parameters

- `description` (string): Description of the character to generate.
- `options` (object, optional): Configuration options for the spritesheet generation.
  - `states` (array of strings): Animation states to generate. Default: `['idle', 'walk', 'run', 'attack']`.
  - `framesPerState` (number): Frames per animation state. Default: 6.
  - `size` (string): Output size of the spritesheet. Default: '1024x1024'.
  - `style` (string): Art style of the spritesheet. Default: 'pixel-art'.
  - `padding` (number): Padding between sprites. Default: 1.
  - `direction` (string): Base direction of the character. Default: 'right'.
  - `save` (boolean): Whether to save the generated image to disk. Default: false.

### Returns

- `Promise<object>`: A promise that resolves with an object containing:
  - `original` (string): URL of the original generated image.
  - `spritesheet` (string): Base64-encoded data URL of the processed spritesheet.
  - `metadata` (object): Metadata about the generated spritesheet.

### Example

```javascript
const result = await generateCharacterSpritesheet('a medieval knight', {
  states: ['idle', 'walk', 'attack'],
  framesPerState: 4,
  size: '512x512',
  style: 'pixel-art',
  save: true
});
console.log(result.metadata);
```

## generateLandscapeSprite

Generates a landscape sprite based on a description.

**Location**: `index.js`

### Syntax

```javascript
async function generateLandscapeSprite(description, options = {})
```

### Parameters

- `description` (string): Description of the landscape to generate.
- `options` (object, optional): Configuration options for the landscape generation.
  - `size` (string): Output size of the sprite. Default: '1024x1024'.
  - `style` (string): Art style of the sprite. Default: 'pixel-art'.
  - `timeOfDay` (string): Time of day setting. Default: 'day'.
  - `weather` (string): Weather conditions. Default: 'clear'.
  - `perspective` (string): Perspective of the landscape. Default: 'side-scrolling'.
  - `save` (boolean): Whether to save the generated image to disk. Default: false.
  - `removeBackground` (boolean): Whether to remove the background. Default: false.
  - `backgroundColor` (string): Background color to remove if removeBackground is true.
  - `colorThreshold` (number): Threshold for background color removal.

### Returns

- `Promise<object>`: A promise that resolves with an object containing:
  - `original` (string): URL of the original generated image.
  - `landscape` (string): Base64-encoded data URL of the processed landscape sprite.
  - `metadata` (object): Metadata about the generated landscape.

### Example

```javascript
const result = await generateLandscapeSprite('a lush forest with a river', {
  size: '512x512',
  style: 'pixel-art',
  timeOfDay: 'sunset',
  weather: 'clear',
  perspective: 'side-scrolling',
  save: true,
  removeBackground: true,
  backgroundColor: '#FFFFFF',
  colorThreshold: 0.1
});
console.log(result.metadata);
```

## fetchAvailableAnimationStates

Fetches the list of available animation states.

**Location**: `spriteAI/index.js`

### Syntax

```javascript
async function fetchAvailableAnimationStates()
```

### Returns

- `Promise<array>`: A promise that resolves with an array of available animation state strings.

### Example

```javascript
const states = await fetchAvailableAnimationStates();
console.log(states); // ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

## fetchAvailableSpriteStyles

Fetches the list of available sprite styles.

**Location**: `spriteAI/index.js`

### Syntax

```javascript
async function fetchAvailableSpriteStyles()
```

### Returns

- `Promise<array>`: A promise that resolves with an array of available sprite style strings.

### Example

```javascript
const styles = await fetchAvailableSpriteStyles();
console.log(styles); // ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

## generateEnvironmentSprites

Generates environment sprites based on a description.

**Location**: `spriteAI/index.js`

### Syntax

```javascript
async function generateEnvironmentSprites(description, options = {})
```

### Parameters

- `description` (string): Description of the environment to generate.
- `options` (object, optional): Configuration options for the environment generation.
  - `elements` (number): Number of different elements to generate. Default: 4.
  - `size` (string): Output size of the tileset. Default: '1024x1024'.
  - `style` (string): Art style of the sprites. Default: 'pixel-art'.
  - `padding` (number): Padding between elements. Default: 1.
  - `theme` (string): Theme of the environment. Default: 'fantasy'.
  - `save` (boolean): Whether to save the generated image to disk. Default: false.

### Returns

- `Promise<object>`: A promise that resolves with an object containing:
  - `original` (string): URL of the original generated image.
  - `tileset` (string): Base64-encoded data URL of the processed tileset.
  - `metadata` (object): Metadata about the generated environment sprites.

### Example

```javascript
const result = await generateEnvironmentSprites('a forest clearing', {
  elements: 6,
  size: '512x512',
  style: 'pixel-art',
  theme: 'fantasy',
  save: true
});
console.log(result.metadata);
```