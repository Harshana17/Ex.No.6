# Ex.No.6 AI-Assisted Programming and Debugging

## Date: 07.09.2026
## Register no: 2122242400523

# Aim:
To write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools

# AI Tools Required:

ChatGPT – Code generation, debugging, optimization and analysis

Google Gemini – Code generation and optimization

Microsoft Copilot – Code analysis and test generation

Python, C and Java environments – Program execution and verification

# Explanation:
Experiment the persona pattern as a programmer for any specific applications related with your interesting area. 
Generate the outoput using more than one AI tool and based on the code generation analyse and discussing that. 
Learnerss generate

Python
C
Java
using AI.

Then

identify bugs
optimise code
explain complexity
generate unit tests
Finally compare manual coding versus AI-assisted coding. 
Deliverable

Code quality analysis.

# Output:

The **persona pattern** is used to make each AI tool respond as a specific kind of programmer, which produces more focused, domain-relevant code. Here, the persona chosen is:

> "Act as a Python/C/Java developer specializing in agri-tech API integrations."

Multiple AI tools (ChatGPT, Gemini, Copilot) are given the same persona-based prompt for the same application area — **Smart Farming Advisory** — and their generated code and outputs are compared. The application integrates with **multiple external AI/weather advisory APIs**, compares the rainfall-probability outputs returned by each source, checks whether the sources agree, and generates a single actionable irrigation recommendation.

The same underlying logic is then implemented in Python, C, and Java, debugged, optimized, analyzed for complexity, and tested — followed by a comparison of AI-assisted coding versus manual coding.

## OBJECTIVE
To understand how AI tools can assist programmers in different stages of software development:

- Code generation using the persona pattern
- Multi-API integration and output comparison
- Bug identification and debugging
- Code optimization
- Complexity analysis
- Unit-test generation
- Comparison with manual coding
- Code-quality analysis

## SCENARIO

**Smart Farming Advisory — Multi-Source AI Comparison**

A farm advisory application queries **three different AI/weather advisory sources** (simulated locally as `SourceA`, `SourceB`, `SourceC`) for the probability of rainfall in the next 24 hours. The program must:

- Accept rainfall-probability readings from each AI source.
- Validate the readings (must be between 0 and 100).
- Calculate the minimum, maximum, and average probability across sources.
- Detect disagreement between sources (a wide spread between minimum and maximum).
- Generate an actionable insight: **"Skip Irrigation"** if the average probability is above a 60% threshold, otherwise **"Irrigate Field"**.
- Handle invalid or empty input safely.

The program is developed in Python, C, and Java using AI assistance with the persona pattern.

## PROCEDURE

The following workflow is followed for all three languages:

```
Persona Prompt → Generate → Execute → Find Bugs → Fix → Optimize
    → Analyze Complexity → Generate Tests → Verify → Compare
```

---

## 1. PYTHON

### Prompt 1 – Code Generation (Persona Pattern)
> Act as a Python developer specializing in agri-tech API integrations. Write a beginner-friendly program that accepts rainfall-probability readings from three simulated AI weather sources, calculates the minimum, maximum and average, checks for disagreement between sources, and generates an actionable irrigation insight using a threshold of 60. Include input validation and use a function for modularity. Explain the logic briefly.

**Code:**
```python
def generate_insight(readings, threshold):
    minimum = min(readings)
    maximum = max(readings)
    average = sum(readings) / len(readings)
    disagreement = maximum - minimum

    insight = "Skip Irrigation" if average > threshold else "Irrigate Field"

    return minimum, maximum, average, disagreement, insight


readings = [72, 65, 40]
threshold = 60

result = generate_insight(readings, threshold)

print("Minimum:", result[0])
print("Maximum:", result[1])
print("Average:", result[2])
print("Disagreement:", result[3])
print("Insight:", result[4])
```

**Output**
```
Minimum: 40
Maximum: 72
Average: 59.0
Disagreement: 32
Insight: Irrigate Field
```

