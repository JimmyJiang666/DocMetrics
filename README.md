
# Evaluation Pipeline

This repository contains a pipeline for evaluating text generation models using various metrics including ROUGE, BLEU, BERTScore, and PARENT. The pipeline is designed to handle reference and hypothesis files and compute evaluation scores based on the selected metric.

## Requirements

To run this code, you will need the following Python libraries:
- `os`
- `json`
- `typing`
- `rouge`
- `nltk`
- `bert_score`

You can install these libraries using pip:
```sh
pip install rouge-score nltk bert-score
```

The parent folder is also needed. The PARENT function is implemented using the [KaijuML/parent](https://github.com/KaijuML/parent) repository.


## Available Metrics

### ROUGE
ROUGE (Recall-Oriented Understudy for Gisting Evaluation) is a set of metrics for evaluating automatic summarization and machine translation. It measures the overlap between the generated text (hypothesis) and the reference text.

### BLEU
BLEU (Bilingual Evaluation Understudy) is a metric for evaluating the quality of text which has been machine-translated from one language to another. It compares the overlap of n-grams between the hypothesis and the reference.

### BERTScore
BERTScore leverages the pre-trained BERT model to evaluate the similarity between the hypothesis and the reference text at the semantic level. It provides precision, recall, and F1 scores.

### PARENT
PARENT (Precision, Recall, and F1 evaluation with Auxiliary Source Tables) is a metric specifically designed for evaluating data-to-text generation tasks. It takes into account both the reference text and auxiliary tables to evaluate the hypothesis.

## Usage

### General Usage

1. Prepare your reference and hypothesis text files.
2. Choose an evaluation metric.
3. Run the evaluation pipeline with the specified metric.

Example:
```python
if __name__ == "__main__":
    # Specify file paths
    reference_file = 'data/wb_test_output.txt'
    hypothesis_file = 'data/wb_predictions.txt'
    
    # Choose the evaluation metric by input string
    metric_name = 'rouge'  # or 'bleu', 'bertscore', 'parent'
    metric = select_metric(metric_name)
    
    # Run the evaluation pipeline
    pipeline = EvaluationPipeline(reference_file, hypothesis_file, metric)
    scores = pipeline.run()
    print(scores)
```

### Using PARENT Metric

To use the PARENT metric, an additional table file is required. Ensure you have the table file prepared and provide its path when initializing the evaluation pipeline.

Example:
```python
if __name__ == "__main__":
    # Specify file paths
    reference_file = 'data/wb_test_output.txt'
    hypothesis_file = 'data/wb_predictions.txt'
    table_file = 'data/wb_test_tables.jl'
    
    # Choose the evaluation metric by input string
    metric_name = 'parent'
    metric = select_metric(metric_name, table_file=table_file)
    
    # Run the evaluation pipeline
    pipeline = EvaluationPipeline(reference_file, hypothesis_file, metric, table_file=table_file)
    scores = pipeline.run()
    print(scores)
```
