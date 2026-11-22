# Experiment 2: Direct Prompting vs Step-by-Step Prompting

## 1. Objective
To compare direct prompting and step-by-step prompting using a multi-step mathematical problem.

## 2. Tool Used
- Platform: Google AI Studio
- Model: Gemini (Model 1, as displayed in the Playground)

## 3. Direct Prompting

### Prompt Used
A college has 240 students. 35% of students participate in a coding competition. Of those participants, 25% qualify for the final round. How many students qualify for the final round?

Give only the final answer.

### Actual Model Output
21

### Result
Correct. The model provided the final answer without showing the calculation steps.

## 4. Step-by-Step Prompting

### Prompt Used
Solve the following problem carefully.

A college has 240 students. 35% of students participate in a coding competition. Of those participants, 25% qualify for the final round.

Break the calculation into clear steps. Calculate the number of participants first, then calculate the number who qualify. Give the final answer at the end.

### Actual Model Output
Here is the step-by-step calculation:

**Step 1: Calculate the number of participants**

- Total number of students = 240
- Percentage of students participating = 35% (or 0.35)

Number of participants = 240 × 0.35 = 84

There are 84 students participating in the coding competition.

**Step 2: Calculate the number of students who qualify for the final round**

- Number of participants = 84
- Percentage of participants who qualify = 25% (or 0.25)

Number who qualify = 84 × 0.25 = 21

**Final Answer:** 21 students qualify for the final round.

### Result
Correct. The model calculated the number of participants first and then calculated the number who qualified for the final round.

## 5. Comparison and Analysis

| Evaluation | Direct Prompting | Step-by-Step Prompting |
|---|---|---|
| Reasoning instructions | No | Yes |
| Shows calculation steps | No | Yes |
| Actual final answer | 21 | 21 |
| Correct answer | Yes | Yes |

Both prompting techniques produced the correct final answer.

Direct prompting was shorter and gave the answer immediately. Step-by-step prompting provided a clear explanation of the two calculations, making the solution easier to follow and verify.

For this problem, step-by-step prompting improved the transparency of the response, but it did not change the final answer or improve its accuracy because both approaches were correct.

## 6. Conclusion

The experiment demonstrates that direct prompting and step-by-step prompting can both solve a multi-step mathematical problem correctly. Direct prompting is useful when only the final answer is needed, while step-by-step prompting is more useful when the calculation process and explanation are important.