### Prompt 2 – Bug Identification and Debugging
> Analyze the Python program for syntax, logical and runtime errors. Check especially for empty input, invalid readings outside 0–100, and incorrect boundary conditions. Explain the errors and provide corrected code.

**Bug Identified:**
The original program does not validate that readings lie between 0 and 100, and does not handle an empty list — `min()`, `max()`, and division by zero will fail.

**Corrected Code:**
```python
def generate_insight(readings, threshold):
    valid = [x for x in readings if 0 <= x <= 100]

    if not valid:
        return None

    minimum = min(valid)
    maximum = max(valid)
    average = sum(valid) / len(valid)
    disagreement = maximum - minimum

    insight = "Skip Irrigation" if average > threshold else "Irrigate Field"

    return minimum, maximum, average, disagreement, insight


readings = [72, 65, 40]
threshold = 60

result = generate_insight(readings, threshold)

if result:
    print("Minimum:", result[0])
    print("Maximum:", result[1])
    print("Average:", result[2])
    print("Disagreement:", result[3])
    print("Insight:", result[4])
else:
    print("No valid AI source readings.")
```

### Prompt 3 – Code Optimization
> Optimize the corrected Python program for readability, modularity and efficiency without changing its functionality. Use meaningful names and avoid unnecessary operations.

**Optimization:**
- Meaningful variable names (`disagreement`, `insight`)
- Input validation restricted to a valid probability range
- Modular function design
- Simple list processing
- Clear conditional logic for the final insight

### Prompt 4 – Complexity Analysis
> Analyze the time and auxiliary space complexity of this Python multi-source insight program for n AI sources. Explain the complexity briefly.

**Analysis:**
- **Time Complexity:** O(n)
- **Auxiliary Space Complexity:** O(n)

The program processes the readings a fixed number of times; the `valid` list requires memory proportional to the input size.

### Prompt 5 – Unit Test Generation
> Generate unit test cases for the Python multi-source insight program. Include normal, boundary, abnormal, invalid and empty inputs with expected outputs.

| Test Case | Input | Expected Result |
|---|---|---|
| TC01 | [72, 65, 40] | Irrigate Field |
| TC02 | [80, 75, 90] | Skip Irrigation |
| TC03 | [60, 60, 60] | Irrigate Field (boundary, avg = threshold) |
| TC04 | [-10, 50, 120] | Invalid values ignored |
| TC05 | [] | No valid AI source readings |

---

## 2. C

### Prompt 1 – Code Generation (Persona Pattern)
> Act as a C developer specializing in agri-tech API integrations. Write a program that accepts rainfall-probability readings from three AI weather sources, calculates minimum, maximum and average, and generates an irrigation insight using a threshold of 60. Include input validation and modular functions. Keep the code beginner-friendly.

**AI-Generated Code:**
```c
#include <stdio.h>

void generateInsight(int readings[], int n, int threshold)
{
    int min = readings[0];
    int max = readings[0];
    int sum = 0;

    for (int i = 0; i < n; i++)
    {
        if (readings[i] < min)
            min = readings[i];

        if (readings[i] > max)
            max = readings[i];

        sum += readings[i];
    }

    float average = (float)sum / n;

    printf("Minimum: %d\n", min);
    printf("Maximum: %d\n", max);
    printf("Average: %.2f\n", average);
    printf("Disagreement: %d\n", max - min);
    printf("Insight: %s\n", (average > threshold) ? "Skip Irrigation" : "Irrigate Field");
}

int main()
{
    int readings[] = {72, 65, 40};
    generateInsight(readings, 3, 60);

    return 0;
}
```

**Output:**
```
Minimum: 40
Maximum: 72
Average: 59.00
Disagreement: 32
Insight: Irrigate Field
```

### Prompt 2 – Bug Identification and Debugging
> Analyze this C program for runtime, logical and boundary errors. Check empty input, array access, division by zero, integer division and invalid readings (outside 0–100). Provide corrected code.

