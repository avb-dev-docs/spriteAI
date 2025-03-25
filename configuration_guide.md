# Configuration Guide

This guide explains how to configure SpriteAI for different use cases. We'll cover setting up API keys, customizing output directories, and configuring default options.

## Table of Contents

1. [Setting Up API Keys](#setting-up-api-keys)
2. [Customizing Output Directories](#customizing-output-directories)
3. [Configuring Default Options](#configuring-default-options)
4. [Environment Variables](#environment-variables)

## Setting Up API Keys

SpriteAI uses OpenAI's API for generating images. To use the library, you need to set up your OpenAI API key.

1. Sign up for an OpenAI account and obtain your API key from the OpenAI dashboard.
2. Set the API key as an environment variable:

```bash
export OPENAI_API_KEY=your_api_key_here
```

Alternatively, you can set the API key programmatically:

```javascript
import OpenAI from "openai";

const openAiObject = new OpenAI({
  apiKey: 'your_api_key_here'
});
```

## Customizing Output Directories

By default, SpriteAI saves generated assets in the `assets` directory within your current working directory. You can customize this by modifying the `save` option when calling the generation functions.

Example:

```javascript
import path from 'path';

const options = {
  save: true,
  outputDir: path.join(process.cwd(), 'custom_assets')
};

const result = await generateCharacterSpritesheet('hero character', options);
```

## Configuring Default Options

You can configure default options for sprite generation by creating a configuration file or setting them programmatically.

### Character Spritesheet Options

```javascript
const defaultOptions = {
  states: ['idle', 'walk', 'run', 'attack'],
  framesPerState: 6,
  size: '1024x1024',
  style: 'pixel-art',
  padding: 1,
  direction: 'right'
};

const result = await generateCharacterSpritesheet('hero character', defaultOptions);
```

### Environment Sprites Options

```javascript
const defaultOptions = {
  elements: 4,
  size: '1024x1024',
  style: 'pixel-art',
  padding: 1,
  theme: 'fantasy'
};

const result = await generateEnvironmentSprites('forest tileset', defaultOptions);
```

## Environment Variables

SpriteAI uses the following environment variables:

- `OPENAI_API_KEY`: Your OpenAI API key (required)
- `SPRITE_AI_OUTPUT_DIR`: Custom output directory for saved assets (optional)

You can set these variables in your shell or use a `.env` file in your project root:

```
OPENAI_API_KEY=your_api_key_here
SPRITE_AI_OUTPUT_DIR=/path/to/custom/output
```

Remember to add the `.env` file to your `.gitignore` to keep your API key secure.

For more detailed information on using SpriteAI, refer to the API documentation and example usage in the project's README.