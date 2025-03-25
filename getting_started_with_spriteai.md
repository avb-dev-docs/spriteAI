# Getting Started with SpriteAI

SpriteAI is a powerful tool for generating game assets using AI. This guide will help you get started with SpriteAI, covering installation, basic usage, and an overview of its main features.

## Installation

To install SpriteAI, follow these steps:

1. Ensure you have Node.js installed on your system.
2. Create a new directory for your project and navigate to it in the terminal.
3. Initialize a new Node.js project:
   ```
   npm init -y
   ```
4. Install SpriteAI and its dependencies:
   ```
   npm install spriteai openai axios sharp jimp
   ```

## Basic Usage

### Generating Character Spritesheets

To generate a character spritesheet, use the `generateCharacterSpritesheet` function:

```javascript
import { generateCharacterSpritesheet } from 'spriteai';

const description = 'a cute cat warrior';
const options = {
  states: ['idle', 'walk', 'run', 'attack'],
  framesPerState: 6,
  size: '1024x1024',
  style: 'pixel-art',
  direction: 'right'
};

const result = await generateCharacterSpritesheet(description, options);
console.log(result);
```

This will generate a spritesheet with four animation states (idle, walk, run, attack) for a cute cat warrior character.

### Generating Landscape Sprites

To generate a landscape sprite, use the `generateLandscapeSprite` function:

```javascript
import { generateLandscapeSprite } from 'spriteai';

const description = 'a lush forest with a river';
const options = {
  size: '1024x1024',
  style: 'pixel-art',
  timeOfDay: 'day',
  weather: 'clear',
  perspective: 'side-scrolling'
};

const result = await generateLandscapeSprite(description, options);
console.log(result);
```

This will generate a side-scrolling landscape sprite of a lush forest with a river during daytime with clear weather.

## Main Features

SpriteAI offers several key features:

1. **Character Spritesheet Generation**: Create animated character spritesheets with customizable states, frames, and styles.

2. **Landscape Sprite Generation**: Generate background landscapes for your games with various settings like time of day, weather, and perspective.

3. **Customization Options**: Both character and landscape generation functions accept various options to tailor the output to your needs.

4. **Background Removal**: For landscape sprites, you can optionally remove the background to create transparent sprites.

5. **Metadata**: Each generated sprite comes with detailed metadata, including dimensions, frame data, and other relevant information.

6. **File Saving**: Option to automatically save generated sprites to your project's assets folder.

## Advanced Features

### Fetching Available Animation States

You can fetch the list of available animation states:

```javascript
import { fetchAvailableAnimationStates } from 'spriteai';

const states = await fetchAvailableAnimationStates();
console.log(states);
```

### Fetching Available Sprite Styles

To get the list of available sprite styles:

```javascript
import { fetchAvailableSpriteStyles } from 'spriteai';

const styles = await fetchAvailableSpriteStyles();
console.log(styles);
```

### Generating Environment Sprites

For creating environmental elements:

```javascript
import { generateEnvironmentSprites } from 'spriteai';

const description = 'forest elements';
const options = {
  elements: 4,
  size: '1024x1024',
  style: 'pixel-art',
  theme: 'fantasy'
};

const result = await generateEnvironmentSprites(description, options);
console.log(result);
```

This generates a tileset of forest elements in a fantasy theme.

## Conclusion

SpriteAI provides a powerful set of tools for game developers to quickly generate high-quality game assets using AI. By leveraging these functions, you can streamline your asset creation process and focus more on game development. Experiment with different options and descriptions to create unique and engaging sprites for your games!