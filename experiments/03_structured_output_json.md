# Experiment 3: Structured Output Using JSON

## 1. Objective

To test whether an AI model can extract payment information from different types of messages and return the information in a consistent JSON format.

## 2. Tool Used

- Platform: Google AI Studio
- Model: Gemini (Model 1, as displayed in the Playground)

## 3. JSON Structure and Prompt

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

## 4. Five Test Inputs and Actual Outputs

### Test 1: Complete Payment Information

**Input:**

Rahul paid ₹1,250 to the college on 15 November 2026 for registration.

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

### Test 2: US Dollar Payment

**Input:**

Daniel received a payment of $120 on 5 September 2026 for freelance work.

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

### Test 3: Missing Date

**Input:**

Meera paid 2,400 rupees for her examination fee.

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

### Test 4: Missing Name

**Input:**

A payment of EUR 75 was made on 21 November 2026 for a software subscription.

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

### Test 5: Informal Message and Numeric Date

**Input:**

hey, this is Arjun — transferred Rs. 3,500 to the workshop yesterday, 17/11/26, for project materials.

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

## 5. Results and Success Rate

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

(5 successful outputs / 5 total tests) × 100 = 100%

## 6. Techniques That Improved Reliability

The following prompting techniques helped produce consistent structured outputs:

1. **Explicit field definitions:** Specifying the exact four JSON keys made the expected structure clear.
2. **Data type instructions:** Defining strings, numbers, and null values helped maintain consistent data types.
3. **Exact output restrictions:** Instructing the model to return only JSON prevented additional explanations.
4. **Examples:** Providing an input and its expected JSON output demonstrated the desired format.
5. **Missing-value rules:** Explicitly instructing the model to use null prevented it from inventing missing information.
6. **Date and currency normalization:** Specifying the required date format and currency codes made the extracted data consistent.

The experiment used prompt instructions and an example in Google AI Studio. API-based JSON mode or schema enforcement was not used.

## 7. Conclusion

The experiment demonstrates that structured prompting can help an AI model extract information and return it in a consistent JSON format.

The model successfully completed all five test cases, including messages with missing information and informal wording. The final success rate was 100%.

Explicit field definitions, data types, examples, and missing-value rules helped produce accurate and consistent outputs.
