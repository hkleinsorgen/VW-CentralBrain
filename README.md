# VW CentralBrain

A generative AI library for VisualWorks, with a focus on text generation.

Work in progress, still in its infancy.

# Quickstart

## Create an API interface

### OpenAI

```
api := CB.OpenAIInterface apiKey: 'sx-proj-.........'
```

### Google Gemini

```
api := CB.GoogleGeminiInterface apiKey: 'AIza.........'
```

Beta:

```
api := CB.GoogleGeminiBetaInterface apiKey: 'AIza.........'
```

### Google Vertex

```
api := CB.GoogleVertexAIInterface 
	accessToken: 'ya12.........'
	project: 'myproject'
	location: 'us-central1'.
```

You can get a token with the gcloud tool by executing `gcloud auth print-access-token`. These tokens are short lived. The renewal mechanism is currently beyond the scope of this package.

### AWS Bedrock

```
api := CB.AWSBedrockInterface
	region: 'us-east-1'
	accessKey: 'AK.........'
	secretKey: 'asm.........'.
```

### Azure

Not yet tested

## Available models

```
api availableModels
```

## Chat

### Ask a question

```
chat := Chat newWithDefaultContext.
chat ask: 'What is the age of the universe?'.
```
### Give instructions

```
chat := CB.Chat newWithAPI: api.
chat instructions: 'You are a cheerful assistant that happily answers all questions, no matter how silly they are'.
chat ask: 'How much is the fish?'.
```

Note that instructions are not supported by all APIs / models.

### Chat with a specific model

```
chat := CB.Chat newWithModelContext: (api contextForModelNamed: 'anthropic.claude-v2').
chat ask: 'What is the meaning of life?'.
```

### Multimodal chat

```
image := CB.Image url: 'https://smalltalk-80.org/image/poster-splash.jpg'.
chat := CB.Chat newWithModelContext: api defaultVisionContext.
chat ask: 'Please describe what you see in this image' attachment: image.
```

## Function calls

```
chat := Chat newWithDefaultContext.
chat addTool: (CB.Tool 
	named: 'get_price' 
	description: 'Get the price for any item'
	parameters: (Array with: (CB.ToolParameter named: 'item'))).
chat addTool: (CB.Tool 
	named: 'get_weight' 
	description: 'Get the weight of items'
	parameters: (Array with: (CB.ToolParameter named: 'item') with: (CB.ToolParameter named: 'amount'))).
chat ask: 'What is the weight of three halibut?'.
```

## Compute embeddings

```
document := CB.Document text: 'Smalltalk is a purely object oriented programming language (OOP) that was originally created in the 1970s for educational use, specifically for constructionist learning, but later found use in business.'.
document embeddingsWithApi: api
```

# Support matrix

| Feature | OpenAI | Azure OpenAI | AWS Bedrock | Google  Gemini | Google Vertex | 
| ------- | ------ | ------- | ------- | -------------- | ------------- |
| Text chat | ✅ | Not tested |  ✅ | ✅  | ✅ |
| Chat instructions | ✅ | Not tested |  ✅ (Titan only) | ✅ (Beta only)  | ❌ | 
| Multimodal chat | ✅ | Not tested | ❌  | ✅  | ✅ |
| Function calls | ✅ | Not tested | ❌  | ❌  | ❌ |
| Create embeddings | ✅ | Not tested |  ✅ | ✅  | ✅ |
| List models |  ✅ | Not tested |  ✅ | ✅  | ❌ |
