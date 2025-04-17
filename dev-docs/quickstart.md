```markdown
---
title: Quickstart
---

# Quickstart Guide to SpriteAI

Welcome to SpriteAI! This guide will walk you through setting up the SpriteAI library and generating your first sprites.

## Prerequisites

Before you begin, make sure you have the following installed:

*   **Node.js:** (version 16 or higher is recommended). You can download it from [nodejs.org](https://nodejs.org/).
*   **npm** (Node Package Manager): npm is usually bundled with Node.js.
*   **An OpenAI API Key:** You'll need an API key from OpenAI to use the image generation features. You can obtain one from [OpenAI's website](https://openai.com/).

## Installation

1.  **Create a new project directory:**

    ```bash
    mkdir spriteai-project
    cd spriteai-project
    ```

2.  **Initialize a new Node.js project:**

    ```bash
    npm init -y
    ```

3.  **Install the SpriteAI library and its dependencies:**

    ```bash
    npm install spriteai axios jimp openai sharp
    ```

    This command installs `spriteai` along with `axios` (for making HTTP requests), `jimp` (for image manipulation), `openai` (for interacting with the OpenAI API) and `sharp` (for image processing).

## Basic Usage

Here's a basic example of how to generate a sprite using SpriteAI.  This example assumes you are using OpenAI's DALL-E to generate the sprites.

1.  **Create a file named `index.js`:**

    ```bash
    touch index.js
    ```

2.  **Edit `index.js` and add the following code:**

    ```javascript
    import OpenAI from 'openai';
    import sharp from 'sharp';
    import fs from 'fs';

    const openai = new OpenAI({
        apiKey: 'YOUR_OPENAI_API_KEY', // Replace with your actual API key
    });

    async function generateSprite(prompt, size = 256) {
      try {
        const response = await openai.images.generate({
          prompt: prompt,
          n: 1, // Generate one image
          size: `${size}x${size}`, // Size of the image (e.g., 256x256, 512x512, 1024x1024)
        });

        const imageUrl = response.data[0].url;
        console.log('Image URL:', imageUrl);

        // Fetch the image and convert it to a buffer
        const imageResponse = await fetch(imageUrl);
        const imageBuffer = await imageResponse.arrayBuffer();

        // Save the image using sharp
        const filename = 'sprite.png';
        await sharp(Buffer.from(imageBuffer)).toFile(filename);

        console.log(`Sprite saved as ${filename}`);

      } catch (error) {
        console.error('Error generating sprite:', error);
      }
    }

    // Example usage:
    generateSprite("A cute pixel art cat", 256);
    ```

3.  **Replace `YOUR_OPENAI_API_KEY` with your actual OpenAI API key.**

4.  **Run the script:**

    ```bash
    node index.js
    ```

    This will generate an image based on the prompt "A cute pixel art cat" and save it as `sprite.png` in your project directory.

## Understanding the Code

*   **Import statements:** The code imports the necessary modules: `OpenAI` for interacting with the OpenAI API, `sharp` for image processing, and `fs` for file system operations.
*   **`OpenAI` initialization:**  The `OpenAI` object is initialized with your API key.
*   **`generateSprite` function:** This function takes a `prompt` (the description of the sprite you want to generate) and an optional `size` parameter (the size of the generated image) as input.
*   **OpenAI API call:** The `openai.images.generate` method is called to generate the image based on the provided prompt and size.
*   **Error handling:** The `try...catch` block handles any errors that may occur during the image generation process.
*   **Saving the image:** The generated image URL is used to download the image and then it is saved as a png file named `sprite.png` using the `sharp` library.

## Basic Parameters

The `generateSprite` function uses the following parameters:

*   **`prompt`:** A text description of the desired image. This is the most important parameter as it tells the AI what to generate. Be as descriptive as possible for best results.
*   **`size`:** The size of the generated image in pixels.  Common values are `256` (256x256), `512` (512x512), and `1024` (1024x1024).  Larger sizes may require more processing time and resources.

## Next Steps

*   Explore the OpenAI API documentation for more advanced options, such as specifying the image quality or style.
*   Experiment with different prompts to create a variety of sprites.
*   Integrate SpriteAI into your own projects.
```