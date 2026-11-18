# Vocal Remover – on-device lyrics models

Speech-recognition models that the **Vocal Remover: Karaoke Maker** Android app downloads on demand to create lyrics on the device with [whisper.cpp](https://github.com/ggml-org/whisper.cpp). Files are attached to the [`lyrics-v1` release](../../releases/tag/lyrics-v1).

| File | Model | Language | License | Size | SHA-256 |
|---|---|---|---|---|---|
| `ggml-small-q5_1.bin` | [OpenAI Whisper small](https://github.com/openai/whisper), whisper.cpp q5_1 conversion from [ggerganov/whisper.cpp](https://huggingface.co/ggerganov/whisper.cpp) (unchanged) | multilingual | MIT, Copyright (c) 2022 OpenAI | 190,085,487 bytes | `ae85e4a935d7a567bd102fe55afc16bb595bdb618e11b2fc7591bc08120411bb` |
| `ggml-phowhisper-small-q5_1.bin` | [VinAI PhoWhisper small](https://huggingface.co/vinai/PhoWhisper-small), converted to whisper.cpp format and quantized to q5_1 | Vietnamese | BSD 3-Clause, Copyright (c) 2024, VinAI | 190,085,504 bytes | `c93fb04f6f586de4eb9b82501f371d4b0bdd033e266264a5ab4f787dea25343e` |

The full license texts are in [`licenses/`](licenses). The model weights are the work of their authors; this repository only redistributes them in whisper.cpp format.

## How `ggml-phowhisper-small-q5_1.bin` was made

Using whisper.cpp at commit `8302b819fc3096c03cedbc91ef1fe982cc6ebb77`:

```sh
# vinai/PhoWhisper-small (Hugging Face, transformers format) -> ggml f32
python models/convert-h5-to-ggml.py PhoWhisper-small /path/to/openai/whisper out
# f32 -> q5_1
./build/bin/whisper-quantize out/ggml-model.bin ggml-phowhisper-small-q5_1.bin q5_1
```

PhoWhisper was trained without timestamp tokens, so it must be run with `no_timestamps = true`.
