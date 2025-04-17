# SpriteAI API Reference

This API reference provides comprehensive documentation for the SpriteAI library, including all public functions, their parameters, return values, and usage examples.

## Table of Contents

1. [Character Sprite Generation](#character-sprite-generation)
   - [generateCharacterSpritesheet](#generatecharacterspritesheet)
2. [Landscape Sprite Generation](#landscape-sprite-generation)
   - [generateLandscapeSprite](#generatelandscapesprite)
3. [Environment Sprite Generation](#environment-sprite-generation)
   - [generateEnvironmentSprites](#generateenvironmentsprites)
4. [SDK-specific Functions](#sdk-specific-functions)
   - [fetchAvailableAnimationStates](#fetchavailableanimationstates)
   - [fetchAvailableSpriteStyles](#fetchavailablespritestyles)
5. [Utility Functions](#utility-functions)
   - [removeBackgroundColor](#removebackgroundcolor)

## Character Sprite Generation

### generateCharacterSpritesheet

Generates a character spritesheet based on the provided description and options.

**Function Signature:**
```javascript
async function generateCharacterSpritesheet(description, options = {})
```

**Parameters:**
- `description` (string): A detailed description of the character to generate.
- `options` (object, optional): Configuration options for the spritesheet generation.
  - `states` (array of strings, default: `['idle', 'walk', 'run', 'attack']`): Animation states to generate.
  - `framesPerState` (number, default: 6): Number of frames per animation state.
  - `size` (string, default: '1024x1024'): Output size of the spritesheet.
  - `style` (string, default: 'pixel-art'): Art style of the character.
  - `padding` (number, default: 1): Padding between sprites in the sheet.
  - `direction` (string, default: 'right'): Base direction of the character.
  - `save` (boolean): Whether to save the generated image to disk.

**Returns:**
An object containing:
- `original` (string): URL of the original generated image.
- `spritesheet` (string): Base64-encoded PNG data of the processed spritesheet.
- `metadata` (object): Detailed information about the generated spritesheet.

**Example Usage:**
```javascript
const characterSprite = await generateCharacterSpritesheet('A brave knight with shining armor', {
  states: ['idle', 'walk', 'attack', 'die'],
  framesPerState: 8,
  size: '2048x2048',
  style: 'pixel-art',
  save: true
});

console.log(characterSprite.metadata);
```

## Landscape Sprite Generation

### generateLandscapeSprite

Generates a landscape sprite based on the provided description and options.

**Function Signature:**
```javascript
async function generateLandscapeSprite(description, options = {})
```

**Parameters:**
- `description` (string): A detailed description of the landscape to generate.
- `options` (object, optional): Configuration options for the landscape generation.
  - `size` (string, default: '1024x1024'): Output size of the sprite.
  - `style` (string, default: 'pixel-art'): Art style of the landscape.
  - `timeOfDay` (string, default: 'day'): Time of day setting (day, night, sunset, dawn).
  - `weather` (string, default: 'clear'): Weather conditions (clear, rainy, foggy, snowy).
  - `perspective` (string, default: 'side-scrolling'): Perspective of the landscape (side-scrolling, top-down, isometric).
  - `save` (boolean, default: false): Whether to save the generated image to disk.
  - `removeBackground` (boolean): Whether to remove the background color.
  - `backgroundColor` (string): Target background color to remove (if removeBackground is true).
  - `colorThreshold` (number): Threshold for color removal (if removeBackground is true).

**Returns:**
An object containing:
- `original` (string): URL of the original generated image.
- `landscape` (string): Base64-encoded PNG data of the processed landscape sprite.
- `metadata` (object): Detailed information about the generated landscape.

**Example Usage:**
```javascript
const landscapeSprite = await generateLandscapeSprite('A lush forest with a winding river', {
  size: '2048x1024',
  style: 'pixel-art',
  timeOfDay: 'sunset',
  weather: 'clear',
  perspective: 'side-scrolling',
  save: true,
  removeBackground: true,
  backgroundColor: '#FFFFFF',
  colorThreshold: 0.1
});

console.log(landscapeSprite.metadata);
```

## Environment Sprite Generation

### generateEnvironmentSprites

Generates a set of environment sprites based on the provided description and options.

**Function Signature:**
```javascript
async function generateEnvironmentSprites(description, options = {})
```

**Parameters:**
- `description` (string): A detailed description of the environment to generate.
- `options` (object, optional): Configuration options for the environment sprites generation.
  - `elements` (number, default: 4): Number of different elements to generate.
  - `size` (string, default: '1024x1024'): Output size of the sprite sheet.
  - `style` (string, default: 'pixel-art'): Art style of the environment sprites.
  - `padding` (number, default: 1): Padding between sprites in the sheet.
  - `theme` (string, default: 'fantasy'): Theme of the environment.
  - `save` (boolean): Whether to save the generated image to disk.

**Returns:**
An object containing:
- `original` (string): URL of the original generated image.
- `tileset` (string): Base64-encoded PNG data of the processed environment tileset.
- `metadata` (object): Detailed information about the generated environment sprites.

**Example Usage:**
```javascript
const environmentSprites = await generateEnvironmentSprites('A medieval castle interior', {
  elements: 6,
  size: '2048x2048',
  style: 'pixel-art',
  theme: 'medieval',
  save: true
});

console.log(environmentSprites.metadata);
```

## SDK-specific Functions

### fetchAvailableAnimationStates

Retrieves a list of available animation states for character sprites.

**Function Signature:**
```javascript
async function fetchAvailableAnimationStates()
```

**Returns:**
An array of strings representing available animation states.

**Example Usage:**
```javascript
const availableStates = await fetchAvailableAnimationStates();
console.log(availableStates);
// Output: ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

### fetchAvailableSpriteStyles

Retrieves a list of available sprite styles.

**Function Signature:**
```javascript
async function fetchAvailableSpriteStyles()
```

**Returns:**
An array of strings representing available sprite styles.

**Example Usage:**
```javascript
const availableStyles = await fetchAvailableSpriteStyles();
console.log(availableStyles);
// Output: ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

## Utility Functions

### removeBackgroundColor

Removes a specified background color from an image.

**Function Signature:**
```javascript
async function removeBackgroundColor(inputPath, outputPath, targetColor, colorThreshold = 0, options = {})
```

**Parameters:**
- `inputPath` (string): Path to the input image file.
- `outputPath` (string): Path where the processed image will be saved.
- `targetColor` (string): CSS color string of the background color to remove.
- `colorThreshold` (number, default: 0): Threshold for color matching.
- `options` (object, optional): Additional options for background removal.

**Returns:**
A promise that resolves when the background removal is complete.

**Example Usage:**
```javascript
await removeBackgroundColor('input.png', 'output.png', '#FFFFFF', 0.1);
console.log('Background removed successfully');
```

This function is primarily used internally by other SpriteAI functions but can be used separately if needed.