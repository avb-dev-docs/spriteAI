# SpriteAI API Reference

## Table of Contents

1. [Introduction](#introduction)
2. [Installation](#installation)
3. [Functions](#functions)
   3.1. [generateCharacterSpritesheet](#generatecharacterspritesheet)
   3.2. [generateLandscapeSprite](#generatelandscapesprite)
   3.3. [fetchAvailableAnimationStates](#fetchavailableanimationstates)
   3.4. [fetchAvailableSpriteStyles](#fetchavailablespritestyles)
   3.5. [generateEnvironmentSprites](#generateenvironmentsprites)
4. [Utility Functions](#utility-functions)
   4.1. [removeBackgroundColor](#removebackgroundcolor)

## Introduction

The SpriteAI library provides a set of powerful functions for generating game assets using AI. This API reference documents all public functions, their parameters, return values, and usage examples.

## Installation

To use the SpriteAI library in your project, install it via npm:

```bash
npm install spriteai
```

Then, import the functions you need in your JavaScript code:

```javascript
import { generateCharacterSpritesheet, generateLandscapeSprite } from 'spriteai';
```

## Functions

### generateCharacterSpritesheet

Generates a character spritesheet based on a given description and options.

```javascript
async function generateCharacterSpritesheet(description, options = {})
```

#### Parameters

- `description` (string): A textual description of the character.
- `options` (object, optional): Configuration options for the spritesheet generation.
  - `states` (array of strings, default: `['idle', 'walk', 'run', 'attack']`): Animation states to generate.
  - `framesPerState` (number, default: 6): Number of frames per animation state.
  - `size` (string, default: '1024x1024'): Output size of the spritesheet.
  - `style` (string, default: 'pixel-art'): Art style of the character.
  - `padding` (number, default: 1): Padding between sprites.
  - `direction` (string, default: 'right'): Base direction of the character.
  - `save` (boolean): If true, saves the generated spritesheet to the filesystem.

#### Returns

An object containing:
- `original` (string): URL of the original generated image.
- `spritesheet` (string): Base64-encoded PNG data of the processed spritesheet.
- `metadata` (object): Detailed information about the generated spritesheet.

#### Example Usage

```javascript
const result = await generateCharacterSpritesheet('A heroic knight in shining armor', {
  states: ['idle', 'walk', 'attack', 'defend'],
  framesPerState: 8,
  size: '2048x2048',
  style: 'pixel-art',
  save: true
});

console.log(result.metadata);
```

### generateLandscapeSprite

Generates a landscape sprite based on a given description and options.

```javascript
async function generateLandscapeSprite(description, options = {})
```

#### Parameters

- `description` (string): A textual description of the landscape.
- `options` (object, optional): Configuration options for the landscape generation.
  - `size` (string, default: '1024x1024'): Output size of the sprite.
  - `style` (string, default: 'pixel-art'): Art style of the landscape.
  - `timeOfDay` (string, default: 'day'): Time of day setting (e.g., 'day', 'night', 'sunset', 'dawn').
  - `weather` (string, default: 'clear'): Weather conditions (e.g., 'clear', 'rainy', 'foggy', 'snowy').
  - `perspective` (string, default: 'side-scrolling'): Perspective of the landscape (e.g., 'side-scrolling', 'top-down', 'isometric').
  - `save` (boolean, default: false): If true, saves the generated landscape to the filesystem.
  - `removeBackground` (boolean): If true, removes the background color.
  - `backgroundColor` (string): The background color to remove (if removeBackground is true).
  - `colorThreshold` (number): Threshold for color removal (if removeBackground is true).

#### Returns

An object containing:
- `original` (string): URL of the original generated image.
- `landscape` (string): Base64-encoded PNG data of the processed landscape sprite.
- `metadata` (object): Detailed information about the generated landscape.

#### Example Usage

```javascript
const result = await generateLandscapeSprite('A lush forest with a winding river', {
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

console.log(result.metadata);
```

### fetchAvailableAnimationStates

Retrieves a list of available animation states for character spritesheets.

```javascript
async function fetchAvailableAnimationStates()
```

#### Returns

An array of strings representing available animation states.

#### Example Usage

```javascript
const states = await fetchAvailableAnimationStates();
console.log(states); // ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

### fetchAvailableSpriteStyles

Retrieves a list of available sprite styles.

```javascript
async function fetchAvailableSpriteStyles()
```

#### Returns

An array of strings representing available sprite styles.

#### Example Usage

```javascript
const styles = await fetchAvailableSpriteStyles();
console.log(styles); // ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

### generateEnvironmentSprites

Generates a tileset of environment sprites based on a given description and options.

```javascript
async function generateEnvironmentSprites(description, options = {})
```

#### Parameters

- `description` (string): A textual description of the environment.
- `options` (object, optional): Configuration options for the environment generation.
  - `elements` (number, default: 4): Number of different elements to generate.
  - `size` (string, default: '1024x1024'): Output size of the tileset.
  - `style` (string, default: 'pixel-art'): Art style of the environment.
  - `padding` (number, default: 1): Padding between elements.
  - `theme` (string, default: 'fantasy'): Theme of the environment.
  - `save` (boolean): If true, saves the generated tileset to the filesystem.

#### Returns

An object containing:
- `original` (string): URL of the original generated image.
- `tileset` (string): Base64-encoded PNG data of the processed environment tileset.
- `metadata` (object): Detailed information about the generated tileset.

#### Example Usage

```javascript
const result = await generateEnvironmentSprites('A mystical forest with ancient ruins', {
  elements: 6,
  size: '2048x2048',
  style: 'pixel-art',
  theme: 'fantasy',
  save: true
});

console.log(result.metadata);
```

## Utility Functions

### removeBackgroundColor

Removes a specified background color from an image.

```javascript
async function removeBackgroundColor(inputPath, outputPath, targetColor, colorThreshold = 0, options = {})
```

#### Parameters

- `inputPath` (string): Path to the input image file.
- `outputPath` (string): Path where the processed image will be saved.
- `targetColor` (string): CSS color string of the background color to remove.
- `colorThreshold` (number, default: 0): Threshold for color matching.
- `options` (object, optional): Additional options for background removal.

#### Returns

A Promise that resolves when the background removal is complete.

#### Example Usage

```javascript
await removeBackgroundColor(
  'input.png',
  'output.png',
  '#FFFFFF',
  0.1
);
```

This function is primarily used internally by other SpriteAI functions but can be utilized separately if needed.