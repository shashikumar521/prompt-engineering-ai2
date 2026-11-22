# AI-2 Milestone: Prompt Engineering Report

## 1. Introduction

Prompt engineering is the process of designing and improving instructions given to an AI model to obtain accurate, consistent, and useful responses.

The objective of this milestone was to explore and compare different prompt engineering techniques using Google AI Studio and Gemini.

Three experiments were conducted:

1. Zero-Shot vs Few-Shot Prompting
2. Direct Prompting vs Step-by-Step Prompting
3. Structured Output Using JSON

Each experiment included actual prompts, model outputs, and an analysis of the results.

## 2. Tools and Environment

- Platform: Google AI Studio
- AI Model: Gemini (displayed as Model 1 in the Playground)
- Testing method: Manual prompt execution
- Programming language: Not required
- API integration: Not used for these experiments

---

## 3. Experiment 1: Zero-Shot vs Few-Shot Prompting

### 3.1 Objective

To compare zero-shot and few-shot prompting techniques using a customer review sentiment classification task.

The task was to classify a customer review into one of three categories:

- Positive
- Negative
- Neutral

### 3.2 Zero-Shot Prompting

Zero-shot prompting means asking the AI model to perform a task without providing examples.

**Prompt Used:**

```text
You are a sentiment classification AI.

Classify the following customer review into one of these categories:
- Positive
- Negative
- Neutral

Return only the sentiment label. Do not explain your answer.

Review: "The product looks nice, but it stopped working after two days and customer support never replied."
```

**Actual Model Output:**

```text
Negative
```

**Result:**

Correct. The review expresses dissatisfaction because the product stopped working and customer support did not respond.

### 3.3 Few-Shot Prompting

Few-shot prompting means providing examples to guide the AI model before asking it to perform the task.

Four examples were provided.

**Prompt Used:**

```text
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
```

**Actual Model Output:**

```text
Negative
```

**Result:**

Correct. The model classified the review as Negative after receiving four examples.

### 3.4 Comparison and Analysis

| Evaluation | Zero-Shot | Few-Shot |
|---|---|---|
| Number of examples | 0 | 4 |
| Actual output | Negative | Negative |
| Correct classification | Yes | Yes |

Both prompting techniques produced the correct classification.

Zero-shot prompting successfully classified the review without examples. Few-shot prompting also produced the correct result by using four examples as guidance.

For this particular review, few-shot prompting did not improve the final answer. However, examples can help guide the model's expected classification pattern and output format, especially in more ambiguous tasks.

### 3.5 Conclusion

The experiment demonstrates that both zero-shot and few-shot prompting can be effective for sentiment classification.

Zero-shot prompting is simple and requires fewer instructions, whereas few-shot prompting provides examples that guide the model's response.

---

## 4. Experiment 2: Direct Prompting vs Step-by-Step Prompting

### 4.1 Objective

To compare direct prompting and step-by-step prompting using a multi-step mathematical problem.

The objective was to check whether asking the model to explain the calculation steps changes the clarity and accuracy of its response.

### 4.2 Problem Used

A college has 240 students. 35% of students participate in a coding competition. Of those participants, 25% qualify for the final round. How many students qualify for the final round?

### 4.3 Direct Prompting

Direct prompting asks the model to provide the answer without requesting an explanation.

**Prompt Used:**

```text
A college has 240 students. 35% of students participate in a coding competition. Of those participants, 25% qualify for the final round. How many students qualify for the final round?

Give only the final answer.
```

**Actual Model Output:**

```text
21
```

**Result:**

Correct. The model provided the final answer without showing the calculation steps.

### 4.4 Step-by-Step Prompting

Step-by-step prompting asks the model to divide the problem into smaller steps and explain the calculations.

**Prompt Used:**

```text
Solve the following problem carefully.

A college has 240 students. 35% of students participate in a coding competition. Of those participants, 25% qualify for the final round.

Break the calculation into clear steps. Calculate the number of participants first, then calculate the number who qualify. Give the final answer at the end.
```

**Actual Model Output:**

```text
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
```

**Result:**

