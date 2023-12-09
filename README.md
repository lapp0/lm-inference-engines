Compared Inference Engines

- TGI: https://github.com/huggingface/text-generation-inference/
- vLLM: https://github.com/vllm-project/vllm/tree/main
- FlexGen: https://github.com/FMInference/FlexGen
- llama.cpp:

### Comparison Table

|                          | TGI                   | vLLM                       | llama.cpp                                    | TensorRT-LLM       | FlexGen            |
|--------------------------|-----------------------|----------------------------|----------------------------------------------|--------------------|--------------------|
| **Performance**          |                       |                            |                                              |                    |                    |
| FlashAttention           | ✅ [^1]                | ☑️ (xFormers) [^4]         | ❓                                           |                    |                    |
| PagedAttention           | ✅                     | ✅ [^1]                    | ❌ [^10]                                     | 🗓️ [^2]           |                    |
| Speculative Decoding     | 🔨 [^3]               | 🔨 [^8]                    | ✅ [^11]                                     |                    |                    |
| Tensor Parallel          | ✅ [^5]                | ✅                         | ❌ (sequential tensor split) [^12]           |                    |                    |
| Pipeline Parallel        | ❓ [^5]                | ✅                         | ✅                                           |                    |                    |
| **Features**             |                       |                            |                                              |                    |                    |
| OpenAI Compatible API    | ❓                     | ✅                         | ✅ [^13]                                     |                    |                    |
| Grammars                 | ❌ [^6]                | ❌ [^9]                    | ✅ [^13]                                     |                    |                    |
| Beam Search              | ❌ [^7]                | ✅                         | ✅ [^14]                                     |                    |                    |
| **Model Support**        |                       |                            |                                              |                    |                    |
| LlamaForCausalLM         | ✅                     | ✅                         | ✅                                           | ✅                | ❌                 |
| MistralForCausalLM       | ✅                     | ✅                         | ✅                                           | ✅                | ❌                 |
| **Repo**                 |                       |                            |                                              |                    |                    |
| License                  | HFOILv1.0 [^15]       | Apache 2.0                 |                                              |                    |                    |
| Github Stars             | 6K                     | 11K                        | 46K                                          |                    |                    |
Key:
- ✅ Included
- ☑️ Equivalent Feature
- 🔨 In progress / PR
- 🗓️ Planned / on Roadmap
- ❓ Unclear / Not officially supported
- ❌ Not supported

[^1]: https://github.com/huggingface/text-generation-inference/issues/753#issuecomment-1663525606
[^2]: https://github.com/NVIDIA/TensorRT-LLM/issues/169
[^3]: https://github.com/huggingface/text-generation-inference/pull/1308
[^4]: https://github.com/vllm-project/vllm/pull/70
[^5]: https://github.com/huggingface/text-generation-inference/issues/1031#issuecomment-1727976990
[^6]: https://github.com/huggingface/text-generation-inference/issues/1050
[^7]: https://github.com/huggingface/text-generation-inference/issues/722#issuecomment-1658823644
[^8]: https://github.com/vllm-project/vllm/pull/1797
[^9]: https://github.com/vllm-project/vllm/issues/1229
[^10]: https://github.com/ggerganov/llama.cpp/issues/1955
[^11]: https://github.com/ggerganov/llama.cpp/blob/fe680e3d1080a765e5d3150ffd7bab189742898d/examples/speculative/README.md
[^12]: https://github.com/ggerganov/llama.cpp/issues/4014#issuecomment-1804925896
[^13]: https://github.com/ggerganov/llama.cpp/tree/master/examples/server
[^14]: https://github.com/ggerganov/llama.cpp/tree/master/examples/beam-search
[^15]: https://raw.githubusercontent.com/huggingface/text-generation-inference/main/LICENSE

## Notes

FlexGen is going through a refactor, so it's mostly been left blank.
