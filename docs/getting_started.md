# Getting Started with SpriteAI

SpriteAI is a powerful library that allows you to generate character spritesheets and landscape sprites using AI. This guide will walk you through the installation process and demonstrate basic usage examples.

## Installation

To get started with SpriteAI, follow these steps:

1. Ensure you have Node.js installed on your system.
2. Create a new directory for your project and navigate to it in your terminal.
3. Initialize a new Node.js project:

```bash
npm init -y
```

4. Install SpriteAI and its dependencies:

```bash
npm install spriteai openai axios sharp jimp
```

## Basic Usage

### Generating Character Spritesheets

To generate a character spritesheet, use the `generateCharacterSpritesheet` function. Here's a basic example:

```javascript
import { generateCharacterSpritesheet } from 'spriteai';

async function createCharacterSprite() {
  const result = await generateCharacterSpritesheet('a cute cat warrior', {
    states: ['idle', 'walk', 'run', 'attack'],
    framesPerState: 6,
    size: '1024x1024',
    style: 'pixel-art',
    save: true
  });

  console.log('Character spritesheet generated:', result.spritesheet);
  console.log('Metadata:', result.metadata);
}

createCharacterSprite();
```

This will generate a pixel-art spritesheet of a cute cat warrior with idle, walk, run, and attack animations.

### Generating Landscape Sprites

To create a landscape sprite, use the `generateLandscapeSprite` function:

```javascript
import { generateLandscapeSprite } from 'spriteai';

async function createLandscapeSprite() {
  const result = await generateLandscapeSprite('a lush forest with a hidden treehouse', {
    size: '1024x1024',
    style: 'pixel-art',
    timeOfDay: 'sunset',
    weather: 'clear',
    perspective: 'side-scrolling',
    save: true
  });

  console.log('Landscape sprite generated:', result.landscape);
  console.log('Metadata:', result.metadata);
}

createLandscapeSprite();
```

This will create a pixel-art landscape sprite of a lush forest with a hidden treehouse at sunset.

## Main Features

SpriteAI offers the following main features:

1. **Character Spritesheet Generation**: Create animated character spritesheets with customizable states, frames, and styles.
2. **Landscape Sprite Generation**: Generate detailed landscape sprites for game backgrounds with various time of day and weather options.
3. **Customizable Output**: Control the size, style, and other parameters of your generated sprites.
4. **Metadata**: Receive detailed metadata about your generated sprites, including frame data and dimensions.
5. **Automatic Saving**: Option to automatically save generated sprites to your project's assets folder.

## Advanced Usage

### Fetching Available Animation States

You can fetch the available animation states using the `fetchAvailableAnimationStates` function:

```javascript
import { fetchAvailableAnimationStates } from 'spriteai';

async function getAnimationStates() {
  const states = await fetchAvailableAnimationStates();
  console.log('Available animation states:', states);
}

getAnimationStates();
```

### Fetching Available Sprite Styles

To get the list of available sprite styles, use the `fetchAvailableSpriteStyles` function:

```javascript
import { fetchAvailableSpriteStyles } from 'spriteai';

async function getSpriteStyles() {
  const styles = await fetchAvailableSpriteStyles();
  console.log('Available sprite styles:', styles);
}

getSpriteStyles();
```

### Generating Environment Sprites

For creating environment sprites or tilesets, use the `generateEnvironmentSprites` function:

```javascript
import { generateEnvironmentSprites } from 'spriteai';

async function createEnvironmentSprites() {
  const result = await generateEnvironmentSprites('medieval castle', {
    elements: 4,
    size: '1024x1024',
    style: 'pixel-art',
    theme: 'fantasy',
    save: true
  });

  console.log('Environment sprites generated:', result.tileset);
  console.log('Metadata:', result.metadata);
}

createEnvironmentSprites();
```

This will generate a tileset of medieval castle elements in a fantasy theme.

## Conclusion

SpriteAI provides a powerful and flexible way to generate game assets using AI. By leveraging these functions, you can quickly create high-quality spritesheets, landscapes, and environment elements for your game development projects. Experiment with different parameters and options to achieve the desired results for your specific needs.