**Bug Identified:**
The program accesses `readings[0]` even when `n` is zero, does not validate the 0–100 range, and would perform integer division if the cast were missing.

**Correction:**
```c
if (n <= 0)
{
    printf("No valid AI source readings.\n");
    return;
}
```
Each reading is validated to be within 0–100 before being processed, and `(float)sum / n` is used to ensure floating-point division.

### Prompt 3 – Code Optimization
> Optimize the corrected C program for readability, efficiency and safe input handling. Keep the implementation simple and modular.

**Optimization:**
- Added input-size and range validation.
- Used a separate processing function.
- Used floating-point division for the average.
- Used meaningful variable names.
- Removed unnecessary operations.

### Prompt 4 – Complexity Analysis
> Determine the time and auxiliary space complexity of the C multi-source insight program for n readings.

- **Time Complexity:** O(n)
- **Auxiliary Space Complexity:** O(1)

The array is traversed once, and only a fixed number of additional variables are used.

### Prompt 5 – Unit Test Generation
> Generate unit test cases for the C multi-source insight program covering normal, boundary, abnormal, invalid and empty input.

| Test Case | Input | Expected Result |
|---|---|---|
| TC01 | {72,65,40} | Irrigate Field |
| TC02 | {80,75,90} | Skip Irrigation |
| TC03 | {60,60,60} | Irrigate Field (boundary) |
| TC04 | {-10,50,120} | Invalid value handled |
| TC05 | Empty input | Error handled safely |

---

## 3. JAVA

### Prompt 1 – Code Generation (Persona Pattern)
> Act as a Java developer specializing in agri-tech API integrations. Create a beginner-friendly program that calculates minimum, maximum and average rainfall-probability values from three AI weather sources and generates an irrigation insight using a threshold of 60. Use a method for modularity and include input validation.

**AI-Generated Code:**
```java
public class InsightGenerator {

    static void generateInsight(int[] readings, int threshold) {

        int min = readings[0];
        int max = readings[0];
        int sum = 0;

        for (int value : readings) {
            if (value < min)
                min = value;

            if (value > max)
                max = value;

            sum += value;
        }

        double average = (double) sum / readings.length;

        System.out.println("Minimum: " + min);
        System.out.println("Maximum: " + max);
        System.out.println("Average: " + average);
        System.out.println("Disagreement: " + (max - min));
        System.out.println("Insight: " +
                (average > threshold ? "Skip Irrigation" : "Irrigate Field"));
    }

    public static void main(String[] args) {

        int[] readings = {72, 65, 40};

        generateInsight(readings, 60);
    }
}
```

**Output:**
```
Minimum: 40
Maximum: 72
Average: 59.0
Disagreement: 32
Insight: Irrigate Field
```

### Prompt 2 – Bug Identification and Debugging
> Analyze this Java program for runtime and logical errors. Check empty arrays, invalid readings (outside 0–100), array access and average calculation. Provide corrected code and explain the corrections briefly.

**Bug Identified:**
The program directly accesses `readings[0]`; an empty or null array causes an `ArrayIndexOutOfBoundsException` or `NullPointerException`. Readings outside the valid 0–100 range are not filtered out.

**Correction:**
```java
if (readings == null || readings.length == 0) {
    System.out.println("No valid AI source readings.");
    return;
}
```
Invalid readings outside the 0–100 range are ignored during processing.

### Prompt 3 – Code Optimization
> Optimize the corrected Java program for readability, modularity and efficient processing while preserving the same functionality.

**Optimization:**
- Added null and empty-array checks.
- Used a separate method.
- Used meaningful variable names.
- Ignored invalid (out-of-range) readings.
- Used enhanced for loops.

### Prompt 4 – Complexity Analysis
> Analyze the time and auxiliary space complexity of the Java multi-source insight program for n readings.

