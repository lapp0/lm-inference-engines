# Open Inference Engines

[View table](https://github.com/lapp0/lm-inference-engines/blob/main/README.md)

Feel free to create a PR or issue if you want a new engine column, feature row, or update a status. 

### Compared Inference Engines

- [vLLM](https://github.com/vllm-project/vllm/)
- [TensorRT-LLM](https://github.com/NVIDIA/TensorRT-LLM)
- [llama.cpp](https://github.com/ggerganov/llama.cpp/)
- [TGI](https://github.com/huggingface/text-generation-inference/) (**Source Available, but not open**)
- [LightLLM](https://github.com/ModelTC/lightllm)
- [DeepSpeed-MII / DeepSpeed-FastGen](https://github.com/microsoft/DeepSpeed-MII)


### Comparison Table

☑️ Superior Alternative | ✅ Included | 🟠 Inferior Alternative | 🔨 PR | 🗓️ Planned |❓ Unclear / Unofficial | ❌ Not Impl.



|                          | vLLM       | TensorRT       | llama.cpp    | TGI         | LightLLM    | DS Fastgen  |
|--------------------------|------------|----------------|--------------|-------------|-------------|-------------|
| **Optimizations**        |            |                |              |             |             |             |
| FlashAttention           | 🟠 [^4]    | ✅ [^16]        | ❓           | ✅ [^1]     | ✅           | ✅         |
| PagedAttention           | ✅ [^1]    | ✅ [^16]        | ❌ [^10]     | ✅          | ☑️ [^19]    |  ✅         |
| Speculative Decoding     | 🔨 [^8]    | 🗓️ [^2]        | ✅ [^11]     | 🔨 [^3]     | ❌           |  ❌ [^27]       |
| Tensor Parallel          | ✅         | ✅ [^17]        | 🟠 [^12]     | ✅ [^5]     | ✅           | ✅ [^25]         |
| Pipeline Parallel        | ✅         | ✅ [^17]        | ✅           | ❓ [^5]     | ❌           | ❌ [^26]            |
| **Functionality**        |            |                |              |             |             |             |
| OpenAI-Style API         | ✅         | ❌              | ✅ [^13]     | ❓           | ✅ [^20]     |  ❌            |
| Grammars                 | ❌ [^9]    | ❌              | ✅ [^13]     | ❌ [^6]     | ❌           | ❌         |
| Beam Search              | ✅         | ✅ [^16]        | ✅ [^14]     | ❌ [^7]     | ❌           | ❌ [^28]            |
| **Scheduling**           |            |                |              |             |             |           |
| Cont. Batching           | ✅ [^22]   | ✅ [^23]        | ✅           | ✅          | ❌           | ✅ [^25]       |
| Other Scheduler          | ❌         | ❌             | ❓           | ❓          | EfficientRouter [^24] | Dynamic SplitFuse [^25]        |

| **Quantization**         |            |                |              |             |             |             |
| AWQ                      | ✅         | ✅              | ❌           | ✅          | ❌           | ❌             |
| Other Quants             | SqueezeLLM | ❌              | GGUF         | GPTQ, BnB, EEQT [^18] | ❓ |             |
| **Models**               |            |                |              |             |             |             |
| LlamaForCausalLM         | ✅         | ✅              | ✅           | ✅          | ✅           |  ✅          |
| MistralForCausalLM       | ✅         | ✅              | ✅           | ✅          | 🗓️ [^21]    |   ✅         |
| **Implementation**       |            |                |              |             |             |             |
| Core Language            | Python     | C++            | C++          | Python/Rust | Python      | Python        |
| GPU Language             | CUDA *     | CUDA *         | CUDA         | CUDA *      | Triton/CUDA | CUDA *        |
| **Repo**                 |            |                |              |             |             |             |
| License                  | Apache 2.0 | Apache 2.0     | MIT          | HFOILv1.0 [^15] | Apache 2.0 | Apache 2.0            |
| Github Stars             | 11K        | 4K             | 46K          | 6K          | 1K          |  1K            |


*Supports Triton for one-off such as FlashAttention (FusedAttention) / quantization, or allows Triton plugins, however it the project doesn't use Triton otherwise.

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
[^22]: https://blog.vllm.ai/2023/11/14/notes-vllm-vs-deepspeed.html
[^23]: https://github.com/NVIDIA/TensorRT-LLM/blob/main/README.md
[^24]: https://github.com/ModelTC/lightllm/blob/a9cf0152ad84beb663cddaf93a784092a47d1515/docs/LightLLM.md#efficient-router
[^25]: https://github.com/microsoft/DeepSpeed-MII
[^26]: https://github.com/microsoft/DeepSpeed-MII/issues/329#issuecomment-1830317364
[^27]: https://github.com/microsoft/DeepSpeed-MII/issues/254
[^28]: https://github.com/microsoft/DeepSpeed-MII/issues/286#issuecomment-1808510043
