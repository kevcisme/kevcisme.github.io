---
layout: post
title: Some Papers
---

I've been reading some really great papers lately. I am especially curious about the practical applications of abstractive text summarization. 

[This paper](https://arxiv.org/pdf/1909.08837.pdf). The abstract reads:
> Under special circumstances, summaries should conform to a particular style with patterns, such as court judgments and abstracts in academic papers. To this end, the prototype document-summary pairs can be utilized to generate better summaries. There are two main challenges in this task: (1) the model needs to incorporate learned patterns from the prototype, but (2) should avoid copying contents other than the patternized words— such as irrelevant facts—into the generated summaries. To tackle these challenges, we design a model named Prototype Editing based Summary Generator (PESG). PESG first learns summary patterns and prototype facts by analyzing the correlation between a prototype document and its summary. Prototype facts are then utilized to help extract facts from the input document. Next, an editing generator generates new summary based on the summary pattern or extracted facts. Finally, to address the second challenge, a fact checker is used to estimate mutual information between the input document and generated summary, providing an additional signal for the generator. Extensive experiments conducted on a large-scale real-world text summarization dataset1 show that PESG achieves the state-of-the-art performance in terms of both automatic metrics and human evaluations.

I ran the paper through a summarizer I have been working on and it produced the following:

> 'This paper proposes a pattern-based summarization framework. We call it Prototype Editing.based Summary Generator (PESG) PESG learns summary patterns and prototype.facts by analyzing the correlation between a document and its. summary. Prototype facts are then utilized to help extract facts from the input document. Next, an editing generator generates a new summary based on the summary pattern or extracted facts.'

A few grammatical errors, but I was actually pretty excited about the results! I am looking forward to trying out the concept of the "editing generator."

The next article I'm really enjoying is titled [A Summarization System for Scientific Documents](https://arxiv.org/pdf/1908.11152.pdf)

The abstract:
> We present a novel system providing summaries for Computer Science publications. Through a qualitative user study, we identified the most valuable scenarios for discovery, exploration and understanding of scientific documents. Based on these findings, we built a system that retrieves and summarizes scientific documents for a given information need, either in form of a free-text query or by choosing categorized values such as scientific tasks, datasets and more. Our system ingested 270,000 papers, and its summarization module aims to generate concise yet detailed summaries. We validated our approach with human experts.

My model's summary of the entire paper:
> 'A new system provides summaries for Computer Science publications. The system ingested270,000 papers and its summarization module aims to generate concise yet detailed summaries. We identified the most valuable scenarios for scientific paper usage through a qualitative user study. We interviewed six potential users: a PhD student, two young researchers, two senior researchers and a research strategist.'

Interestingly enough, both of these summaries are heavily weighted to the beginning of text. I think the model might have learned that most of the information about to be conveyed is actually contained in the beginning of the block of text...

So maybe this is a great way to say: wrap it up, Kevin!