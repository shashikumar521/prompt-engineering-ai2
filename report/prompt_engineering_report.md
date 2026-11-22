# AI-2 Milestone: Prompt Engineering Report

## 1. Introduction

This project explores three important prompt engineering techniques using Google AI Studio and Gemini.

The objective was to understand how different prompting techniques affect model responses, reasoning explanations, and structured data extraction.

The three experiments conducted were:

1. Zero-Shot vs Few-Shot Prompting
2. Direct Prompting vs Step-by-Step Prompting
3. Structured Output Using JSON

## 2. Tools and Environment

- Platform: Google AI Studio
- Model: Gemini (displayed as Model 1 in the Playground)
- Testing method: Manual prompt execution
- Programming/API integration: Not used for these experiments

---

## 3. Experiment 1: Zero-Shot vs Few-Shot Prompting

### Objective

To compare zero-shot and few-shot prompting using a customer review sentiment classification task.

### Task

Classify a customer review as Positive, Negative, or Neutral.

### Zero-Shot Prompt

You are a sentiment classification AI.

Classify the following customer review into one of these categories:
- Positive
- Negative
- Neutral

Return only the sentiment label. Do not explain your answer.

Review: "The product looks nice, but it stopped working after two days and customer support never replied."

### Actual Zero-Shot Output

Negative

### Few-Shot Prompt

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

### Actual Few-Shot Output

Negative

### Analysis

Both prompting techniques produced the correct sentiment classification.

Zero-shot prompting worked without examples. Few-shot prompting used four examples to guide the model's classification and output format.

For this review, few-shot prompting did not change the final answer. However, examples can help guide model responses, especially when tasks or expected output formats are more ambiguous.

### Conclusion

Both zero-shot and few-shot prompting were effective for this sentiment classification task. Zero-shot prompting was simpler, while few-shot prompting provided additional guidance through examples.

---

## 4. Experiment 2: Direct Prompting vs Step-by-Step Prompting

### Objective

To compare direct prompting and step-by-step prompting using a multi-step mathematical problem.

### Problem

A college has 240 students. 35% of students participate in a coding competition. Of those participants, 25% qualify for the final round. How many students qualify for the final round?

### Direct Prompt

A college has 240 students. 35% of students participate in a coding competition. Of those participants, 25% qualify for the final round. How many students qualify for the final round?

Give only the final answer.

### Actual Direct Prompt Output

21

### Step-by-Step Prompt

Solve the following problem carefully.

A college has 240 students. 35% of students participate in a coding competition. Of those participants, 25% qualify for the final round.

Break the calculation into clear steps. Calculate the number of participants first, then calculate the number who qualify. Give the final answer at the end.

### Actual Step-by-Step Output

Here is the step-by-step calculation:

Step 1: Calculate the number of participants

- Total number of students = 240
- Percentage of students participating = 35% (or 0.35)

Number of participants = 240 × 0.35 = 84

There are 84 students participating in the coding competition.

Step 2: Calculate the number of students who qualify for the final round

- Number of participants = 84
- Percentage of participants who qualify = 25% (or 0.25)

Number who qualify = 84 × 0.25 = 21

Final Answer: 21 students qualify for the final round.

### Analysis

Both prompting techniques produced the correct final answer.

Direct prompting returned only the answer, while step-by-step prompting explained the two calculations.

The step-by-step approach improved the transparency and understandability of the response. However, it did not change the accuracy because both approaches produced the correct answer.

### Conclusion

Direct prompting is useful when only the final answer is needed. Step-by-step prompting is useful when the calculation process and explanation are important.

---

## 5. Experiment 3: Structured Output Using JSON

### Objective

To test whether an AI model can extract payment information from different types of messages and return the information in a consistent JSON format.

### Required JSON Structure

The model was instructed to return exactly four fields:

- `name`: string or null
- `date`: string in YYYY-MM-DD format or null
- `amount`: number or null
- `currency`: string or null

### Prompt Used

You are a data extraction assistant. Extract payment information from the input message.

Return ONLY one valid JSON object. Do not include Markdown, code fences, comments, or explanations.

Use exactly these four keys:
- "name": string or null
- "date": string in YYYY-MM-DD format or null
- "amount": number or null
- "currency": string or null

Rules:
1. Do not invent missing information.
2. Convert dates to YYYY-MM-DD whenever the date is clear.
3. The amount must be a numeric value without currency symbols or commas.
4. Use INR for Indian Rupees, USD for US Dollars, and EUR for Euros.
5. If information is missing, use null.
6. Do not add extra keys.

