---
title: Troubleshooting and FAQs
description: Common issues, solutions, and frequently asked questions about SpriteAI
---

# Troubleshooting and FAQs

This guide addresses common issues that SpriteAI users may encounter during installation, sprite generation, or API usage. It also includes solutions to potential errors, performance tips, and answers to frequently asked questions about the library's capabilities and limitations.

## Table of Contents

1. [Installation Issues](#installation-issues)
2. [Sprite Generation Problems](#sprite-generation-problems)
3. [API Usage Errors](#api-usage-errors)
4. [Performance Optimization](#performance-optimization)
5. [Frequently Asked Questions](#frequently-asked-questions)

## Installation Issues

### Error: Unable to locate specified dependency

If you encounter an error related to missing dependencies during installation, try the following:

1. Ensure you have the latest version of Node.js installed.
2. Clear your npm cache:
   ```
   npm cache clean --force
   ```
3. Reinstall the dependencies:
   ```
   npm install
   ```

### Error: Python is not installed or not found in PATH

SpriteAI relies on some packages that require Python for installation. If you encounter this error:

1. Install Python from the [official website](https://www.python.org/downloads/).
2. Ensure Python is added to your system's PATH.
3. Restart your terminal or command prompt.
4. Retry the installation.

## Sprite Generation Problems

### Error: DALL-E API request failed

If you encounter issues with DALL-E API requests:

1. Check your OpenAI API key and ensure it's correctly set in your environment variables.
2. Verify your OpenAI account has sufficient credits.
3. Check the OpenAI status page for any ongoing service issues.

### Unexpected sprite output

If the generated sprites don't match your expectations:

1. Review your prompt and make it more specific.
2. Adjust the `style` parameter in the options object.
3. Try increasing the `size` parameter for more detailed output.

Example of a more specific prompt:

```javascript
const description = "A pixelated warrior with a red cape and golden sword";
const options = {
  style: "pixel-art",
  size: "1024x1024"
};
const result = await generateCharacterSpritesheet(description, options);
```

## API Usage Errors

### TypeError: Cannot read property 'X' of undefined

This error often occurs when trying to access properties of an undefined object. Common causes include:

1. Incorrect function names or parameters.
2. Forgetting to await asynchronous functions.

Ensure you're using the correct function names and awaiting promises:

```javascript
// Correct usage
const states = await fetchAvailableAnimationStyles();

// Incorrect usage
const states = fetchAvailableAnimationStyles(); // Missing await
```

### Error: Invalid API key

If you receive an "Invalid API key" error:

1. Double-check your OpenAI API key.
2. Ensure the API key is correctly set in your environment variables.
3. Verify that you're not accidentally exposing your API key in your code.

## Performance Optimization

1. **Caching**: Implement caching for frequently used sprites to reduce API calls.
2. **Batch Processing**: When generating multiple sprites, use batch processing to reduce overhead.
3. **Image Optimization**: Use the `sharp` library to optimize generated images for web use.

Example of image optimization:

```javascript
import sharp from 'sharp';

// After generating a sprite
const optimizedSprite = await sharp(spriteBuffer)
  .resize(800, 600) // Resize if needed
  .webp({ quality: 80 }) // Convert to WebP format
  .toBuffer();
```

## Frequently Asked Questions

### Q: What art styles does SpriteAI support?

A: SpriteAI supports various styles including pixel-art, vector, 3D, hand-drawn, and anime. You can specify the style using the `style` option when generating sprites.

### Q: Can I generate environment sprites?

A: Yes, you can use the `generateEnvironmentSprites` function to create environment assets. This function allows you to specify the number of elements, style, and theme.

### Q: How can I remove the background from generated sprites?

A: SpriteAI includes a `removeBackgroundColor` function that you can use to remove backgrounds. Here's an example:

```javascript
await removeBackgroundColor(
  inputPath,
  outputPath,
  '#FFFFFF', // Background color to remove
  0.1 // Color threshold
);
```

### Q: What is the maximum resolution for generated sprites?

A: The maximum resolution is currently 1024x1024 pixels, as defined by the DALL-E API limitations.

### Q: Can I customize the animation states for character spritesheets?

A: Yes, you can specify custom animation states using the `states` option in the `generateCharacterSpritesheet` function:

```javascript
const options = {
  states: ['idle', 'walk', 'jump', 'attack'],
  framesPerState: 8
};
const result = await generateCharacterSpritesheet(description, options);
```

### Q: How can I ensure consistent character size across all frames?

A: SpriteAI attempts to maintain consistent character size, but you can improve consistency by:

1. Providing a detailed description of the character's size in your prompt.
2. Using the `padding` option to add space between frames.
3. Post-processing the spritesheet to normalize character sizes if needed.

For any issues not covered in this guide, please refer to the SpriteAI GitHub repository or contact our support team.