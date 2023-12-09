# Open Inference Engines

Feel free to create a PR or issue if you want a new engine column, feature row, or update a status. 

### Compared Inference Engines

- TGI: https://github.com/huggingface/text-generation-inference/
- vLLM: https://github.com/vllm-project/vllm/
- llama.cpp: https://github.com/ggerganov/llama.cpp/
- TensorRT-LLM: https://github.com/NVIDIA/TensorRT-LLM

### Comparison Table

✅ Included | ☑️ Similar Feature | 🔨 In progress / PR |🗓️ Planned / on Roadmap |❓ Unclear / Not official |❌ Not supported



|                          | vLLM                  | TensorRT-LLM              | llama.cpp                                   | TGI               | LightLLM           |
|--------------------------|-----------------------|---------------------------|---------------------------------------------|-------------------|--------------------|
| **Performance**          |                       |                           |                                             |                   |                    |
| FlashAttention           | ☑️ (xFormers) [^4]    | ✅ [^16]                   | ❓                                           | ✅ [^1]            | ✅                  |
| PagedAttention           | ✅ [^1]               | ✅ [^16]                   | ❌ [^10]                                    | ✅                 | ☑️ (TokenAttention) [^19] |
| Speculative Decoding     | 🔨 [^8]               | 🗓️ [^2]                   | ✅ [^11]                                    | 🔨 [^3]            | ❌                  |
| Tensor Parallel          | ✅                    | ✅ [^17]                   | ☑️ ** [^12]          | ✅ [^5]            | ✅                  |
| Pipeline Parallel        | ✅                    | ✅ [^17]                   | ✅                                          | ❓ [^5]            | ❌                  |
| **Functionality**        |                       |                           |                                             |                   |                    |
| OpenAI Compatible API    | ✅                    |                           | ✅ [^13]                                    | ❓                 | ✅ [^20]            |
| Grammars                 | ❌ [^9]               | ❌                         | ✅ [^13]                                    | ❌ [^6]            | ❌                  |
| Beam Search              | ✅                    | ✅ [^16]                   | ✅ [^14]                                    | ❌ [^7]            | ❌                  |
| **Quantization**         |                       |                           |                                             |                   |                    |
| AWQ                      | ✅                    | ✅                         | ❌                                          | ✅                 | ❌                  |
| Other Quants             | SqueezeLLM            | ❌                         | GGUF                                        | GPTQ, BnB, EEQT [^18]| ❓              |
| **Models**               |                       |                           |                                             |                   |                    |
| LlamaForCausalLM         | ✅                    | ✅                         | ✅                                          | ✅                 | ✅                  |
| MistralForCausalLM       | ✅                    | ✅                         | ✅                                          | ✅                 | 🗓️ [^21]          |
| **Implementation**       |                       |                           |                                             |                   |                    |
| Core Language            | Python                | C++                       | C++                                        | Python / Rust     | Python             |
| GPU Kernel Language      | CUDA *                 | CUDA *                    | CUDA                                       | CUDA *            | **Triton** / CUDA  |
| **Repo**                 |                       |                           |                                             |                   |                    |
| License                  | Apache 2.0            | Apache 2.0                | MIT                                        | HFOILv1.0 [^15]   | Apache 2.0         |
| Github Stars             | 11K                   | 4K                        | 46K                                         | 6K                | 1K                 |

*Supports Triton for one-off such as FlashAttention (FusedAttention) / or AWQ, or allows Triton plugins but doesn't use Triton otherwise.
**Sequentially processed tensor split

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
[^16]: https://github.com/NVIDIA/TensorRT-LLM/blob/main/docs/source/gpt_attention.md
[^17]: https://github.com/NVIDIA/TensorRT-LLM/blob/main/cpp/tensorrt_llm/pybind/bindings.cpp#L184
[^18]: https://github.com/huggingface/text-generation-inference/blob/main/server/text_generation_server/cli.py#L15-L21
[^19]: https://github.com/ModelTC/lightllm/blob/main/docs/TokenAttention.md
[^20]: https://github.com/ModelTC/lightllm/blob/main/lightllm/server/api_models.py#L9
[^21]: https://github.com/ModelTC/lightllm/issues/224#issuecomment-1827365514

## Notes

FlexGen is going through a refactor, so it's mostly been left blank.
