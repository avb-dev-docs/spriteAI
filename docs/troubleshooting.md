# Troubleshooting Guide for SpriteAI

This guide addresses common issues users might encounter when using SpriteAI, provides solutions, and offers tips for diagnosing and resolving problems.

## Table of Contents

1. [API Errors](#api-errors)
2. [Unexpected Sprite Generation Results](#unexpected-sprite-generation-results)
3. [Integration Challenges](#integration-challenges)
4. [Frequently Asked Questions (FAQ)](#frequently-asked-questions-faq)

## API Errors

### OpenAI API Connection Issues

If you're experiencing connection problems with the OpenAI API, try the following:

1. Check your internet connection.
2. Verify that your OpenAI API key is valid and correctly set.
3. Ensure you haven't exceeded your API rate limits or quota.

If the issue persists, you may see an error like this:

```javascript
Error: Request failed with status code 401
```

This usually indicates an authentication problem. Double-check your API key and make sure it's correctly set in your environment variables or configuration file.

### Axios Request Failures

If you encounter issues with Axios requests, such as:

```javascript
Error: Request failed with status code 500
```

This might be due to server-side issues. Try the following:

1. Retry the request after a short delay.
2. Check if the OpenAI service status page reports any ongoing issues.
3. Verify that your request payload is correctly formatted.

## Unexpected Sprite Generation Results

### Inconsistent Sprite Sizes

If you notice that your generated sprites have inconsistent sizes across frames, try adjusting the `framesPerState` and `size` options in your `generateCharacterSpritesheet` function call:

```javascript
const result = await generateCharacterSpritesheet("character description", {
  framesPerState: 4,
  size: "512x512"
});
```

Reducing the number of frames or the overall size can sometimes help maintain consistency.

### Unwanted Background Colors

If your sprites have unwanted background colors, you can use the `removeBackgroundColor` function to clean them up. Here's an example:

```javascript
await removeBackgroundColor(
  'input_image.png',
  'output_image.png',
  '#FFFFFF',
  0.1
);
```

Adjust the color threshold (the last parameter) to fine-tune the background removal process.

## Integration Challenges

### Module Import Issues

If you're having trouble importing the SpriteAI functions, ensure that you're using the correct import syntax for ES modules:

```javascript
import { generateCharacterSpritesheet, generateEnvironmentSprites } from 'spriteai';
```

If you're using CommonJS, you'll need to use `require` instead:

```javascript
const { generateCharacterSpritesheet, generateEnvironmentSprites } = require('spriteai');
```

### Saving Generated Sprites

To save generated sprites, make sure you set the `save` option to `true` and have write permissions in your project's `assets` directory:

```javascript
const result = await generateCharacterSpritesheet("character description", {
  save: true
});
```

The sprite will be saved in the `assets` folder of your current working directory.

## Frequently Asked Questions (FAQ)

### Q: What image formats does SpriteAI support?
A: SpriteAI generates PNG images by default. The `sharp` library is used for image processing, which supports a wide range of formats for input and output.

### Q: Can I customize the animation states for character spritesheets?
A: Yes, you can customize the animation states by passing a `states` array in the options:

```javascript
const result = await generateCharacterSpritesheet("character description", {
  states: ['idle', 'walk', 'jump', 'attack']
});
```

### Q: How can I get a list of available animation states?
A: You can use the `fetchAvailableAnimationStates` function to get a list of predefined states:

```javascript
const states = await fetchAvailableAnimationStates();
console.log(states);
```

### Q: Are there limits to the sprite size I can generate?
A: The maximum size is determined by the OpenAI API limitations. Currently, DALL-E 3 supports up to 1024x1024 pixel images. You can specify the size in the options:

```javascript
const result = await generateCharacterSpritesheet("character description", {
  size: '1024x1024'
});
```

### Q: How can I generate environment sprites?
A: Use the `generateEnvironmentSprites` function to create environment tilesets:

```javascript
const result = await generateEnvironmentSprites("forest environment", {
  elements: 6,
  theme: 'fantasy'
});
```

If you encounter any issues not covered in this guide, please check the SpriteAI GitHub repository for the latest updates or open an issue for further assistance.