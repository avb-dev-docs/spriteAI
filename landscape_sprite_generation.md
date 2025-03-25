# Landscape Sprite Generation with SpriteAI

This guide explains how to generate landscape sprites using the SpriteAI library. The `generateLandscapeSprite` function allows you to create diverse and game-ready landscape assets with customizable options.

## Function Overview

```javascript
generateLandscapeSprite(description, options)
```

This asynchronous function generates a landscape sprite based on the provided description and options.

### Parameters

1. `description` (string): A detailed description of the landscape you want to generate.
2. `options` (object): An optional object containing customization parameters.

### Options

The `options` object can include the following properties:

- `size` (string): Output size of the image (default: '1024x1024').
- `style` (string): Art style of the landscape (default: 'pixel-art').
- `timeOfDay` (string): Time setting for the landscape (default: 'day').
- `weather` (string): Weather conditions in the landscape (default: 'clear').
- `perspective` (string): Viewing perspective of the landscape (default: 'side-scrolling').
- `save` (boolean): Whether to save the generated image locally (default: false).
- `removeBackground` (boolean): Whether to remove the background (optional).
- `backgroundColor` (string): The background color to remove (used with `removeBackground`).
- `colorThreshold` (number): Threshold for color removal (used with `removeBackground`).

## Usage Example

Here's a basic example of how to use the `generateLandscapeSprite` function:

```javascript
import { generateLandscapeSprite } from 'spriteAI';

async function createLandscape() {
  const result = await generateLandscapeSprite("A lush forest with a winding river", {
    size: '1024x1024',
    style: 'pixel-art',
    timeOfDay: 'sunset',
    weather: 'clear',
    perspective: 'side-scrolling',
    save: true
  });

  console.log(result);
}

createLandscape();
```

## Customization Tips

1. **Detailed Descriptions**: Provide a clear and detailed description of the landscape you want to generate. Include key elements, atmosphere, and any specific features you want to see.

2. **Art Style**: Experiment with different art styles beyond the default 'pixel-art'. Options might include 'vector', '3d', 'hand-drawn', or 'realistic'.

3. **Time of Day**: Vary the `timeOfDay` option to create different moods. Options include 'day', 'night', 'sunset', and 'dawn'.

4. **Weather Conditions**: Use the `weather` option to add atmosphere. Try 'clear', 'rainy', 'foggy', or 'snowy' for diverse environments.

5. **Perspective**: Change the `perspective` to suit your game's viewpoint. Options include 'side-scrolling', 'top-down', and 'isometric'.

6. **Background Removal**: If you need a transparent background, use the `removeBackground` option along with `backgroundColor` and `colorThreshold` to fine-tune the removal process.

## Return Value

The function returns an object with the following properties:

- `original`: URL of the originally generated image.
- `landscape`: Base64-encoded string of the processed image.
- `metadata`: Object containing details about the generated landscape.

## Best Practices

1. Start with a clear vision of your desired landscape and provide a detailed description.
2. Experiment with different option combinations to achieve the perfect look for your game.
3. Use the `save` option to keep local copies of your generated landscapes for easy access and version control.
4. When removing backgrounds, adjust the `colorThreshold` value to balance between removing the background and preserving important details.
5. Generate multiple variations of the same landscape with different time of day and weather settings to create a dynamic game environment.

By leveraging these customization options and tips, you can create a wide variety of landscape sprites suitable for different game styles and atmospheres.