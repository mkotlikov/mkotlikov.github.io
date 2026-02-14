# Expanded-Context RAG: Enhancing Semantic Search and Contextual Retrieval

*Michael Kotlikov - March 10, 2025*

> **TL;DR:** Embed small text chunks for precise semantic search, but return them with expanded surrounding context—reducing LLM hallucination by giving the model the full picture instead of isolated fragments.

## Introduction

As large language models (LLMs) become more integral to information retrieval and knowledge synthesis, ensuring they receive accurate and complete context is crucial. One of the core challenges in retrieval-augmented generation (RAG) is that conventional approaches often return incomplete chunks of text. This can lead to fragmentation in the retrieved content, causing the LLM to hallucinate missing information or generate responses that lack coherence.

To address this issue, Expanded-Context RAG offers a refined retrieval strategy that improves the utility of retrieved information by embedding smaller text chunks while returning a broader surrounding context. This approach enhances both the accuracy and reliability of the model's outputs.

## The Challenge: Incomplete Context in Retrieval

Traditional RAG implementations use semantic search to retrieve relevant text based on embeddings. However, embedding high-quality representations requires concise chunks of text—typically around 250 tokens—to preserve semantic meaning. The problem arises when these isolated chunks lack crucial context.

For instance, if a retrieved chunk contains steps 2 through 4 of a process but omits step 1 and any steps beyond 4, the LLM is likely to generate its own assumptions. This results in unreliable outputs, as the model attempts to fill in the missing gaps, often with fabricated or inaccurate details.

## The Expanded-Context RAG Approach

The Expanded-Context RAG method resolves this issue by embedding smaller, high-precision text chunks but returning them alongside additional surrounding content. Here's how it works:

- The system generates embeddings from smaller chunks (e.g., 250 tokens) for better semantic precision in search results.
- When retrieving a chunk, the system expands the returned context by including 500 tokens before and after the embedded chunk.
- The final context window totals 1,250 tokens, providing the LLM with a more complete view of the relevant information.

By expanding the retrieval scope in this way, the LLM receives a richer, more coherent dataset to process, leading to better-informed and more accurate responses.

## Benefits of Expanded-Context RAG

This retrieval strategy offers several key advantages:

1. **Improved Coherence** – The inclusion of adjacent content allows the LLM to generate responses that are more contextually complete and logically structured.

2. **Reduced Hallucination** – By providing a more comprehensive chunk of information, the LLM is less likely to generate missing details on its own, reducing misinformation.

3. **Configurable Context Windows** – The buffer size (e.g., 500 tokens before and after) can be adjusted based on token constraints and the specific needs of an application.

## Optimizing Expanded Context for Performance

While Expanded-Context RAG significantly improves retrieval quality, implementing it effectively requires careful consideration of token limits and computational efficiency. Here are some best practices:

- Choose the Right Chunk Size – Keeping embedded chunks small (e.g., 250 tokens) ensures high-quality semantic search.
- Adjust Buffer Size for Different Use Cases – The 500-token buffer is a guideline, but real-world applications may benefit from larger or smaller expansions based on available token limits.
- Manage Token Constraints – Expanded context retrieval must stay within the LLM's input limits to avoid truncation, especially when handling multiple retrieved chunks.

## Conclusion

Expanded-Context RAG is a simple yet powerful enhancement to traditional RAG methods. By embedding smaller, semantically precise chunks while returning expanded context windows, this approach improves response accuracy, reduces hallucinations, and ensures more reliable retrieval.

Organizations leveraging LLMs for information retrieval should experiment with different buffer sizes to find an optimal balance between semantic accuracy and contextual completeness. By refining how context is retrieved and presented to LLMs, Expanded-Context RAG offers a scalable, adaptable solution for improving LLM-powered applications.