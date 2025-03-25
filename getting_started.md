# Getting Started with SpriteAI

SpriteAI is a powerful library that allows you to generate character spritesheets and landscape sprites using AI. This guide will walk you through the installation process, basic usage of the main functions, and provide a simple example project to get you started.

## Installation

To begin using SpriteAI, you'll need to install it along with its dependencies. Follow these steps:

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

### Generating a Character Spritesheet

The `generateCharacterSpritesheet` function allows you to create a spritesheet with multiple animation states for a character. Here's how to use it:

```javascript
import { generateCharacterSpritesheet } from 'spriteai';

async function createCharacter() {
  const options = {
    states: ['idle', 'walk', 'run', 'attack'],
    framesPerState: 6,
    size: '1024x1024',
    style: 'pixel-art',
    direction: 'right',
    save: true
  };

  const result = await generateCharacterSpritesheet('a knight in shining armor', options);
  console.log('Character spritesheet generated:', result.spritesheet);
  console.log('Metadata:', result.metadata);
}

createCharacter();
```

### Generating a Landscape Sprite

The `generateLandscapeSprite` function creates a single landscape image that can be used as a game background. Here's an example:

```javascript
import { generateLandscapeSprite } from 'spriteai';

async function createLandscape() {
  const options = {
    size: '1024x1024',
    style: 'pixel-art',
    timeOfDay: 'sunset',
    weather: 'clear',
    perspective: 'side-scrolling',
    save: true
  };

  const result = await generateLandscapeSprite('a medieval castle on a hill', options);
  console.log('Landscape sprite generated:', result.landscape);
  console.log('Metadata:', result.metadata);
}

createLandscape();
```

## Example Project: Simple Game Asset Generator

Let's create a small project that generates both a character spritesheet and a landscape sprite, which could be used as assets for a simple game.

1. Create a new file named `game-asset-generator.js` with the following content:

```javascript
import { generateCharacterSpritesheet, generateLandscapeSprite } from 'spriteai';

async function generateGameAssets() {
  // Generate character spritesheet
  const characterOptions = {
    states: ['idle', 'walk', 'attack'],
    framesPerState: 4,
    size: '512x512',
    style: 'pixel-art',
    save: true
  };

  const character = await generateCharacterSpritesheet('a brave adventurer with a sword and shield', characterOptions);
  console.log('Character spritesheet generated');

  // Generate landscape sprite
  const landscapeOptions = {
    size: '1024x512',
    style: 'pixel-art',
    timeOfDay: 'day',
    weather: 'clear',
    perspective: 'side-scrolling',
    save: true
  };

  const landscape = await generateLandscapeSprite('a lush forest with ancient ruins', landscapeOptions);
  console.log('Landscape sprite generated');

  // Log asset information
  console.log('\nGame Assets Generated:');
  console.log('Character Spritesheet:', character.spritesheet.substring(0, 50) + '...');
  console.log('Character States:', character.metadata.states);
  console.log('Landscape Sprite:', landscape.landscape.substring(0, 50) + '...');
  console.log('Landscape Description:', landscape.metadata.description);
}

generateGameAssets();
```

2. Run the script:

```bash
node game-asset-generator.js
```

This script will generate a character spritesheet and a landscape sprite, saving them in the `assets` folder of your project directory. The console output will provide information about the generated assets, including base64-encoded previews and metadata.

## Next Steps

Now that you've got the basics down, you can explore more advanced features of SpriteAI:

- Experiment with different animation states and styles for characters.
- Try generating various landscapes with different weather conditions and times of day.
- Integrate the generated assets into your game development workflow.
- Explore the `removeBackgroundColor` function for more control over sprite transparency.

Remember to refer to the API documentation for detailed information on all available options and functions. Happy sprite generating!