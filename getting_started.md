# Getting Started with SpriteAI

SpriteAI is a powerful tool that allows you to generate character spritesheets and landscape sprites for your game development projects. This guide will walk you through the installation process, basic configuration, and how to create your first sprite using SpriteAI.

## Installation

To get started with SpriteAI, follow these steps:

1. Make sure you have Node.js installed on your system.
2. Create a new directory for your project and navigate to it in your terminal.
3. Initialize a new Node.js project:

```bash
npm init -y
```

4. Install SpriteAI and its dependencies:

```bash
npm install spriteai openai axios sharp jimp
```

## Basic Configuration

Before using SpriteAI, you need to set up your OpenAI API key. Create a `.env` file in your project root and add your API key:

```
OPENAI_API_KEY=your_api_key_here
```

Make sure to add `.env` to your `.gitignore` file to keep your API key secure.

## Creating Your First Sprite

### Generating a Character Spritesheet

To create a character spritesheet, you can use the `generateCharacterSpritesheet` function. Here's a basic example:

```javascript
import { generateCharacterSpritesheet } from 'spriteai';

async function createCharacterSprite() {
  const result = await generateCharacterSpritesheet('a cute robot', {
    states: ['idle', 'walk', 'run'],
    framesPerState: 4,
    size: '512x512',
    style: 'pixel-art',
    save: true
  });

  console.log('Character spritesheet generated:', result);
}

createCharacterSprite();
```

This will generate a pixel-art spritesheet of a cute robot with idle, walk, and run animations, each having 4 frames.

### Generating a Landscape Sprite

To create a landscape sprite, use the `generateLandscapeSprite` function:

```javascript
import { generateLandscapeSprite } from 'spriteai';

async function createLandscapeSprite() {
  const result = await generateLandscapeSprite('a lush forest with a waterfall', {
    size: '1024x512',
    style: 'pixel-art',
    timeOfDay: 'sunset',
    weather: 'clear',
    perspective: 'side-scrolling',
    save: true
  });

  console.log('Landscape sprite generated:', result);
}

createLandscapeSprite();
```

This will generate a pixel-art landscape of a lush forest with a waterfall, set during sunset with clear weather, in a side-scrolling perspective.

## Customizing Output

Both `generateCharacterSpritesheet` and `generateLandscapeSprite` functions accept various options to customize the output:

### Character Spritesheet Options

- `states`: An array of animation states (default: `['idle', 'walk', 'run', 'attack']`)
- `framesPerState`: Number of frames per animation state (default: 6)
- `size`: Output image size (default: '1024x1024')
- `style`: Art style (default: 'pixel-art')
- `padding`: Padding between sprites (default: 1)
- `direction`: Base direction of character (default: 'right')
- `save`: Whether to save the generated image (default: false)

### Landscape Sprite Options

- `size`: Output image size (default: '1024x1024')
- `style`: Art style (default: 'pixel-art')
- `timeOfDay`: Time of day setting (default: 'day')
- `weather`: Weather conditions (default: 'clear')
- `perspective`: Perspective view (default: 'side-scrolling')
- `save`: Whether to save the generated image (default: false)
- `removeBackground`: Whether to remove the background (optional)
- `backgroundColor`: Background color to remove (if removeBackground is true)
- `colorThreshold`: Threshold for background color removal (if removeBackground is true)

## Working with Generated Sprites

The generated sprites are returned as base64-encoded strings, which you can use directly in your game engine or save as image files. The returned object also includes metadata about the sprite, such as dimensions, frame data, and other relevant information.

## Conclusion

This guide has covered the basics of getting started with SpriteAI, including installation, basic usage, and customization options. Experiment with different descriptions and options to create unique and exciting sprites for your game projects!

For more advanced usage and additional features, refer to the API documentation and examples provided in the SpriteAI package.