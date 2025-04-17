# SpriteAI Quickstart Guide

Welcome to SpriteAI! This quickstart guide will help you get started with generating character spritesheets and landscape sprites using our AI-powered tool.

## Installation

To install SpriteAI, follow these steps:

1. Ensure you have Node.js installed on your system.
2. Open your terminal and run the following command:

```bash
npm install spriteai
```

3. Once installed, you can import SpriteAI in your project.

## Basic Usage

### Generating Character Spritesheets

To generate a character spritesheet, use the `generateCharacterSpritesheet` function:

```javascript
import { generateCharacterSpritesheet } from 'spriteai';

const result = await generateCharacterSpritesheet('a brave knight in shining armor', {
  states: ['idle', 'walk', 'run', 'attack'],
  framesPerState: 6,
  size: '1024x1024',
  style: 'pixel-art',
  direction: 'right'
});

console.log(result.spritesheet); // Base64 encoded spritesheet image
console.log(result.metadata); // Metadata about the generated spritesheet
```

### Generating Landscape Sprites

To generate a landscape sprite, use the `generateLandscapeSprite` function:

```javascript
import { generateLandscapeSprite } from 'spriteai';

const result = await generateLandscapeSprite('a lush forest with a winding river', {
  size: '1024x1024',
  style: 'pixel-art',
  timeOfDay: 'day',
  weather: 'clear',
  perspective: 'side-scrolling'
});

console.log(result.landscape); // Base64 encoded landscape image
console.log(result.metadata); // Metadata about the generated landscape
```

## Additional Features

### Fetching Available Animation States

You can fetch the available animation states for character spritesheets:

```javascript
import { fetchAvailableAnimationStates } from 'spriteai';

const states = await fetchAvailableAnimationStates();
console.log(states); // ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

### Fetching Available Sprite Styles

To get a list of available sprite styles:

```javascript
import { fetchAvailableSpriteStyles } from 'spriteai';

const styles = await fetchAvailableSpriteStyles();
console.log(styles); // ['pixel-art', 'vector', '3d', 'hand-drawn', 'anime']
```

### Generating Environment Sprites

For creating environment sprites, use the `generateEnvironmentSprites` function:

```javascript
import { generateEnvironmentSprites } from 'spriteai';

const result = await generateEnvironmentSprites('medieval castle', {
  elements: 4,
  size: '1024x1024',
  style: 'pixel-art',
  theme: 'fantasy'
});

console.log(result.tileset); // Base64 encoded tileset image
console.log(result.metadata); // Metadata about the generated environment sprites
```

## Next Steps

This quickstart guide covers the basic usage of SpriteAI. For more detailed information on advanced features, configuration options, and best practices, please refer to our comprehensive documentation.

Happy sprite generating!