Correct. The model calculated the number of participants first and then calculated the number who qualified for the final round.

### 4.5 Comparison and Analysis

| Evaluation | Direct Prompting | Step-by-Step Prompting |
|---|---|---|
| Reasoning instructions | No | Yes |
| Shows calculation steps | No | Yes |
| Actual final answer | 21 | 21 |
| Correct answer | Yes | Yes |

Both prompting techniques produced the correct final answer.

Direct prompting was shorter and gave the answer immediately. Step-by-step prompting provided a clear explanation of the two calculations, making the solution easier to follow and verify.

For this problem, step-by-step prompting improved the transparency of the response, but it did not change the final answer or improve its accuracy because both approaches were correct.

### 4.6 Conclusion

The experiment demonstrates that direct prompting and step-by-step prompting can both solve a multi-step mathematical problem correctly.

Direct prompting is useful when only the final answer is needed, while step-by-step prompting is more useful when the calculation process and explanation are important.

---

## 5. Experiment 3: Structured Output Using JSON

### 5.1 Objective

To test whether an AI model can extract payment information from different types of messages and return the information in a consistent JSON format.

The experiment also defines a JSON Schema to describe the expected structure, field names, data types, and validation rules.

### 5.2 Tool Used

- Platform: Google AI Studio
- Model: Gemini (Model 1, as displayed in the Playground)
- Testing method: Manual prompt execution

### 5.3 Required JSON Structure

The model was instructed to return exactly four fields.

| Field | Data Type | Description |
|---|---|---|
| name | String or null | Name of the person |
| date | String or null | Date in YYYY-MM-DD format |
| amount | Number or null | Payment amount |
| currency | String or null | Currency code (INR, USD, EUR) |

### 5.4 JSON Schema

The following JSON Schema formally defines the expected output structure.

```json
{
  "type": "object",
  "additionalProperties": false,
  "required": [
    "name",
    "date",
    "amount",
    "currency"
  ],
  "properties": {
    "name": {
      "type": ["string", "null"]
    },
    "date": {
      "type": ["string", "null"],
      "pattern": "^\\d{4}-\\d{2}-\\d{2}$"
    },
    "amount": {
      "type": ["number", "null"]
    },
    "currency": {
      "type": ["string", "null"],
      "enum": ["INR", "USD", "EUR", null]
    }
  }
}
```

**Schema Explanation:**

1. `type: object` requires the output to be a JSON object.
2. `required` ensures all four fields are present.
3. `additionalProperties: false` prevents extra fields.
4. The type definitions specify the expected data types.
5. The date pattern specifies the YYYY-MM-DD format for non-null dates.
6. The currency enumeration restricts non-null currency values to INR, USD, or EUR.
7. Null values are allowed when information is missing.

The schema was documented as the expected output specification. It was not enabled as API-based schema enforcement during testing.

### 5.5 Prompt Used

```text
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
```

### 5.6 Five Test Inputs and Actual Outputs

#### Test 1: Complete Payment Information

**Input:**

```text
Rahul paid ₹1,250 to the college on 15 November 2026 for registration.
```

**Actual Model Output:**

```json
{
  "name": "Rahul",
  "date": "2026-11-15",
  "amount": 1250,
  "currency": "INR"
}
```

**Result:** Correct. All four fields were extracted accurately.

#### Test 2: US Dollar Payment

**Input:**

```text
Daniel received a payment of $120 on 5 September 2026 for freelance work.
```

**Actual Model Output:**

```json
{
  "name": "Daniel",
  "date": "2026-09-05",
  "amount": 120,
  "currency": "USD"
}
```

**Result:** Correct. The model extracted the name, date, amount, and USD currency code accurately.

#### Test 3: Missing Date

**Input:**

```text
Meera paid 2,400 rupees for her examination fee.
```

**Actual Model Output:**

```json
{
  "name": "Meera",
  "date": null,
  "amount": 2400,
  "currency": "INR"
}
```

**Result:** Correct. The model used null for the missing date and extracted the other information accurately.

#### Test 4: Missing Name

**Input:**