Example input:
"Ananya paid $45 on 2 March 2026 for her subscription."

Example output:
{
  "name": "Ananya",
  "date": "2026-03-02",
  "amount": 45,
  "currency": "USD"
}

Now extract the information from this input:

"Rahul paid ₹1,250 to the college on 15 November 2026 for registration."

### Test 1: Rahul – Complete Payment Information

**Input:**

Rahul paid ₹1,250 to the college on 15 November 2026 for registration.

**Actual Output:**

{
  "name": "Rahul",
  "date": "2026-11-15",
  "amount": 1250,
  "currency": "INR"
}

**Result:** Correct.

### Test 2: Daniel – US Dollar Payment

**Input:**

Daniel received a payment of $120 on 5 September 2026 for freelance work.

**Actual Output:**

{
  "name": "Daniel",
  "date": "2026-09-05",
  "amount": 120,
  "currency": "USD"
}

**Result:** Correct.

### Test 3: Meera – Missing Date

**Input:**

Meera paid 2,400 rupees for her examination fee.

**Actual Output:**

{
  "name": "Meera",
  "date": null,
  "amount": 2400,
  "currency": "INR"
}

**Result:** Correct. The model represented the missing date using null.

### Test 4: Missing Name

**Input:**

A payment of EUR 75 was made on 21 November 2026 for a software subscription.

**Actual Output:**

{
  "name": null,
  "date": "2026-11-21",
  "amount": 75,
  "currency": "EUR"
}

**Result:** Correct. The model represented the missing name using null.

### Test 5: Arjun – Informal Message and Numeric Date

**Input:**

hey, this is Arjun — transferred Rs. 3,500 to the workshop yesterday, 17/11/26, for project materials.

**Actual Output:**

{
  "name": "Arjun",
  "date": "2026-11-17",
  "amount": 3500,
  "currency": "INR"
}

**Result:** Correct. The model handled informal wording, the Rs. abbreviation, and the numeric date format.

### Results and Success Rate

| Evaluation | Result |
|---|---|
| Total test inputs | 5 |
| Successful outputs | 5 |
| Incorrect outputs | 0 |
| Success rate | 100% |
| Required JSON keys present | Yes |
| Missing values represented using null | Yes |
| Amounts returned as numbers | Yes |

**Success Rate = (5 / 5) × 100 = 100%**

### Techniques That Improved Reliability

1. Explicitly defining the required JSON keys.
2. Specifying the expected data types for every field.
3. Instructing the model to return only JSON.
4. Providing an exact example of the expected input and output.
5. Specifying that missing information must be represented using null.
6. Defining date and currency normalization rules.

The experiment used prompt instructions and an example in Google AI Studio. API-based JSON mode or schema enforcement was not used.

### Conclusion

The model successfully completed all five test cases and returned the expected information in the required JSON structure.

Structured prompting helped maintain consistency, handle missing information, and normalize dates and currencies.

---

## 6. Overall Comparison of Experiments

| Experiment | Technique | Main Observation |
|---|---|---|
| Experiment 1 | Zero-Shot vs Few-Shot | Both produced the correct sentiment |
| Experiment 2 | Direct vs Step-by-Step | Both produced the correct answer; step-by-step showed calculations |
| Experiment 3 | Structured JSON Output | All five test cases passed |

## 7. Overall Learning Outcomes

Through these experiments, I learned:

1. Zero-shot prompting can perform simple classification tasks without examples.
2. Few-shot prompting provides examples that guide the model's responses.
3. Step-by-step instructions can make multi-step solutions easier to understand and verify.
4. Structured output instructions help produce consistent JSON responses.
5. Explicit field definitions, examples, and missing-value rules improve output consistency.
6. Testing prompts with multiple inputs is important for evaluating reliability.

## 8. Final Conclusion

This milestone demonstrated how prompt engineering techniques can influence AI model responses.

The experiments showed that different prompting approaches are useful for different tasks. Zero-shot and few-shot prompting were effective for sentiment classification. Direct and step-by-step prompting both solved the mathematical problem, while step-by-step prompting provided more explanation. Structured JSON prompting successfully extracted payment information across five test cases with a 100% success rate.

Overall, the experiments helped develop a practical understanding of prompt design, model response evaluation, and structured output generation.
