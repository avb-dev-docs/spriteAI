# SpriteAI API Reference

This API reference provides detailed documentation for all public functions in the SpriteAI module. The functions are organized by categories for easy navigation.

## Table of Contents

1. [Character Generation](#character-generation)
2. [Landscape Generation](#landscape-generation)
3. [Environment Generation](#environment-generation)
4. [Utility Functions](#utility-functions)

## Character Generation

### generateCharacterSpritesheet

Generates a character spritesheet based on a description.

**Location**: `/index.js` and `/spriteAI/index.js`

```javascript
async function generateCharacterSpritesheet(description, options = {})
```

#### Parameters:

- `description` (string): Description of the character to generate.
- `options` (object): Additional options for sprite generation.
  - `states` (array): Animation states to generate. Default: `['idle', 'walk', 'run', 'attack']`
  - `framesPerState` (number): Frames per animation state. Default: `6`
  - `size` (string): Output size. Default: `'1024x1024'`
  - `style` (string): Art style. Default: `'pixel-art'`
  - `padding` (number): Padding between sprites. Default: `1`
  - `direction` (string): Base direction of character. Default: `'right'`
  - `save` (boolean): Whether to save the generated image. Default: `false`

#### Returns:

An object containing:
- `original` (string): URL of the original generated image.
- `spritesheet` (string): Base64-encoded spritesheet image.
- `metadata` (object): Metadata about the generated spritesheet.

#### Example Usage:

```javascript
const result = await generateCharacterSpritesheet('a knight in armor', {
  states: ['idle', 'walk', 'attack'],
  framesPerState: 4,
  size: '512x512',
  style: 'pixel-art',
  direction: 'left',
  save: true
});

console.log(result.metadata);
```

## Landscape Generation

### generateLandscapeSprite

Generates a landscape sprite based on a description.

**Location**: `/index.js`

```javascript
async function generateLandscapeSprite(description, options = {})
```

#### Parameters:

- `description` (string): Description of the landscape to generate.
- `options` (object): Additional options for landscape generation.
  - `size` (string): Output size. Default: `'1024x1024'`
  - `style` (string): Art style. Default: `'pixel-art'`
  - `timeOfDay` (string): Time of day setting. Default: `'day'`
  - `weather` (string): Weather conditions. Default: `'clear'`
  - `perspective` (string): Perspective view. Default: `'side-scrolling'`
  - `save` (boolean): Whether to save the generated image. Default: `false`
  - `removeBackground` (boolean): Whether to remove the background. Default: `false`
  - `backgroundColor` (string): Background color to remove. Default: `'#FFFFFF'`
  - `colorThreshold` (number): Threshold for color removal. Default: `0.1`

#### Returns:

An object containing:
- `original` (string): URL of the original generated image.
- `landscape` (string): Base64-encoded landscape image.
- `metadata` (object): Metadata about the generated landscape.

#### Example Usage:

```javascript
const result = await generateLandscapeSprite('a lush forest with a river', {
  size: '512x512',
  style: 'pixel-art',
  timeOfDay: 'sunset',
  weather: 'clear',
  perspective: 'side-scrolling',
  save: true,
  removeBackground: true
});

console.log(result.metadata);
```

## Environment Generation

### generateEnvironmentSprites

Generates environment sprites based on a description.

**Location**: `/spriteAI/index.js`

```javascript
async function generateEnvironmentSprites(description, options = {})
```

#### Parameters:

- `description` (string): Description of the environment to generate.
- `options` (object): Additional options for environment generation.
  - `elements` (number): Number of different elements to generate. Default: `4`
  - `size` (string): Output size. Default: `'1024x1024'`
  - `style` (string): Art style. Default: `'pixel-art'`
  - `padding` (number): Padding between sprites. Default: `1`
  - `theme` (string): Theme of the environment. Default: `'fantasy'`
  - `save` (boolean): Whether to save the generated image. Default: `false`

#### Returns:

An object containing:
- `original` (string): URL of the original generated image.
- `tileset` (string): Base64-encoded tileset image.
- `metadata` (object): Metadata about the generated environment sprites.

#### Example Usage:

```javascript
const result = await generateEnvironmentSprites('medieval town', {
  elements: 6,
  size: '512x512',
  style: 'pixel-art',
  theme: 'medieval',
  save: true
});

console.log(result.metadata);
```

## Utility Functions

### removeBackgroundColor

Removes a specified background color from an image.

**Location**: `/index.js` and `/spriteAI/index.js`

```javascript
async function removeBackgroundColor(inputPath, outputPath, targetColor, colorThreshold = 0, options = {})
```

#### Parameters:

- `inputPath` (string): Path to the input image file.
- `outputPath` (string): Path to save the output image file.
- `targetColor` (string): Color to remove (e.g., '#FFFFFF').
- `colorThreshold` (number): Tolerance for color matching. Default: `0`
- `options` (object): Additional options (currently unused).

#### Returns:

The result of the image write operation.

#### Example Usage:

```javascript
const result = await removeBackgroundColor(
  'input.png',
  'output.png',
  '#FFFFFF',
  0.1
);
console.log('Background removed:', result);
```

### fetchAvailableAnimationStates

Fetches available animation states for character generation.

**Location**: `/spriteAI/index.js`

```javascript
async function fetchAvailableAnimationStates()
```

#### Returns:

An array of strings representing available animation states.

#### Example Usage:

```javascript
const states = await fetchAvailableAnimationStates();
console.log('Available animation states:', states);
```

### fetchAvailableSpriteStyles

Fetches available sprite styles for generation.

**Location**: `/spriteAI/index.js`

```javascript
async function fetchAvailableSpriteStyles()
```

#### Returns:

An array of strings representing available sprite styles.

#### Example Usage:

```javascript
const styles = await fetchAvailableSpriteStyles();
console.log('Available sprite styles:', styles);
```