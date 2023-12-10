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

 ✅ Included | 🟠 Inferior Alternative | 🔨 PR | 🗓️ Planned |❓ Unclear / Unofficial | ❌ Not Implemented



|                          | vLLM       | TensorRT       | llama.cpp    | TGI         | LightLLM    | DS Fastgen  |
|--------------------------|------------|----------------|--------------|-------------|-------------|-------------|
| **Optimizations**        |            |                |              |             |             |             |
| FlashAttention2           | ✅ [^4]    | ✅ [^16]        | ❌              | ✅ [^1]     | ✅           | ✅         |
| PagedAttention           | ✅ [^1]    | ✅ [^16]        | ❌ [^10]     | ✅          | 🟠 ***  [^19]    |  ✅         |
| Speculative Decoding     | 🔨 [^8]    | 🗓️ [^2]        | ✅ [^11]     | 🔨 [^3]     | ❌           |  ❌ [^27]       |
| Tensor Parallel          | ✅         | ✅ [^17]        | 🟠 ** [^12]     | ✅ [^5]     | ✅         | ✅ [^25]         |
| Pipeline Parallel        | ❌ [^34]    | ✅ [^17]        | ✅           | ❓ [^5]     | ❌           | ❌ [^26]            |
| **Optim. / Scheduler**      |            |                |              |             |            |           |
| Dyn. SplitFuse (SOTA[^22])     | 🗓️ [^22]   | 🗓️ [^29]       | ❌          | ❌          | ❌           | ✅ [^22]       |
| Efficient Rtr (better)    | ❌       | ❌               | ❌           | ❌          | ✅ [^24]    | ❌          |
| Cont. Batching           | ✅ [^22]   | ✅ [^23]        | ✅           | ✅          | ❌           | ✅ [^25]       |
| **Features**             |            |                |              |             |             |             |
| OpenAI-Style API         | ✅         | ❌              | ✅ [^13]     | ❓           | ✅ [^20]     |  ❌            |
| **Feat. / Sampling**     |            |                |              |            |               |                   |
| Beam Search              | ✅         | ✅ [^16]        | ✅ [^14]     | ❌ [^7]     | ❌           | ❌ [^28]            |
| LMQL Support             | 🗓️ [^32]   | ❌              | ✅           | ❌ [^33]    | ❌           | ❌              |
| Grammars                 | ❌ [^9]    | ❌              | ✅ [^13]     | ❌ [^6]     | ❌           | ❌         
| **Feat. / Quantize**     |            |                |              |             |             |             |
| EXL2 (SOTA[^35])         | 🔨 [^34]   | ❌              | ❌           | ✅          | ❌           | ❌             |
| AWQ                      | ✅         | ✅              | ❌           | ✅          | ❌           | ❌             |
| Other Quants             | (yes) [^30]  | GPTQ         | GGUF [^31]  | (many) [^18] | ?           |  ?          |
| **Models**               |            |                |              |             |             |             |
| LlamaForCausalLM         | ✅         | ✅              | ✅           | ✅          | ✅           |  ✅          |
| MistralForCausalLM       | ✅         | ✅              | ✅           | ✅          | 🗓️ [^21]    |   ✅         |
| **Implementation**       |            |                |              |             |             |             |
| Core Language            | Python     | C++            | C++          | Python/Rust | Python      | Python        |
| GPU Language             | CUDA *     | CUDA *         | CUDA         | CUDA *      | Triton/CUDA | CUDA *        |
| **Repo**                 |            |                |              |             |             |             |
| License                  | Apache 2.0 | Apache 2.0     | MIT          | HFOILv1.0 [^15] | Apache 2.0 | Apache 2.0            |
| Github Stars             | 11K        | 4K             | 46K          | 6K          | 1K          |  1K            |


*Supports Triton for one-off such as FlashAttention (FusedAttention) / quantization, or allows Triton plugins, however the project doesn't use Triton otherwise.

**Sequentially processed tensor split

***["TokenAttention is the special case of PagedAttention when block size equals to 1, which we have tested before and find it under-utilizes GPU compute compared to larger block size. Unless LightLLM's Triton kernel implementation is surprisingly fast, this should not bring speedup."](https://github.com/vllm-project/vllm/issues/670#issuecomment-1664683953)

[^1]: https://github.com/huggingface/text-generation-inference/issues/753#issuecomment-1663525606
[^2]: https://github.com/NVIDIA/TensorRT-LLM/issues/169
[^3]: https://github.com/huggingface/text-generation-inference/pull/1308
[^4]: https://github.com/vllm-project/vllm/issues/485#issuecomment-1693009046
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
[^29]: https://github.com/NVIDIA/TensorRT-LLM/issues/317#issuecomment-1810841752
[^30]: https://github.com/vllm-project/vllm/blob/1f24755bf802a2061bd46f3dd1191b7898f13f45/vllm/model_executor/quantization_utils/squeezellm.py#L8
[^31]: https://github.com/ggerganov/llama.cpp/blob/master/gguf-py/README.md
[^32]: https://github.com/eth-sri/lmql/issues/143#issuecomment-1826287242
[^33]: [LMQL waiting on logit_bias](https://github.com/eth-sri/lmql/issues/190#issuecomment-1686540002) however [TGI logit_bias PR author closed it](https://github.com/huggingface/text-generation-inference/pull/810). [TGI developer states its on their roadmap](https://github.com/huggingface/text-generation-inference/issues/505#issuecomment-1708367609)
[^34]: https://github.com/vllm-project/vllm/pull/916#issuecomment-1793351502
[^35]: [https://oobabooga.github.io/blog/posts/gptq-awq-exl2-llamacpp/](https://oobabooga.github.io/blog/posts/gptq-awq-exl2-llamacpp/#pareto-frontiers)https://oobabooga.github.io/blog/posts/gptq-awq-exl2-llamacpp/#pareto-frontiers
[^34]: https://github.com/vllm-project/vllm/issues/387
