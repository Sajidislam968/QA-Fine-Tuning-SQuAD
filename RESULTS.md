# Experimental Results

Populate this report from the outputs of the executed notebook. Do not guess or invent missing results.

## 1. Validation Metrics

| Metric | Result |
|---|---:|
| Exact Match (EM) | `80.17` |
| Token-level F1 | `87.75` |
| Validation loss | `1.0089569091796875` |
| Training time (minutes) | `109.70 minutes` |

## 2. Custom Q&A Tests

| Test | Question | Expected answer | Predicted answer | Exact string match |
|---|---|---|---|---|
| 1 | Who developed the theory of relativity? | Albert Einstein | `Albert Einstein` | `True` |
| 2 | Which two elements did Marie Curie discover with Pierre Curie? | polonium and radium | `polonium and radium` | `True` |

Note: this table's exact-string comparison is a simple custom check, not the normalized SQuAD EM metric.

## 3. Training Curve

![Training and validation loss](outputs/figures/training_validation_loss.png)

## 4. Prediction Inspection

![Validation prediction examples](outputs/figures/validation_predictions.png)

## 5. Brief Discussion

The fine-tuned BERT model achieved a validation Exact Match (EM) score of 80.17% and an F1 score of 87.75% on the SQuAD v1.1 dataset. EM measures the percentage of predictions that exactly match a reference answer after normalization, whereas F1 measures the overlap between predicted and reference answer tokens. These metrics provide complementary perspectives on the model's answer-extraction performance.

In the two custom tests, the model predicted Albert Einstein for the relativity question and polonium and radium for the Marie Curie question. Comparing these predictions with the expected answers helped assess whether the model could extract relevant information from previously unseen contexts. However, two custom examples are insufficient to establish general performance.

Correct answer-span alignment was essential during preprocessing because the model learns to predict the start and end token positions of each answer. Incorrect alignment can produce misleading training labels and reduce answer-extraction accuracy. The maximum sequence length of 384 tokens and document stride of 128 tokens allowed long contexts to be processed through overlapping windows, although answers may still be missed if tokenization, window coverage, or span selection is inadequate.

One limitation of extractive question answering is that the model selects answers from the provided context rather than generating new explanations. It may therefore struggle when the context does not contain a clear answer, when information is ambiguous, or when the expected answer requires combining information from multiple passages. Overall, this experiment demonstrates how fine-tuning a pre-trained Transformer can adapt it to extractive question answering, while highlighting the importance of evaluation metrics, accurate preprocessing, and context length management.
