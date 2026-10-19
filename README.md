# lipi

Small on-device English speech recognition: a streaming CTC model (about 20M parameters, 4-bit weights, 8-bit activations) built for CPU-only runtimes.

## Status
In development. Weights are not released yet; they will be published on Hugging Face under Apache-2.0.

## Benchmarks (intermediate checkpoint)
Word error rate (%), lower is better. Greedy CTC decoding, no language model, English only.
Weights are simulated at 4 bits (group size 128) and activations at 8 bits.
"Streaming" means 640 ms chunks with a 2-chunk look-back; "full context" sees the whole utterance.

| Benchmark (test set) | Full context | Streaming (640 ms) |
|---|---|---|
| LibriSpeech test-clean | 5.00 | 6.52 |
| LibriSpeech test-other | 12.73 | 16.50 |
| Earnings-22 | 24.86 | 33.40 |
| Common Voice (English) | 32.33 | 39.96 |

Test data: the `hf-audio/open-asr-leaderboard` test configs (`librispeech`, `earnings22`, `common_voice`).
Scoring: our own scorer with the Whisper English text normaliser applied to the references; Common Voice audio (48 kHz) is resampled to 16 kHz.
This is not the leaderboard's own evaluation harness, so numbers may differ slightly from an official run.
This is an intermediate checkpoint, not the final model. Common Voice (accented, noisy read speech) is a known weak spot.
