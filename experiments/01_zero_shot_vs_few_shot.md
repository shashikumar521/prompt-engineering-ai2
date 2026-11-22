
# Experiment 1: Zero-Shot vs Few-Shot Prompting

## 1. Objective
To compare zero-shot and few-shot prompting techniques using a customer review sentiment classification task.

## 2. Tool Used
- Platform: Google AI Studio
- Model: Gemini (Model 1, as displayed in the Playground)

## 3. Zero-Shot Prompting

### Prompt Used
You are a sentiment classification AI.

Classify the following customer review into one of these categories:
- Positive
- Negative
- Neutral

Return only the sentiment label. Do not explain your answer.

Review: "The product looks nice, but it stopped working after two days and customer support never replied."

### Actual Model Output
Negative

### Result
Correct. The review expresses dissatisfaction because the product stopped working and customer support did not respond.

## 4. Few-Shot Prompting

### Prompt Used
You are a sentiment classification AI.

Study these examples:

Example 1:
Review: "The delivery was fast and the product quality is excellent."
Sentiment: Positive

Example 2:
Review: "The item arrived broken and the seller refused to help."
Sentiment: Negative

Example 3:
Review: "The package arrived yesterday. I have not tried the product yet."
Sentiment: Neutral

Example 4:
Review: "The product is useful, but the battery drains very quickly."
Sentiment: Negative

Now classify this review into Positive, Negative, or Neutral.

Return only the sentiment label. Do not explain your answer.

Review: "The product looks nice, but it stopped working after two days and customer support never replied."

### Actual Model Output
Negative

### Result
Correct. The model classified the review as Negative after being provided with four examples.

## 5. Comparison and Analysis

| Evaluation | Zero-Shot | Few-Shot |
|---|---|---|
| Number of examples | 0 | 4 |
| Actual output | Negative | Negative |
| Correct classification | Yes | Yes |

Both prompting techniques produced the correct classification.

Zero-shot prompting successfully classified the review without examples. Few-shot prompting also produced the correct result by using four examples as guidance.

For this particular review, few-shot prompting did not improve the final answer. However, examples can help guide the model's expected classification pattern and output format, especially in more ambiguous tasks.

## 6. Conclusion

The experiment demonstrates that both zero-shot and few-shot prompting can be effective for sentiment classification. Zero-shot prompting is simple and requires fewer instructions, whereas few-shot prompting provides examples that guide the model's response.
