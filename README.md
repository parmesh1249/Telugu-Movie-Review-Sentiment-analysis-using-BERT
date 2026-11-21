# Telugu Movie Reviews Sentiment Analysis

Fine-tuned `xlm-roberta-base` to classify Telugu movie review sentences as positive or negative, plus a simple rating generator that turns the model's output probabilities into a movie rating.

## Results

| Metric | Value |
|---|---|
| Accuracy | 0.8814 |
| F1 | 0.8889 |
| Loss | 0.3627 |

Measured on the held-out evaluation set. 24,300 sentences in the train and 7034 sentences in the evaluation sets. 

## Dataset

The data comes from the **Sentiraama** corpus, created by G. Rama Rohit Reddy at the Language Technologies Research Centre, KCIS, IIIT Hyderabad. The movie reviews folder has 267 Telugu reviews (136 positive, 131 negative), about 20,000 sentences and 165,049 words.

The reviews are long, so we split them into short sentences and labelled each one by hand as `positive` or `negative`.

## Method

1. Pre-process the text and split long reviews into short sentences.
2. Load the pre-trained `xlm-roberta-base` model and tokenizer from Hugging Face.
3. Fine-tune with the Hugging Face `Trainer` (about 1 to 1.5 hours per run, depending on the data size).
4. Push the model and tokenizer to the Hugging Face Hub and test with example Telugu sentences.
5. **Rating generator:** convert the positive and negative probabilities for a review into a rating.

### Training hyperparameters

| Setting | Value |
|---|---|
| Learning rate | 2e-5 |
| Train and eval batch size | 16 |
| Epochs | 4 |
| Optimizer | Adam (betas 0.9, 0.999; epsilon 1e-8) |
| LR scheduler | Linear |
| Seed | 42 |

### Environment

Transformers 4.28.1, PyTorch 2.0.0+cu118, Datasets 2.11.0, Tokenizers 0.13.3

## Limitations

- Supports Telugu only.
- Trained on movie reviews, so it may do poorly on other domains or on reviews with obscure references.
- The dataset is small and labelled by hand, so it may carry labelling bias.
- Only two classes (positive and negative), so neutral or mixed reviews are not handled.

## Status

Completed as a college project (2023). Possible next steps: a larger and more balanced dataset, a neutral class, and document-level sentiment.
