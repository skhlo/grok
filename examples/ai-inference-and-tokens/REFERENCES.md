# AI inference and tokens References

## Sources

- [Google Cloud: What is AI inference?](https://cloud.google.com/discover/what-is-ai-inference)
  Used for: Clear training vs fine-tuning vs inference vs serving distinction, including inference as the execution phase that uses a trained model on new data.
  Trust: Official cloud provider documentation written for builders and business readers.

- [IBM: What is AI inference?](https://www.ibm.com/think/topics/ai-inference)
  Used for: Plain explanation that inference uses a trained model to make predictions or decisions on new data, plus examples such as spam detection and language models.
  Trust: Recognized enterprise AI source with a detailed educational article.

- [OpenAI: Counting tokens](https://developers.openai.com/api/docs/guides/token-counting)
  Used for: Why token counting matters: context limits, cost estimation, routing by size, and request structure that affects token counts.
  Trust: Official OpenAI API documentation for current token-counting behavior.

## Gaps

- Need a non-technical source or example specifically explaining tokens as chunks of text without API implementation detail.
- Need a follow-up explanation of context windows and compression if the user wants the next layer.
