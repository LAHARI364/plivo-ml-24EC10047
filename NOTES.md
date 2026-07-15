# NOTES

## Objective

The objective was to minimize Bits Per Byte (BPB) while satisfying:

- Maximum 2,000 optimizer steps
- Maximum 2 million parameters
- Training only on the supplied corpus

---

## Experiments

### Optimizer

AdamW with cosine decay, warmup and gradient clipping was evaluated.

Although these techniques are common in transformer training, the limited training budget of 2,000 steps prevented the model from benefiting from them.

---

### Weight Tying

Weight tying reduced the total number of parameters but slightly increased BPB.

---

### Initialization

Xavier initialization was tested instead of the baseline normal initialization.

Training remained stable but final validation performance did not improve.

---

### Tokenizer

A Byte Pair Encoding tokenizer was investigated to reduce sequence length.

However, increasing the vocabulary substantially increased embedding and output-layer parameters beyond the assignment limit of 2 million parameters.

Because of the time constraint and submission requirements, the baseline tokenizer was retained.

---

## Future Improvements

Given additional time I would investigate:

- Compact BPE tokenizer within parameter budget
- Rotary positional embeddings
- Improved learning-rate search
- Better parameter allocation between embedding size and transformer depth