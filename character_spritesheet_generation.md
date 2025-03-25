# Character Spritesheet Generation

This guide explains how to generate character spritesheets using SpriteAI. You'll learn about available options, customization possibilities, and best practices for achieving desired results.

## Overview

The `generateCharacterSpritesheet` function allows you to create pixel art character spritesheets with various animation states. These spritesheets can be easily integrated into game development projects.

## Function Signature

```javascript
generateCharacterSpritesheet(description: string, options?: object): Promise<object>
```

## Parameters

- `description` (string): A detailed description of the character you want to generate.
- `options` (object, optional): Customization options for the spritesheet generation.

### Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| states | string[] | ['idle', 'walk', 'run', 'attack'] | Animation states to generate |
| framesPerState | number | 6 | Number of frames per animation state |
| size | string | '1024x1024' | Output size of the spritesheet |
| style | string | 'pixel-art' | Art style of the character |
| padding | number | 1 | Padding between sprites |
| direction | string | 'right' | Base direction of the character |
| save | boolean | false | Whether to save the generated image |

## Usage

Here's a basic example of how to use the `generateCharacterSpritesheet` function:

```javascript
import { generateCharacterSpritesheet } from 'spriteAI';

async function createCharacter() {
  const result = await generateCharacterSpritesheet('a cute robot with glowing eyes', {
    states: ['idle', 'walk', 'jump'],
    framesPerState: 8,
    size: '2048x2048',
    style: 'pixel-art',
    direction: 'right',
    save: true
  });

  console.log(result);
}

createCharacter();
```

## Return Value

The function returns a Promise that resolves to an object with the following structure:

```javascript
{
  original: string, // URL of the original generated image
  spritesheet: string, // Base64-encoded PNG data of the processed spritesheet
  metadata: {
    states: string[], // List of animation states
    framesPerState: number, // Number of frames per state
    totalFrames: number, // Total number of frames in the spritesheet
    dimensions: {
      width: number,
      height: number
    },
    frameData: {
      [stateName: string]: {
        row: number, // Row index in the spritesheet
        frames: number, // Number of frames for this state
        startFrame: number, // Starting frame index
        endFrame: number // Ending frame index
      }
    }
  }
}
```

## Best Practices

1. **Detailed Descriptions**: Provide clear and specific descriptions for your character to get the best results. Include details about appearance, style, and any unique features.

2. **Consistent States**: Choose animation states that make sense for your character and game. Common states include idle, walk, run, and attack, but you can customize these based on your needs.

3. **Frame Count**: Balance the number of frames per state with the complexity of the animation. More frames can result in smoother animations but may increase file size and processing time.

4. **Size Considerations**: Choose an appropriate size for your spritesheet based on your game's resolution and scaling needs. Larger sizes provide more detail but require more processing time and memory.

5. **Style Consistency**: Stick to a consistent art style throughout your game. The 'pixel-art' style is default and works well for retro-style games, but you can experiment with other styles if needed.

6. **Direction**: Set the base direction of your character to match your game's default orientation. You can always flip the sprites horizontally in your game engine if needed.

7. **Saving Output**: Use the `save` option to automatically save the generated spritesheet to your project's assets folder for easy integration.

## Customization Tips

- **Character Variations**: Generate multiple characters with similar descriptions but slight variations to create diverse NPCs or enemies.
- **Special Animations**: Include unique states like "cast-spell" or "transform" for characters with special abilities.
- **Environmental Adaption**: Create variations of the same character for different environments (e.g., "arctic explorer" vs. "desert explorer").

## Error Handling

The `generateCharacterSpritesheet` function may throw errors if there are issues with the API connection or if invalid options are provided. Always wrap your calls in a try-catch block to handle potential errors gracefully:

```javascript
try {
  const result = await generateCharacterSpritesheet('a battle-worn knight');
  // Process the result
} catch (error) {
  console.error('Error generating character spritesheet:', error);
  // Handle the error (e.g., show a user-friendly message, use a fallback image, etc.)
}
```

## Performance Considerations

Generating spritesheets can be resource-intensive, especially for larger sizes or complex characters. Consider implementing caching mechanisms or generating spritesheets as part of your build process rather than at runtime for better performance in your game.

By following these guidelines and experimenting with different options, you can create high-quality character spritesheets that bring your game characters to life using SpriteAI.