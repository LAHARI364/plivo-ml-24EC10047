# RUNLOG

## Environment

- Framework: PyTorch
- Device: CPU
- Optimizer Steps: 2000
- Training Corpus: Provided train_corpus.txt

---

## Run 1 - Baseline

Changes:
- No modifications.

Result:
- Parameters: 1,339,840
- BPB: 2.3718

Status:
- Baseline reference.

---

## Run 2 - AdamW + LR Scheduler

Changes:
- Replaced Adam with AdamW.
- Added cosine learning-rate schedule.
- Added warmup.
- Added gradient clipping.
- Added weight decay.

Result:
- BPB: 2.6083

Observation:
Performance degraded. The learning-rate schedule appeared too aggressive for the fixed 2,000-step budget.

Decision:
Reverted.

---

## Run 3 - Weight Tying

Changes:
- Enabled weight tying.

Result:
- Parameters: 1,298,880
- BPB: 2.4122

Observation:
Reduced parameter count but slightly worsened validation BPB.

Decision:
Reverted.

---

## Run 4 - Xavier Initialization

Changes:
- Replaced default initialization with Xavier initialization.

Result:
- BPB: 2.4073

Observation:
Training remained stable but validation BPB increased slightly.

Decision:
Reverted.

---

## Tokenizer Investigation

Attempted to replace the byte tokenizer with a Byte Pair Encoding tokenizer.

Issue encountered:
- Vocabulary expansion exceeded the 2M parameter limit.
- Alternative tokenizer implementation required additional integration work.

Decision:
Reverted to the provided tokenizer to ensure a valid submission.

---

## Final Submitted Model

Configuration:
- Original byte tokenizer
- Original architecture
- Original optimizer

Final BPB:
2.3718