- **Time Complexity:** O(n)
- **Auxiliary Space Complexity:** O(1)

The input array is processed linearly and only a fixed number of variables are used.

### Prompt 5 – Unit Test Generation
> Generate unit test cases for the Java multi-source insight program covering normal, boundary, abnormal, invalid and empty inputs.

| Test Case | Input | Expected Result |
|---|---|---|
| TC01 | {72,65,40} | Irrigate Field |
| TC02 | {80,75,90} | Skip Irrigation |
| TC03 | {60,60,60} | Irrigate Field (boundary) |
| TC04 | {-10,50,120} | Invalid value handled |
| TC05 | {} | Empty input handled |

---

## AI OUTPUT COMPARISON

The three AI tools were compared based on their usefulness during the experiment.

| Parameter | ChatGPT | Gemini | Copilot |
|---|---|---|---|
| Code Generation | Very Good | Very Good | Good |
| Debugging | Very Good | Good | Very Good |
| Optimization | Good | Very Good | Good |
| Unit Tests | Very Good | Good | Very Good |
| Explanation | Detailed | Detailed | Concise |
| Overall | Very Good | Very Good | Very Good |

The comparison shows that different AI tools may produce different solutions for the same persona-based requirement. Therefore, generated code must always be executed and verified before use.

## MANUAL CODING VS AI-ASSISTED CODING

| Parameter | Manual Coding | AI-Assisted Coding |
|---|---|---|
| Development Time | Higher | Lower |
| Code Generation | Manual | AI-assisted |
| Debugging | Manual | AI-assisted |
| Optimization | Programmer-dependent | AI suggestions |
| Test Generation | Manual | Faster |
| Error Risk | Programmer-dependent | AI may introduce errors |
| Learning | Strong conceptual involvement | Requires verification |
| Productivity | Moderate | Higher |

## CODE QUALITY ANALYSIS

The generated programs were evaluated based on:

- **Correctness** – Verified through execution and test cases.
- **Readability** – Improved using meaningful names and simple logic.
- **Modularity** – Functions/methods were used for processing and insight generation.
- **Efficiency** – All three implementations have O(n) time complexity.
- **Maintainability** – Clear and modular code is easier to extend to more AI sources.
- **Error Handling** – Empty, invalid, and out-of-range inputs were considered.
- **Testing** – Unit test cases were generated and verified across normal, boundary, and invalid scenarios.

AI-generated code was useful for reducing development time, but execution and manual verification were necessary to ensure correctness of the multi-source comparison logic.

## OBSERVATION

The experiment showed that prompt quality — especially the **persona pattern** ("Act as a … developer specializing in agri-tech API integrations") — directly affects the quality of AI-generated programming solutions. Prompts containing the role, programming language, requirements, constraints, expected behavior, and desired output produced more useful, domain-relevant responses.

AI tools were helpful in generating multi-source comparison code, identifying errors, suggesting optimizations, analyzing complexity, and creating test cases. However, the generated code still required human review and execution, particularly around input validation and threshold-boundary behavior.

## RESULT

Python, C, and Java programs that integrate outputs from multiple simulated AI weather sources, compare them, and generate an actionable irrigation insight were successfully generated using the persona prompting pattern across multiple AI tools.

The programs were debugged, optimized, analyzed for complexity, and tested using AI-generated prompts. The outputs of multiple AI tools were compared, and AI-assisted programming was compared with manual coding.

Thus, the corresponding prompt is executed successfully, and the experiment successfully demonstrated the use of effective persona-based AI prompting throughout the multi-API programming and debugging workflow.

## CONCLUSION

AI tools can assist programmers throughout the software development process — from persona-driven code generation to debugging, optimization, and testing — when integrating with and comparing outputs from multiple AI-based APIs. However, AI-generated code should not be accepted without verification, and disagreement between multiple AI/API sources should always be checked before acting on a generated insight.


# Result: 
The corresponding Prompt is executed successfully.
