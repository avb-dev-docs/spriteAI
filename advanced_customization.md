# Advanced Customization

This guide provides advanced techniques for customizing SpriteAI outputs, including fine-tuning prompts, adjusting image processing parameters, and extending the library's functionality. We'll also cover examples of creating custom sprite types and integrating with other game development tools.

## Table of Contents
1. [Fine-tuning Prompts](#fine-tuning-prompts)
2. [Adjusting Image Processing Parameters](#adjusting-image-processing-parameters)
3. [Extending Library Functionality](#extending-library-functionality)
4. [Creating Custom Sprite Types](#creating-custom-sprite-types)
5. [Integrating with Game Development Tools](#integrating-with-game-development-tools)

## Fine-tuning Prompts

The quality and specificity of the generated sprites heavily depend on the prompts provided to the AI model. Here are some tips for fine-tuning your prompts:

### Character Spritesheets

When generating character spritesheets, you can enhance the prompt by specifying detailed characteristics:

```javascript
const description = "A steampunk inventor with brass goggles, wearing a brown leather apron";
const options = {
  states: ['idle', 'work', 'think', 'celebrate'],
  style: 'pixel-art',
  direction: 'left'
};

const result = await generateCharacterSpritesheet(description, options);
```

### Environment Sprites

For environment sprites, focus on the theme and specific elements you want to include:

```javascript
const description = "Ancient ruins overgrown with bioluminescent plants";
const options = {
  elements: 6,
  style: 'hand-drawn',
  theme: 'sci-fi'
};

const result = await generateEnvironmentSprites(description, options);
```

## Adjusting Image Processing Parameters

### Background Removal

The `removeBackgroundColor` function allows for customization of background removal. You can adjust the `colorThreshold` to fine-tune the removal process:

```javascript
const options = {
  removeBackground: true,
  backgroundColor: '#FFFFFF',
  colorThreshold: 0.2  // Increase for more aggressive removal
};

const result = await generateLandscapeSprite(description, options);
```

### Spritesheet Generation

When generating spritesheets, you can adjust the padding between sprites:

```javascript
const options = {
  padding: 2,  // Increase for more space between sprites
  framesPerState: 8  // Increase for more detailed animations
};

const result = await generateCharacterSpritesheet(description, options);
```

## Extending Library Functionality

To extend the library's functionality, you can create wrapper functions or add new features. Here's an example of a wrapper function that generates a character spritesheet with mirrored animations:

```javascript
async function generateMirroredCharacterSpritesheet(description, options = {}) {
  const result = await generateCharacterSpritesheet(description, options);
  
  // Mirror the spritesheet horizontally
  const mirroredSpritesheet = await sharp(Buffer.from(result.spritesheet.split(',')[1], 'base64'))
    .flop()
    .toBuffer();

  return {
    ...result,
    mirroredSpritesheet: `data:image/png;base64,${mirroredSpritesheet.toString('base64')}`
  };
}
```

## Creating Custom Sprite Types

You can create custom sprite types by combining existing functionalities. Here's an example of generating a composite sprite for a game item:

```javascript
async function generateItemSprite(description, options = {}) {
  const itemResult = await generateEnvironmentSprites(description, { ...options, elements: 1 });
  const backgroundResult = await generateLandscapeSprite("Mystical glow effect", { ...options, removeBackground: true });

  // Combine item and background
  const compositeBuffer = await sharp(Buffer.from(itemResult.tileset.split(',')[1], 'base64'))
    .composite([{ input: Buffer.from(backgroundResult.landscape.split(',')[1], 'base64') }])
    .toBuffer();

  return {
    itemSprite: `data:image/png;base64,${compositeBuffer.toString('base64')}`,
    metadata: {
      ...itemResult.metadata,
      background: backgroundResult.metadata
    }
  };
}
```

## Integrating with Game Development Tools

SpriteAI can be integrated with various game development tools to streamline your workflow. Here are some examples:

### Phaser Integration

To use SpriteAI-generated assets in Phaser, you can create a preload function:

```javascript
function preloadSpriteAIAssets(scene) {
  scene.load.on('filecomplete', (key, type, data) => {
    if (type === 'image' && key.startsWith('spriteai_')) {
      // Process SpriteAI metadata and create animations
      const metadata = JSON.parse(localStorage.getItem(key + '_metadata'));
      if (metadata && metadata.frameData) {
        Object.keys(metadata.frameData).forEach(state => {
          const frameData = metadata.frameData[state];
          scene.anims.create({
            key: key + '_' + state,
            frames: scene.anims.generateFrameNumbers(key, {
              start: frameData.startFrame,
              end: frameData.endFrame
            }),
            frameRate: 10,
            repeat: -1
          });
        });
      }
    }
  });
}
```

### Unity Integration

For Unity integration, you can create a custom editor script to import SpriteAI-generated assets:

```csharp
using UnityEngine;
using UnityEditor;
using System.IO;

public class SpriteAIImporter : EditorWindow
{
    [MenuItem("SpriteAI/Import Assets")]
    public static void ShowWindow()
    {
        GetWindow<SpriteAIImporter>("SpriteAI Importer");
    }

    void OnGUI()
    {
        if (GUILayout.Button("Import SpriteAI Assets"))
        {
            string path = EditorUtility.OpenFilePanel("Select SpriteAI Asset", "", "png");
            if (path.Length != 0)
            {
                ImportSpriteAIAsset(path);
            }
        }
    }

    void ImportSpriteAIAsset(string path)
    {
        // Import texture
        string fileName = Path.GetFileNameWithoutExtension(path);
        string destPath = "Assets/SpriteAI/" + fileName + ".png";
        FileUtil.CopyFileOrDirectory(path, destPath);
        AssetDatabase.ImportAsset(destPath);

        // Create sprite from texture
        Texture2D texture = AssetDatabase.LoadAssetAtPath<Texture2D>(destPath);
        Sprite sprite = Sprite.Create(texture, new Rect(0, 0, texture.width, texture.height), new Vector2(0.5f, 0.5f));
        AssetDatabase.CreateAsset(sprite, "Assets/SpriteAI/" + fileName + "_Sprite.asset");

        AssetDatabase.SaveAssets();
        AssetDatabase.Refresh();
    }
}
```

By leveraging these advanced customization techniques, you can create unique and tailored sprites for your game development projects using SpriteAI.