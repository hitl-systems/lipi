# lipi

Small, fast, on-device English speech recognition. Streaming-capable, 4-bit weights, 13.6 MB, built for CPU-only runtimes.

Weights: https://huggingface.co/hitl-systems/lipi

## Results
Word error rate (%), lower is better. Greedy decoding, no language model, English only. 4-bit weights with 8-bit activations.
"Streaming" uses 640 ms chunks; "full context" sees the whole utterance.

| Benchmark (test set) | Full context | Streaming (640 ms) |
|---|---|---|
| LibriSpeech test-clean | 5.03 | 6.49 |
| LibriSpeech test-other | 12.78 | 16.47 |
| Earnings-22 | 24.74 | 33.39 |
| Common Voice (English) | 32.32 | 40.02 |

Test data: the `hf-audio/open-asr-leaderboard` test configurations (`librispeech`, `earnings22`, `common_voice`).
Scored with our own scorer and the Whisper English text normaliser on the references; Common Voice audio is resampled from 48 kHz to 16 kHz.
This is not the leaderboard's own harness, so an official run may differ slightly. Numbers were measured from the exported 4-bit weights.
Known weak spots: accented and noisy speech (Common Voice), and long-form business speech (Earnings-22).

## Files
- `lipi-w4.lipi` the 4-bit model (13.6 MB)
- `tokenizer.model` SentencePiece tokenizer (1024 pieces)

## License
Apache-2.0 for the model weights and these documents.

## Training data
Trained on public English speech corpora, including LibriSpeech, GigaSpeech, SPGISpeech, VoxPopuli, AMI and TED-LIUM.
Some of these corpora are distributed under research-only or non-commercial terms. Check the upstream licences before commercial use.
