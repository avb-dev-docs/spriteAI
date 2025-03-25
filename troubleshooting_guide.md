# Troubleshooting Guide for SpriteAI

This guide addresses common issues that users might encounter when working with SpriteAI, including problems related to image generation, processing, and integration. Follow the solutions provided for each issue to resolve them quickly.

## Table of Contents

1. [Image Generation Issues](#image-generation-issues)
2. [Image Processing Problems](#image-processing-problems)
3. [Integration Challenges](#integration-challenges)
4. [Performance Concerns](#performance-concerns)
5. [Error Messages](#error-messages)

## Image Generation Issues

### Unexpected or Low-Quality Outputs

**Problem**: The generated sprites or landscapes don't match the expected quality or style.

**Solution**:
1. Refine your prompt: Be more specific about the desired style, details, and context.
2. Adjust the `style` parameter: Try different styles like 'pixel-art', 'vector', or '3d'.
3. Modify the `size` parameter: Increase the resolution for more detailed sprites.

Example:

```javascript
const result = await generateCharacterSpritesheet("medieval knight with shining armor", {
  style: "pixel-art",
  size: "2048x2048"
});
```

### Missing Animation States

**Problem**: Some expected animation states are not present in the generated spritesheet.

**Solution**:
1. Explicitly specify the desired states in the `states` array.
2. Ensure you're not exceeding the maximum number of supported states.

Example:

```javascript
const result = await generateCharacterSpritesheet("ninja character", {
  states: ['idle', 'walk', 'run', 'attack', 'jump'],
  framesPerState: 4
});
```

## Image Processing Problems

### Background Removal Issues

**Problem**: The background is not properly removed from generated sprites.

**Solution**:
1. Adjust the `colorThreshold` when using the `removeBackgroundColor` function.
2. Ensure the `targetColor` matches the background color of your sprite.

Example:

```javascript
await removeBackgroundColor(
  'input.png',
  'output.png',
  '#FFFFFF',  // White background
  0.1  // Adjust this threshold as needed
);
```

### Inconsistent Sprite Sizes

**Problem**: Sprites within a spritesheet have inconsistent sizes.

**Solution**:
1. Use the `padding` option to ensure clear separation between frames.
2. Verify that the `framesPerState` and `states` parameters are set correctly.

Example:

```javascript
const result = await generateCharacterSpritesheet("robot character", {
  padding: 2,
  framesPerState: 6,
  states: ['idle', 'walk', 'run']
});
```

## Integration Challenges

### Incorrect File Paths

**Problem**: Generated assets are not being saved in the expected location.

**Solution**:
1. Check that the `save` option is set to `true`.
2. Verify the current working directory using `process.cwd()`.
3. Ensure the `assets` folder exists in your project structure.

Example:

```javascript
const result = await generateLandscapeSprite("forest scene", {
  save: true,
  // This will save the file in the 'assets' folder of your project
});
```

### Incompatible Image Formats

**Problem**: Generated images are not compatible with your game engine or framework.

**Solution**:
1. Use the `sharp` library to convert the image to a compatible format.
2. Adjust the output format when saving the file.

Example:

```javascript
const sharp = require('sharp');
const spritesheet = result.spritesheet;
await sharp(Buffer.from(spritesheet.split(',')[1], 'base64'))
  .toFormat('png')
  .toFile('compatible_spritesheet.png');
```

## Performance Concerns

### Slow Generation Times

**Problem**: Sprite or landscape generation is taking too long.

**Solution**:
1. Reduce the `size` parameter for faster generation.
2. Limit the number of `states` or `elements` in your requests.
3. Implement caching for frequently used sprites.

Example:

```javascript
const result = await generateCharacterSpritesheet("simple character", {
  size: "512x512",
  states: ['idle', 'walk'],  // Reduced number of states
  framesPerState: 4  // Reduced frames per state
});
```

### High Memory Usage

**Problem**: The application is consuming too much memory when processing large spritesheets.

**Solution**:
1. Process images in smaller batches.
2. Implement streaming for large file operations.
3. Use the `sharp` library for more efficient image processing.

Example:

```javascript
const sharp = require('sharp');
const streamableSprite = await sharp(spriteBuffer)
  .resize(1024, 1024)
  .toBuffer();
```

## Error Messages

### "OpenAI API Error"

**Problem**: Requests to the OpenAI API are failing.

**Solution**:
1. Check your OpenAI API key and ensure it's correctly set.
2. Verify your API usage limits and billing status.
3. Implement proper error handling for API requests.

Example:

```javascript
try {
  const result = await generateCharacterSpritesheet("warrior");
} catch (error) {
  if (error.response) {
    console.error(`OpenAI API error: ${error.response.data.error.message}`);
  } else {
    console.error(`Error: ${error.message}`);
  }
}
```

### "File System Error"

**Problem**: Unable to save generated assets to the file system.

**Solution**:
1. Ensure your application has write permissions for the target directory.
2. Check for available disk space.
3. Verify that the file path is correctly constructed.

Example:

```javascript
const fs = require('fs').promises;
const path = require('path');

try {
  const dir = path.join(process.cwd(), 'assets');
  await fs.mkdir(dir, { recursive: true });
  await fs.writeFile(path.join(dir, 'sprite.png'), spriteBuffer);
} catch (error) {
  console.error(`File system error: ${error.message}`);
}
```

By following this troubleshooting guide, you should be able to resolve most common issues encountered when working with SpriteAI. If you continue to experience problems, please reach out to our support team or consult the API documentation for more detailed information.