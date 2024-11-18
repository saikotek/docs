---
title: AI Endpoints - Getting started
excerpt: Discover AI Endpoints, the secure serverless platform by OVHcloud for developers to access top AI models with easy-to-use APIs. No AI expertise needed.
updated: 2024-11-18
flag: hidden
---

> [!primary]
>
> AI Endpoints is currently in **Beta**. Although we aim to offer a production-ready product even in this testing phase, service availability may not be guaranteed. Please be careful if you use endpoints for production, as the Beta phase is not yet complete.
>
> AI Endpoints is covered by the **[OVHcloud AI Endpoints Conditions](https://storage.gra.cloud.ovh.net/v1/AUTH_325716a587c64897acbef9a4a4726e38/contracts/48743bf-AI_Endpoints-ALL-1.1.pdf)** and the **[OVHcloud Public Cloud Special Conditions](https://storage.gra.cloud.ovh.net/v1/AUTH_325716a587c64897acbef9a4a4726e38/contracts/d2a208c-Conditions_particulieres_OVH_Stack-WE-9.0.pdf)**.
>

## Introduction

[AI Endpoints](https://endpoints.ai.cloud.ovh.net/) is a serverless platform provided by OVHcloud that offers easy access to a selection of world-renowned, pre-trained AI models. The platform is designed to be simple, secure, and intuitive, making it an ideal solution for developers who want to enhance their applications with AI capabilities without extensive AI expertise or concerns about data privacy.

## Objective

The objective of this guide is to help developers interested in AI quickly and easily get started with [AI Endpoints](https://endpoints.ai.cloud.ovh.net/), the AI serverless platform by OVHcloud.

It explains how to obtain an access token, access AI models, and interact with AI APIs on the [AI Endpoints](https://endpoints.ai.cloud.ovh.net/) platform. By following this guide, you will learn how to integrate AI capabilities into your applications with ease.

## Requirements

- A [Public Cloud project](https://www.ovhcloud.com/en-gb/public-cloud/) in your OVHcloud account
  
## Instructions

### Getting an access token

During the Beta phase of AI Endpoints, obtaining an access token is straightforward and free of charge. This token enables you to use the models available in our catalog and test their integration into your solutions. To obtain an access token, please follow these steps:

- Visit the AI Endpoints access token page.
- Log in using your OVHcloud account credentials.
- Follow the on-screen instructions to generate your access token.

With your access token in hand, you are now ready to access the AI models and their easy-to-use APIs.
  
### Accessing AI models

Once your token has been generated, you can navigate to the [Catalog page](https://endpoints.ai.cloud.ovh.net/catalog) to choose the AI model you want to interact with.

AI Endpoints offers a variety of world-renowned AI models to choose from, including:

- **Assistant**: Use models like CodeLlama, Mistral, Mathstral, and Codestral for tasks like code generation, language translation, and more.
- **Audio analysis**: Automatic Speech Recognition and Text to Speech using NVIDIA's models.
- **Embeddings**: Generate embeddings for use in machine learning applications (BGE base, Multilingual E5).
- **Natural language Processing**: Use models like RoBERTa, Bert, and T5 for NLP tasks like sentiment analysis, entity recognition, and text summarization.
- **Translation**: Translate text using NVIDIA Neural Machine Translation or T5 large.
- **Image Generation**: Generate images using Stable Diffusion XL. WILL IT BE AVAILABLE ? NAME OF THE CATEFGORY ?

*Additional models will be added in the coming months, including multimodal models and object detection models.*

Once you have selected the category of model you want to use, you will be presented with a list of models to choose from. 

For example, if you select the "Assistant" category, you will see a list of available assistant models. 

To access one of them, simply click on the name of the model you want to use. Let's take the "CodeLlama-13b-Instruct-hf" code assistant as our example.

This will take you to a page with several options for interacting with the model. Here is an overview of the available options:

- **Playground**: The "Playground" option allows you to quickly try out the model by playing with it to see if it meets your needs. This is a great way to get a feel for the model without having to use some codes.
- **Documentation**: The "Documentation" option provides detailed documentation for the model, including example Python code that demonstrates how to interact with the model using its API. The documentation also includes the OpenAI specification codes, as our LLM APIs are compatible with the OpenAI specifications.
- **Tutorials**: The "Tutorials" option lists blog articles related to AI Endpoints that you may find helpful in learning how to use the model more effectively. Whether you're building a chatbot with Langchain and JavaScript or creating a video translator app, we provide step-by-step guidance to support your AI projects.
- **API**: The "API" option provides access to POST routes that you can use to send a request to the model and receive an output. Here you can also find information on how to send a correct request to the model.

### Billing and usage

AI Endpoint is always free during its beta phase. 

## Going further

To discover how to build complete and powerful applications using AI Endpoints, explore our dedicated [AI Endpoints blog page](https://blog.ovhcloud.com/tag/ai-endpoints/). This blog offers a wealth of knowledge and inspiration, including the following articles:

- [Create your own Audio Summarizer assistant with AI Endpoints](https://blog.ovhcloud.com/create-audio-summarizer-assistant-with-ai-endpoints/)
- [Implement chatbot memory management with LangChain and AI Endpoints](https://blog.ovhcloud.com/chatbot-memory-management-with-langchain-and-ai-endpoints/)
- [Discover how to create a Retrieval Augmented Generation (RAG) system](https://blog.ovhcloud.com/reference-architecture-retrieval-augmented-generation-rag/)

If you need training or technical assistance to implement our solutions, contact your sales representative or click on [this link](/links/professional-services) to get a quote and ask our Professional Services experts for a custom analysis of your project.

## Feedback

Please feel free to send us your questions, feedback, and suggestions regarding AI Endpoints:

-  In the #ai-endpoints channel of the OVHcloud [Discord server](https://discord.com/invite/vXVurFfwe9), where you can engage with the community and OVHcloud team members.