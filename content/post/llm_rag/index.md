---
title: 基于 LLMs 的平台/系统开发
subtitle: 简要介绍 基于 LLMs 平台/系统开发 需要使用的开发框架、评测系统、观测性系统。

# Summary for listings and search engines
summary: 什么是 LLM RAG ？

# Link this post with a project
projects: []

# Date published
date: "2023-11-25T00:00:00Z"

# Date updated
lastmod: "2023-11-25T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

toc: true

pager: true

show_related: true

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: "Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)"
  focal_point: ""
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - Go
  - ASAN

categories:
  - Tutorial
# Book page type (do not modify).
# type: book
---

## 1. 开源框架选择

### 1.1. 🦜️🔗 LangChain

{{< icon name="github" pack="fab" >}}[langchain](https://github.com/langchain-ai/langchain)

`LangChain` 是一个基于语言模型开发应用程序的框架。它可以实现以下功能:

- 数据感知: 将语言模型与其他数据源连接起来
- 主体性: 允许语言模型与其环境进行交互

`LangChain` 的主要价值包括:

- 组件: 用于处理语言模型的抽象，以及每个抽象的一系列实现。组件是模块化且易于使用的，无论您是否使用 `LangChain` 框架的其他部分，都可以轻松使用
- 现成的管道: 用于完成特定高级任务的结构化组件组合

- 集成度高

### 1.2. Haystack

{{< icon name="github" pack="fab" >}}[haystack](https://github.com/deepset-ai/haystack)

- 可实现定制化的 LLM application
- pipeline 构建
- 更加灵活

支持的数据库

- Elasticsearch
- OpenSearch
- Weaviate
- Pinecone
- Qdrant
- Milvus

### 1.3. 🗂️ LlamaIndex 🦙

{{< icon name="github" pack="fab" >}}[llama_index](https://github.com/run-llama/llama_index)

LlamaIndex 是一个数据框架，供基于 LLM 的应用程序摄取、构建和访问私有或特定领域的数据。它可以在 `Python` 和 `Typescript` 中使用。

## 2. 检索增强生成 （RAG）

什么是 RAG？RAG 的全称是 `Retrieval Augmented Generation`，最初由 [Meta AI](https://ai.meta.com/blog/retrieval-augmented-generation-streamlining-the-creation-of-intelligent-natural-language-processing-models/) 的研究人员提出。

RAG 接受输入并检索一组给定来源的相关/支持文档（例如，维基百科）。文档与原始输入提示连接为上下文，并馈送到生成最终输出的文本生成器。这使得 RAG 能够适应事实可能随时间演变的情况。这非常有用，因为 LLM 的参数知识是静态的。RAG 允许语言模型绕过重新训练，从而能够访问最新信息，通过基于检索的生成生成可靠的输出。

[ACL 2023 Tutorial: Retrieval-based Language Models and Applications](https://acl2023-retrieval-lm.github.io/)

### 2.1. RAG 构建

### 2.2. RAG Evaluation 评测 （准确性）

{{< icon name="github" pack="fab" >}}[ragas](https://github.com/explodinggradients/ragas)

Ragas 是一个框架，可帮助评估检索增强生成 (RAG) pipeline。

```python
from ragas import evaluate
from datasets import Dataset
import os

os.environ["OPENAI_API_KEY"] = "your-openai-key"

# prepare your huggingface dataset in the format
# Dataset({
#     features: ['question', 'contexts', 'answer', 'ground_truths'],
#     num_rows: 25
# })

dataset: Dataset

results = evaluate(dataset)
# {'ragas_score': 0.860, 'context_precision': 0.817,
# 'faithfulness': 0.892, 'answer_relevancy': 0.874}
```

## 3. LLMs 可观测性

### 3.2. 框架选择

#### 3.2.1. 🪢 Langfuse

{{< icon name="github" pack="fab" >}}[langfuse](https://github.com/langfuse/langfuse)：基于 LLM 的应用程序的开源可观测性和分析

- **可观察性**：在可视化 UI 中探索和调试复杂的日志和跟踪
- **分析**：衡量和改善成本、延迟和响应质量

当前支持的 SDK 列表

- {{< icon name="github" pack="fab" >}}[langfuse-python](https://github.com/langfuse/langfuse-python)
- {{< icon name="github" pack="fab" >}}[langfuse-js](https://github.com/langfuse/langfuse-js): `JS/TS`

#### 3.2.2. 🦜️🛠️ LangSmith

- 官网：https://smith.langchain.com/
- 文档：https://docs.smith.langchain.com/

{{<callout note "注意">}}
截止 2023/11/25：LangSmith 当前仍处于早期测试阶段。暂未开放。
{{</callout>}}

## 4. 向量数据库选择

### 4.1. [Milvus](https://milvus.io/docs)

{{< icon name="github" pack="fab" >}}[milvus](https://github.com/milvus-io/milvus)：`Milvus` 是一个**开源**矢量数据库，旨在为嵌入相似性搜索和人工智能应用程序提供支持。 `Milvus` 使非结构化数据搜索更容易访问，并且无论部署环境如何，都可以提供一致的用户体验。

- 支持的索引类型众多，详见[In-memory Index](https://milvus.io/docs/index.md)。
- 支持标量检索、矢量检索、混合检索。

SDK 支持

- Python：支持最好
- Go：部分接口当前还未支持，如。
- Rust

`v2.3.0` 之后支持 ARM 架构、GPU 检索。

### 4.2. Pincone

商业化

## 5. 参考

- [Retrieval Augmented Generation: Streamlining the creation of intelligent natural language processing models](https://ai.meta.com/blog/retrieval-augmented-generation-streamlining-the-creation-of-intelligent-natural-language-processing-models/)
- [What is RAG (Retrieval-Augmented Generation)?](https://colabdoge.medium.com/what-is-rag-retrieval-augmented-generation-b0afc5dd5e79)
- [Secrets to Optimizing RAG LLM Apps for Better Performance, Accuracy and Lower Costs!](https://medium.com/madhukarkumar/secrets-to-optimizing-rag-llm-apps-for-better-accuracy-performance-and-lower-cost-da1014127c0a)
