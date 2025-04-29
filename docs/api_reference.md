# SpriteAI API Reference

## Table of Contents
1. [Introduction](#introduction)
2. [Character Spritesheet Generation](#character-spritesheet-generation)
3. [Landscape Sprite Generation](#landscape-sprite-generation)
4. [Utility Functions](#utility-functions)
5. [Types and Interfaces](#types-and-interfaces)

## Introduction

The SpriteAI library provides a set of powerful functions for generating game assets using AI. This API reference documents all public functions, their parameters, return values, and usage examples.

## Character Spritesheet Generation

### `generateCharacterSpritesheet(description, options)`

Generates a character spritesheet based on the provided description and options.

#### Parameters

- `description` (string): A textual description of the character to generate.
- `options` (object, optional): Configuration options for the spritesheet generation.
  - `states` (string[], default: `['idle', 'walk', 'run', 'attack']`): Animation states to generate.
  - `framesPerState` (number, default: 6): Number of frames per animation state.
  - `size` (string, default: '1024x1024'): Output size of the spritesheet.
  - `style` (string, default: 'pixel-art'): Art style of the character.
  - `padding` (number, default: 1): Padding between sprites.
  - `direction` (string, default: 'right'): Base direction of the character.
  - `save` (boolean, default: false): Whether to save the generated image to disk.

#### Returns

Promise<Object>:
- `original` (string): URL of the original generated image.
- `spritesheet` (string): Base64-encoded PNG data of the processed spritesheet.
- `metadata` (object): Metadata about the generated spritesheet.

#### Example Usage

```javascript
const spriteAI = require('spriteai');

const character = await spriteAI.generateCharacterSpritesheet('A brave knight in shining armor', {
  states: ['idle', 'walk', 'attack', 'defend'],
  framesPerState: 8,
  style: 'pixel-art',
  size: '2048x2048',
  save: true
});

console.log(character.metadata);
// Use character.spritesheet in your game engine
```

## Landscape Sprite Generation

### `generateLandscapeSprite(description, options)`

Generates a landscape sprite based on the provided description and options.

#### Parameters

- `description` (string): A textual description of the landscape to generate.
- `options` (object, optional): Configuration options for the landscape generation.
  - `size` (string, default: '1024x1024'): Output size of the sprite.
  - `style` (string, default: 'pixel-art'): Art style of the landscape.
  - `timeOfDay` (string, default: 'day'): Time of day setting (day, night, sunset, dawn).
  - `weather` (string, default: 'clear'): Weather conditions (clear, rainy, foggy, snowy).
  - `perspective` (string, default: 'side-scrolling'): Perspective of the landscape (side-scrolling, top-down, isometric).
  - `save` (boolean, default: false): Whether to save the generated image to disk.
  - `removeBackground` (boolean, default: false): Whether to remove the background.
  - `backgroundColor` (string, optional): Background color to remove (if removeBackground is true).
  - `colorThreshold` (number, default: 0.1): Color threshold for background removal.

#### Returns

Promise<Object>:
- `original` (string): URL of the original generated image.
- `landscape` (string): Base64-encoded PNG data of the processed landscape sprite.
- `metadata` (object): Metadata about the generated landscape.

#### Example Usage

```javascript
const spriteAI = require('spriteai');

const landscape = await spriteAI.generateLandscapeSprite('A lush forest with a winding river', {
  style: 'pixel-art',
  timeOfDay: 'sunset',
  weather: 'clear',
  perspective: 'side-scrolling',
  removeBackground: true,
  backgroundColor: '#FFFFFF',
  save: true
});

console.log(landscape.metadata);
// Use landscape.landscape in your game engine
```

## Utility Functions

### `fetchAvailableAnimationStates()`

Retrieves a list of available animation states for character spritesheets.

#### Returns

Promise<string[]>: An array of animation state names.

#### Example Usage

```javascript
const spriteAI = require('spriteai');

const states = await spriteAI.fetchAvailableAnimationStates();
console.log(states); // ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

### `fetchAvailableSpriteStyles()`

Retrieves a list of available sprite styles.

#### Returns

Promise<string[]>: An array of sprite style names.

#### Example Usage

```javascript
const spriteAI = require('spriteai');

const styles = await spriteAI.fetchAvailableSpriteStyles();
console.log(styles); // ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

## Types and Interfaces

### CharacterSpritesheetOptions

```typescript
interface CharacterSpritesheetOptions {
  states?: string[];
  framesPerState?: number;
  size?: string;
  style?: string;
  padding?: number;
  direction?: string;
  save?: boolean;
}
```

### LandscapeSpriteOptions

```typescript
interface LandscapeSpriteOptions {
  size?: string;
  style?: string;
  timeOfDay?: string;
  weather?: string;
  perspective?: string;
  save?: boolean;
  removeBackground?: boolean;
  backgroundColor?: string;
  colorThreshold?: number;
}
```

### SpritesheetMetadata

```typescript
interface SpritesheetMetadata {
  states: string[];
  framesPerState: number;
  totalFrames: number;
  dimensions: {
    width: number;
    height: number;
  };
  frameData: {
    [state: string]: {
      row: number;
      frames: number;
      startFrame: number;
      endFrame: number;
    };
  };
}
```

### LandscapeMetadata

```typescript
interface LandscapeMetadata {
  description: string;
  style: string;
  timeOfDay: string;
  weather: string;
  perspective: string;
  dimensions: {
    width: number;
    height: number;
  };
}
```

This API reference provides a comprehensive guide to using the SpriteAI library for generating game assets. Developers can easily integrate these functions into their game development workflows to create character spritesheets and landscape sprites with AI-powered generation.