---
title: Advanced Usage Guide
description: Learn advanced techniques for using the SpriteAI library, including customization, animation states, and game engine integration.
---

# Advanced Usage Guide for SpriteAI

This guide covers advanced techniques for using the SpriteAI library, including customizing sprite generation, working with different animation states, and integrating generated sprites into game engines.

## Table of Contents

1. [Customizing Sprite Generation](#customizing-sprite-generation)
2. [Working with Animation States](#working-with-animation-states)
3. [Game Engine Integration](#game-engine-integration)
4. [Complex Use Cases](#complex-use-cases)

## Customizing Sprite Generation

The SpriteAI library offers various options to customize your sprite generation process. Here are some advanced techniques:

### Character Spritesheet Customization

When generating character spritesheets, you can customize several parameters:

```javascript
const options = {
  states: ['idle', 'walk', 'run', 'attack', 'jump'],
  framesPerState: 8,
  size: '2048x2048',
  style: 'pixel-art',
  padding: 2,
  direction: 'left'
};

const characterSprite = await generateCharacterSpritesheet('warrior with a sword', options);
```

This example creates a more complex character spritesheet with additional states, more frames per state, larger size, and a different facing direction.

### Environment Sprite Customization

For environment sprites, you can adjust the number of elements, style, and theme:

```javascript
const envOptions = {
  elements: 6,
  size: '1024x1024',
  style: 'vector',
  padding: 2,
  theme: 'sci-fi'
};

const environmentSprites = await generateEnvironmentSprites('space station interior', envOptions);
```

This generates a set of sci-fi themed vector art environment sprites for a space station interior.

## Working with Animation States

SpriteAI supports various animation states for character sprites. You can fetch available states and customize your spritesheets accordingly.

### Fetching Available Animation States

Use the `fetchAvailableAnimationStates` function to get a list of supported states:

```javascript
const availableStates = await fetchAvailableAnimationStates();
console.log(availableStates);
// Output: ['idle', 'walk', 'run', 'attack', 'jump', 'fall', 'hurt', 'die']
```

### Creating Custom Animation Sequences

You can create custom animation sequences by selecting specific states:

```javascript
const customStates = ['idle', 'attack', 'hurt', 'die'];
const options = {
  states: customStates,
  framesPerState: 10
};

const characterSprite = await generateCharacterSpritesheet('mage casting spells', options);
```

This example creates a spritesheet focused on a mage's spell-casting sequence.

## Game Engine Integration

Integrating SpriteAI-generated sprites into game engines typically involves these steps:

1. Generate the sprite or spritesheet
2. Save or process the image data
3. Load the sprite into your game engine
4. Set up animation or rendering logic

Here's a generic example of how you might use a generated character spritesheet in a game:

```javascript
// Generate the spritesheet
const characterSprite = await generateCharacterSpritesheet('knight in armor');

// Save the spritesheet (if not already saved)
const fs = require('fs');
const path = require('path');
fs.writeFileSync(path.join('assets', 'knight_spritesheet.png'), characterSprite.spritesheet, 'base64');

// In your game code (pseudo-code, as it depends on your game engine)
function setupCharacterSprite() {
  const texture = loadTexture('assets/knight_spritesheet.png');
  const sprite = createSprite(texture);
  
  // Set up animations using the metadata
  const { frameData } = characterSprite.metadata;
  for (const [state, data] of Object.entries(frameData)) {
    sprite.addAnimation(state, data.startFrame, data.endFrame);
  }
  
  return sprite;
}

// Use the sprite in your game
const playerCharacter = setupCharacterSprite();
playerCharacter.playAnimation('idle');
```

## Complex Use Cases

### Generating Full Game Asset Sets

You can use SpriteAI to generate a complete set of assets for a game:

```javascript
async function generateGameAssets(theme) {
  const characters = ['hero', 'villain', 'sidekick'];
  const environments = ['forest', 'castle', 'cave'];
  const assets = {};

  for (const character of characters) {
    assets[character] = await generateCharacterSpritesheet(`${theme} ${character}`);
  }

  for (const environment of environments) {
    assets[environment] = await generateEnvironmentSprites(`${theme} ${environment}`);
  }

  return assets;
}

const fantasyGameAssets = await generateGameAssets('fantasy');
```

### Creating Themed Sprite Collections

You can create collections of sprites with a consistent theme:

```javascript
async function generateThemedSprites(theme, characters, environments) {
  const spriteCollection = {
    characters: {},
    environments: {}
  };

  for (const character of characters) {
    spriteCollection.characters[character] = await generateCharacterSpritesheet(`${theme} ${character}`);
  }

  for (const environment of environments) {
    spriteCollection.environments[environment] = await generateEnvironmentSprites(`${theme} ${environment}`);
  }

  return spriteCollection;
}

const steampunkCollection = await generateThemedSprites(
  'steampunk',
  ['inventor', 'airship captain', 'mechanist'],
  ['airship deck', 'clockwork factory', 'victorian street']
);
```

This function creates a collection of steampunk-themed character and environment sprites, maintaining a consistent style across all generated assets.

By leveraging these advanced techniques, you can create rich, customized sprite assets for your games or applications using the SpriteAI library.