# Landscape Sprite Generation with SpriteAI

This guide covers the process of generating landscape sprites using the SpriteAI library. With this powerful tool, you can create diverse game environments and backgrounds tailored to your specific needs.

## Table of Contents

1. [Introduction](#introduction)
2. [Basic Usage](#basic-usage)
3. [Customization Options](#customization-options)
4. [Examples](#examples)
5. [Advanced Features](#advanced-features)
6. [Best Practices](#best-practices)

## Introduction

The `generateLandscapeSprite` function in SpriteAI allows you to create pixel-art landscape scenes for use in game backgrounds or environments. By providing a description and various customization options, you can generate unique and detailed landscapes that fit your game's aesthetic.

## Basic Usage

To generate a landscape sprite, use the `generateLandscapeSprite` function:

```javascript
import { generateLandscapeSprite } from 'spriteAI';

const result = await generateLandscapeSprite('a lush forest with a winding river');
```

This will generate a default landscape sprite based on the provided description.

## Customization Options

The `generateLandscapeSprite` function accepts an options object that allows you to customize various aspects of the generated landscape:

- `size`: Output size of the image (default: '1024x1024')
- `style`: Art style of the landscape (default: 'pixel-art')
- `timeOfDay`: Time setting for the scene (default: 'day')
- `weather`: Weather conditions in the scene (default: 'clear')
- `perspective`: Viewing angle of the landscape (default: 'side-scrolling')
- `save`: Whether to save the generated image to disk (default: false)

Example with custom options:

```javascript
const options = {
  size: '2048x2048',
  style: 'pixel-art',
  timeOfDay: 'sunset',
  weather: 'rainy',
  perspective: 'isometric',
  save: true
};

const result = await generateLandscapeSprite('a medieval castle on a hilltop', options);
```

## Examples

### 1. Sunny Beach Scene

```javascript
const beachScene = await generateLandscapeSprite('a tropical beach with palm trees', {
  timeOfDay: 'day',
  weather: 'clear',
  perspective: 'side-scrolling'
});
```

### 2. Foggy Mountain Range

```javascript
const mountainScene = await generateLandscapeSprite('a mysterious mountain range', {
  timeOfDay: 'dawn',
  weather: 'foggy',
  perspective: 'side-scrolling'
});
```

### 3. Snowy Forest (Top-down)

```javascript
const snowyForest = await generateLandscapeSprite('a dense pine forest covered in snow', {
  timeOfDay: 'night',
  weather: 'snowy',
  perspective: 'top-down'
});
```

## Advanced Features

### Background Removal

You can automatically remove the background from the generated landscape sprite by setting the `removeBackground` option to `true`:

```javascript
const options = {
  removeBackground: true,
  backgroundColor: '#FFFFFF',
  colorThreshold: 0.1
};

const transparentLandscape = await generateLandscapeSprite('a desert oasis', options);
```

This feature uses the `removeBackgroundColor` function to create a transparent background, which can be useful for layering sprites in your game.

## Best Practices

1. **Descriptive Prompts**: Provide clear and detailed descriptions for the best results.
2. **Consistent Style**: Keep the art style consistent across your game assets by using the same `style` option.
3. **Appropriate Sizing**: Choose an appropriate `size` based on your game's resolution and scaling needs.
4. **Scene Variety**: Experiment with different `timeOfDay` and `weather` combinations to create diverse environments.
5. **Perspective Matching**: Ensure the `perspective` option matches your game's viewpoint for seamless integration.

By leveraging the power of SpriteAI's landscape sprite generation, you can quickly create a wide variety of game environments and backgrounds, saving time and resources in your game development process.