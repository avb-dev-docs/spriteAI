```markdown
```
---
title: Landscape Spritesheet Generation
description: Documentation for the generateLandscapeSprite function.
---

# Landscape Spritesheet Generation

This document describes the `generateLandscapeSprite` function, which generates landscape sprites using DALL-E.

## Function Signature

```javascript
generateLandscapeSprite(description, options = {})
```

## Parameters

| Parameter       | Type   | Description                                                                                                                                                                                             | Default Value | Example                                                                                                                                                              |
|-----------------|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `description`   | string | A textual description of the landscape you want to generate.  This is the primary input that guides DALL-E's image creation.                                                                        |               | `"a serene forest with a hidden path"` , `"a futuristic city at sunset"`                                                                                          |
| `options`       | object | An optional object containing various configuration options for the sprite generation.                                                                                                               | `{}`          | See details below.                                                                                                                                                   |

### Options Object

The `options` object can contain the following properties:

| Property          | Type    | Description                                                                                                                                               | Default Value | Example                                                                        |
|-------------------|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------------------------------------------------------------------------|
| `size`            | string  | The size of the output image.                                                                                                                              | `"1024x1024"`  | `"512x512"`, `"256x256"`                                                       |
| `style`           | string  | The art style of the landscape.                                                                                                                            | `"pixel-art"` | `"photorealistic"`, `"cartoon"`                                                 |
| `timeOfDay`       | string  | The time of day for the landscape scene.                                                                                                                    | `"day"`       | `"night"`, `"sunset"`, `"dawn"`                                                 |
| `weather`         | string  | The weather conditions for the landscape.                                                                                                                   | `"clear"`     | `"rainy"`, `"foggy"`, `"snowy"`                                                |
| `perspective`     | string  | The perspective of the landscape.                                                                                                                          | `"side-scrolling"` | `"top-down"`, `"isometric"`                                                   |
| `save`            | boolean | Whether to save the generated image to the `assets` directory.                                                                                             | `false`       | `true`                                                                         |
| `removeBackground`| boolean | Whether to remove the background of the generated image.                                                                                                   | `false`       | `true`                                                                         |
| `backgroundColor` | string  | The target color to remove when `removeBackground` is true.  CSS color name or Hex code.                                                                 | `"#FFFFFF"`   | `"red"`, `"#00FF00"`                                                             |
| `colorThreshold`  | number  | The color difference threshold for background removal.  A value between 0 and 1, where lower values make the removal more precise.                          | `0.1`         | `0.05`, `0.2`                                                                    |

## Return Value

The function returns a promise that resolves to an object with the following properties:

| Property      | Type   | Description                                                                                                       |
|---------------|--------|-------------------------------------------------------------------------------------------------------------------|
| `original`    | string | The URL of the original image generated by DALL-E.                                                              |
| `landscape`   | string | A base64 encoded string representing the landscape image in PNG format (background removed if `removeBackground` is set to true). |
| `metadata`    | object | An object containing metadata about the generated image, including description, style, time of day, weather, perspective, and dimensions. |

## Example Usage

```javascript
import { generateLandscapeSprite } from './index.js';

async function generateExample() {
  try {
    const result = await generateLandscapeSprite(
      "a desert oasis with palm trees and a clear blue pond",
      {
        size: "512x512",
        style: "pixel-art",
        timeOfDay: "day",
        weather: "clear",
        perspective: "side-scrolling",
        removeBackground: true,
        backgroundColor: "#FFFFFF",
        colorThreshold: 0.05,
        save: true
      }
    );

    console.log("Original image URL:", result.original);
    console.log("Landscape data:", result.landscape);
    console.log("Metadata:", result.metadata);
  } catch (error) {
    console.error("Error generating landscape:", error);
  }
}

generateExample();
```

This example generates a pixel-art landscape of a desert oasis with a white background removed and saves it to the assets folder.

## Error Handling

The function may throw errors if:

-   DALL-E fails to generate an image.
-   There are issues with the network request.
-   The sharp library encounters an error during image processing.

Ensure you wrap the function call in a `try...catch` block to handle potential errors gracefully.

## Notes

- The `assets` directory is created at the root of your project if it does not already exist, when the `save` parameter is set to true.
- Temporary files (`temp_input.png`, `temp_output.png`) are created and then deleted when `removeBackground` is `true`.
```