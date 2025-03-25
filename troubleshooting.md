# Troubleshooting Guide for SpriteAI

This guide provides solutions for common issues you might encounter when using SpriteAI. If you're experiencing problems with image generation, API errors, file handling, or output quality, you'll find helpful information here.

## Table of Contents
1. [Image Generation Issues](#image-generation-issues)
2. [API Errors](#api-errors)
3. [File Handling Problems](#file-handling-problems)
4. [Output Quality Concerns](#output-quality-concerns)

## Image Generation Issues

### Problem: No image is generated
**Possible causes:**
- Invalid API key
- Network connection issues
- Incorrect function parameters

**Solutions:**
1. Verify your OpenAI API key is correct and has the necessary permissions.
2. Check your internet connection.
3. Ensure you're calling the functions with the correct parameters.

Example of correct function call:
```javascript
const result = await generateCharacterSpritesheet("A knight in shining armor", {
  states: ['idle', 'walk', 'run', 'attack'],
  framesPerState: 6,
  size: '1024x1024'
});
```

### Problem: Generated image doesn't match the description
**Possible causes:**
- Ambiguous or complex description
- AI model limitations

**Solutions:**
1. Simplify and clarify your description.
2. Break down complex characters into multiple generation requests.
3. Use more specific terms in your description.

## API Errors

### Error: "Authorization failed"
**Cause:** Invalid or expired API key

**Solution:**
1. Double-check your API key in your code.
2. Regenerate a new API key from your OpenAI account.
3. Ensure the API key has the necessary permissions for image generation.

### Error: "Rate limit exceeded"
**Cause:** Too many requests in a short time period

**Solution:**
1. Implement rate limiting in your application.
2. Use exponential backoff for retries.
3. Consider upgrading your API plan for higher rate limits.

Example of implementing exponential backoff:
```javascript
const backoff = (retries) => Math.pow(2, retries) * 1000;

async function retryApiCall(fn, maxRetries = 3) {
  for (let i = 0; i < maxRetries; i++) {
    try {
      return await fn();
    } catch (error) {
      if (i === maxRetries - 1) throw error;
      await new Promise(resolve => setTimeout(resolve, backoff(i)));
    }
  }
}
```

## File Handling Problems

### Problem: Unable to save generated images
**Possible causes:**
- Insufficient permissions
- Incorrect file path
- Disk space issues

**Solutions:**
1. Check file write permissions for the target directory.
2. Verify the file path is correct and the directory exists.
3. Ensure sufficient disk space is available.

Example of creating a directory if it doesn't exist:
```javascript
import fs from 'fs';
import path from 'path';

const ensureDirectoryExists = (filePath) => {
  const dirname = path.dirname(filePath);
  if (fs.existsSync(dirname)) {
    return true;
  }
  fs.mkdirSync(dirname, { recursive: true });
};

// Usage
const filePath = '/path/to/your/file.png';
ensureDirectoryExists(filePath);
```

### Problem: Error when processing large images
**Cause:** Insufficient memory for image processing

**Solution:**
1. Increase the Node.js memory limit:
   ```
   node --max-old-space-size=4096 your-script.js
   ```
2. Process images in smaller chunks or lower resolutions.
3. Use streams for large file operations.

## Output Quality Concerns

### Problem: Low-quality or pixelated sprites
**Possible causes:**
- Incorrect size parameter
- Style mismatch

**Solutions:**
1. Adjust the `size` parameter in the options object:
   ```javascript
   const options = {
     size: '1024x1024',  // Increase for higher quality
     style: 'pixel-art'  // Ensure this matches your desired style
   };
   ```
2. Experiment with different styles (e.g., 'vector', '3d', 'hand-drawn').
3. Post-process the generated images using sharp for additional enhancements.

### Problem: Inconsistent character size across frames
**Cause:** AI model variation in generation

**Solution:**
1. Use the `padding` option to add space between frames:
   ```javascript
   const options = {
     padding: 2  // Adjust as needed
   };
   ```
2. Post-process the spritesheet to normalize character sizes.
3. Generate individual frames and manually compose the spritesheet.

If you encounter any issues not covered in this guide, please refer to the API documentation or reach out to our support team for further assistance.