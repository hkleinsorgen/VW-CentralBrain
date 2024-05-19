# VW CentralBrain

A generative AI library for VisualWorks, with a focus on text generation.

Work in progress, still in its infancy.

# Quickstart

## Create an API interface

### OpenAI

```
api := CB.OpenAIInterface apiKey: 'sx-proj-.........'
```

### Google Vertex

```
api := CB.GoogleVertexAIInterface 
	apiKey: 'ya12.........'
	project: 'myproject'
	location: 'us-central1'.
```

### AWS Bedrock

```
api := AWSBedrockInterface
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

```
chat := CB.Chat newWithAPI: api.
chat prompt: 'You are a cheerful assistant that happily answers all questions, no matter how silly they are'.
chat ask: 'How much is the fish?'.
chat complete.
```

### Chat with a specific model

```
chat := Chat newWithModelContext: (api contextForModelNamed: 'anthropic.claude-v2').
chat ask: 'How much is the fish?'.
```

### Multimodal chat

```
image := CB.Image filename: 'Lighthouse.jpg'.
chat := CB.Chat newWithModelContext: api defaultVisionContext.
chat prompt: 'You are an assistant that answers questions regarding images'.
chat ask: 'Please describe what you see in this image' attachment: image.
chat complete.
```

## Compute embeddings

```
document := CB.Document text: 'Smalltalk is a purely object oriented programming language (OOP) that was originally created in the 1970s for educational use, specifically for constructionist learning, but later found use in business.'.
document embeddingsWithApi: api
```