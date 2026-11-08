# lipi

Small, fast, on-device English speech recognition. Streaming-capable, 4-bit weights, 13.6 MB, built for CPU-only runtimes.

Weights: https://huggingface.co/hitl-systems/lipi

For English plus Hinglish (Hindi and English mixed), see https://huggingface.co/hitl-systems/lipi-hn

## Results
Word error rate (%), lower is better. Greedy decoding, no language model, full context, English only.
Measured from the exported 4-bit weights with 8-bit activations. Test data: the `hf-audio/open-asr-leaderboard` test configurations, using the cleaned versions where the leaderboard provides them.

| Benchmark (test set) | WER |
|---|---|
| LibriSpeech test-clean | 4.55 |
| LibriSpeech test-other | 11.75 |
| Earnings-22 (cleaned, call level) | 17.50 |
| GigaSpeech (cleaned) | 14.80 |
| SPGISpeech | 3.82 |
| AMI (cleaned) | 14.78 |
| VoxPopuli (cleaned) | 6.39 |
| **Mean of the seven** | **10.51** |

Also: Earnings-22 raw test 20.49, Common Voice (English) 29.38.
Streaming (640 ms chunks) costs accuracy: on LibriSpeech dev-clean 4.46 full context versus 5.86 streaming.

Scoring: our own scorer with the Whisper English text normaliser applied to the references; Common Voice audio is resampled from 48 kHz to 16 kHz.
This is not the leaderboard's own harness, so an official run may differ slightly.
Known weak spots: accented and noisy speech (Common Voice) and phone-quality business calls (Earnings-22).

## Files
- `lipi-w4.lipi` the 4-bit model (13.6 MB)
- `tokenizer.model` SentencePiece tokenizer (1024 pieces)

## License
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 (CC BY-NC-SA 4.0) for the model weights and these documents: attribution required, non-commercial use only, and adaptations must be shared under the same licence. Full text in `LICENSE`.