```text
A payment of EUR 75 was made on 21 November 2026 for a software subscription.
```

**Actual Model Output:**

```json
{
  "name": null,
  "date": "2026-11-21",
  "amount": 75,
  "currency": "EUR"
}
```

**Result:** Correct. The model used null for the missing name and extracted the remaining information accurately.

#### Test 5: Informal Message and Numeric Date

**Input:**

```text
hey, this is Arjun — transferred Rs. 3,500 to the workshop yesterday, 17/11/26, for project materials.
```

**Actual Model Output:**

```json
{
  "name": "Arjun",
  "date": "2026-11-17",
  "amount": 3500,
  "currency": "INR"
}
```

**Result:** Correct. The model handled informal wording, the Rs. currency abbreviation, and the numeric date format accurately.

### 5.7 Results and Success Rate

All five test inputs produced the expected information in the required JSON structure.

| Evaluation | Result |
|---|---|
| Total test inputs | 5 |
| Successful outputs | 5 |
| Incorrect outputs | 0 |
| Success rate | 100% |
| Required JSON keys present | Yes |
| Missing values represented using null | Yes |
| Amounts returned as numbers | Yes |

**Success Rate Calculation:**

Success Rate = (Successful Outputs / Total Test Inputs) × 100

Success Rate = (5 / 5) × 100 = **100%**

### 5.8 Techniques That Improved Reliability

The following techniques helped produce consistent structured outputs:

1. **Explicit field definitions:** Specifying the exact four JSON keys made the expected structure clear.
2. **Data type instructions:** Defining strings, numbers, and null values helped maintain consistent data types.
3. **Exact output restrictions:** Instructing the model to return only JSON prevented additional explanations.
4. **Examples:** Providing an input and its expected JSON output demonstrated the desired format.
5. **Missing-value rules:** Explicitly instructing the model to use null prevented it from inventing missing information.
6. **Date and currency normalization:** Specifying the required date format and currency codes made the extracted data consistent.
7. **JSON Schema definition:** Defining required fields, data types, allowed currency values, and date formatting provided a formal specification for the expected output.

The experiment used prompt instructions and an example in Google AI Studio. The JSON Schema was documented for the experiment, but API-based JSON mode or schema enforcement was not enabled.

### 5.9 Conclusion

The experiment demonstrates that structured prompting can help an AI model extract information and return it in a consistent JSON format.

The model successfully completed all five test cases, including messages with missing information and informal wording. The final success rate was 100%.

Explicit field definitions, data types, examples, missing-value rules, and a formal JSON Schema helped define a reliable and consistent output format.

---

## 6. Overall Comparison of Experiments

| Experiment | Prompting Technique | Main Observation |
|---|---|---|
| Experiment 1 | Zero-Shot vs Few-Shot | Both produced the correct sentiment classification |
| Experiment 2 | Direct vs Step-by-Step | Both produced the correct answer; step-by-step showed the calculations |
| Experiment 3 | Structured JSON Output | All five test cases passed with a 100% success rate |

## 7. Overall Learning Outcomes

Through these experiments, I learned the following:

1. Zero-shot prompting can perform classification tasks without examples.
2. Few-shot prompting provides examples that guide the model's responses.
3. Step-by-step instructions can make multi-step solutions easier to understand and verify.
4. Structured output instructions help produce consistent JSON responses.
5. Explicit field definitions, examples, and missing-value rules improve output consistency.
6. JSON Schema provides a formal way to describe expected JSON fields, types, and validation rules.
7. Testing prompts with multiple inputs is important for evaluating model reliability.

## 8. Final Conclusion

This milestone demonstrated how prompt engineering techniques can influence AI model responses.

The experiments showed that different prompting approaches are useful for different tasks.

Zero-shot and few-shot prompting were effective for sentiment classification. Direct and step-by-step prompting both solved the mathematical problem, while step-by-step prompting provided a more detailed explanation.

Structured JSON prompting successfully extracted payment information across five test cases with a 100% success rate.

Overall, these experiments helped develop a practical understanding of prompt design, model response evaluation, and structured output generation.
