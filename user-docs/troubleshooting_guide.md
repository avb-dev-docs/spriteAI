# Troubleshooting Guide for SpriteAI

This guide covers common issues you might encounter when using SpriteAI, along with solutions and debugging tips. If you're experiencing problems, follow the steps below to diagnose and resolve them.

## Table of Contents

1. [API-Related Issues](#api-related-issues)
2. [Image Processing Errors](#image-processing-errors)
3. [Integration Challenges](#integration-challenges)
4. [General Debugging Tips](#general-debugging-tips)
5. [Additional Resources](#additional-resources)

## API-Related Issues

### Authentication Errors

If you're encountering authentication errors when making API calls:

1. Double-check your API key:
   ```javascript
   const openAiObject = new OpenAI();
   ```
   Ensure that you've set the API key correctly in your environment variables or configuration file.

2. Verify API key permissions:
   Make sure your API key has the necessary permissions to access the SpriteAI endpoints.

3. Check for API key expiration:
   If your key has expired, generate a new one from your account dashboard.

### Rate Limiting

If you're hitting rate limits:

1. Implement exponential backoff:
   ```javascript
   async function makeApiCallWithRetry(fn, maxRetries = 3) {
     for (let i = 0; i < maxRetries; i++) {
       try {
         return await fn();
       } catch (error) {
         if (error.response && error.response.status === 429) {
           await new Promise(resolve => setTimeout(resolve, Math.pow(2, i) * 1000));
         } else {
           throw error;
         }
       }
     }
     throw new Error('Max retries reached');
   }
   ```

2. Optimize your API usage:
   Batch requests when possible and cache results to reduce API calls.

## Image Processing Errors

### Invalid Image Format

If you're getting errors related to image formats:

1. Check the input image format:
   Ensure that you're using supported image formats (PNG, JPEG, WebP).

2. Verify the image buffer:
   ```javascript
   const imgBuffer = Buffer.from(res.data);
   ```
   Make sure the buffer contains valid image data.

### Background Removal Issues

If the background removal is not working as expected:

1. Adjust the color threshold:
   ```javascript
   await removeBackgroundColor(
     tempInputPath, 
     tempOutputPath, 
     options.backgroundColor || '#FFFFFF', 
     options.colorThreshold || 0.1
   );
   ```
   Try increasing the `colorThreshold` value if the background is not being fully removed.

2. Check the target color:
   Ensure that the `backgroundColor` option is set to the correct color value of the background you want to remove.

## Integration Challenges

### Module Import Errors

If you're having trouble importing the SpriteAI module:

1. Verify the import statement:
   ```javascript
   import { generateCharacterSpritesheet, generateLandscapeSprite } from 'spriteai';
   ```
   Make sure you're using the correct import syntax and module name.

2. Check your project's dependencies:
   Ensure that SpriteAI is listed in your `package.json` and that you've run `npm install` or `yarn install`.

### Incorrect Function Usage

If you're getting errors when calling SpriteAI functions:

1. Review the function signatures:
   ```javascript
   generateCharacterSpritesheet(description, options)
   generateLandscapeSprite(description, options)
   ```
   Make sure you're passing the correct arguments in the right order.

2. Check the options object:
   Verify that you're using the correct option names and values as defined in the API documentation.

## General Debugging Tips

1. Enable verbose logging:
   Add console logs or use a logging library to track the execution flow and identify where errors occur.

2. Use try-catch blocks:
   Wrap API calls and image processing operations in try-catch blocks to handle and log errors gracefully.

3. Validate input data:
   Implement input validation to catch and handle invalid parameters before they cause errors in the SpriteAI functions.

4. Check for updates:
   Ensure you're using the latest version of SpriteAI, as some issues may have been resolved in recent updates.

## Additional Resources

- [SpriteAI API Documentation](https://docs.spriteai.com)
- [OpenAI API Reference](https://platform.openai.com/docs/api-reference)
- [Sharp Image Processing Library](https://sharp.pixelplumbing.com/)
- [Jimp Image Manipulation](https://github.com/oliver-moran/jimp)

If you're still experiencing issues after following this troubleshooting guide, please reach out to our support team at support@spriteai.com or open an issue on our [GitHub repository](https://github.com/spriteai/spriteai).