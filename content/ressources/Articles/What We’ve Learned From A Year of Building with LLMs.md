---
title: What We’ve Learned From A Year of Building with LLMs
draft: false
publish: false
tags:
  - 📬
  - 📖
date: 2025-01-16
---
[Link](https://applied-llms.org)

## Prompting

The idea of in-context learning via n-shot prompts is to provide the LLM with examples that demonstrate the task and align outputs to our expectations. A few tips:

- If n is too low, the model may over-anchor on those specific examples, hurting its ability to generalize. As a rule of thumb, aim for n ≥ 5. Don’t be afraid to go as high as a few dozen.  
- Examples should be representative of the prod distribution. If you’re building a movie summarizer, include samples from different genres in roughly the same proportion you’d expect to see in practice.   
- You don’t always need to provide the input-output pairs; examples of desired outputs may be sufficient.      
- If you plan for the LLM to use tools, include examples of using those tools.

In Chain-of-Thought (CoT) prompting, we encourage the LLM to explain its thought process before returning the final answer.

For example, when asking an LLM to summarize a meeting transcript, we can be explicit about the steps:

- First, list out the key decisions, follow-up items, and associated owners in a sketchpad.  
- Then, check that the details in the sketchpad are factually consistent with the transcript.  
- Finally, synthesize the key points into a concise summary.

Providing relevant resources is a powerful mechanism to expand the model’s knowledge base, reduce hallucinations, and increase the user’s trust. Often accomplished via Retrieval Augmented Generation (RAG), providing the model with snippets of text that it can directly utilize in its response is an essential technique.

### Structure your inputs and outputs

When using structured input, be aware that each LLM family has their own preferences. Claude prefers `<xml>` while GPT favors Markdown and JSON. With XML, you can even pre-fill Claude’s responses by providing a `<response>` tag like so.

`messages=[`
    `{`
        `"role": "user",`
        `"content": """Extract the <name>, <size>, <price>, and <color> from this product description into your <response>.`
            `<description>The SmartHome Mini is a compact smart home assistant available in black or white for only $49.99. At just 5 inches wide, it lets you control lights, thermostats, and other connected devices via voice or app—no matter where you place it in your home. This affordable little hub brings convenient hands-free control to your smart devices.`
            `</description>"""`
    `},`
    `{`
        `"role": "assistant",`
        `"content": "<response><name>"`
    `}`
`]`

### Have small prompts that do one thing, and only one thing, well

Just like how we strive (read: struggle) to keep our systems and code simple, so should we for our prompts. Instead of having a single, catch-all prompt for the meeting transcript summarizer, we can break it into steps:

- Extract key decisions, action items, and owners into structured format
- Check extracted details against the original transcription for consistency
- Generate a concise summary from the structured details

### Craft your context tokens

We’ve found that taking the final prompt sent to the model—with all of the context construction, and meta-prompting, and RAG results—putting it on a blank page and just reading it, really helps you rethink your context. We have found redundancy, self-contradictory language, and poor formatting using this method.

The other key optimization is the structure of your context. If your bag-of-docs representation isn’t helpful for humans, don’t assume it’s any good for agents. Think carefully about how you structure your context to underscore the relationships between parts of it and make extraction as simple as possible.

## Information Retrieval / RAG

RAG = [[retrieval-augmented generation]]

