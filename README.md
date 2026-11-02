# EX3-Implementation-of-GSP-Algorithm-in-Python
**DATE:** 02-11-2026
### NAME : LATHIKA K
### REG NO : 212224230140
### AIM
To implement the GSP Algorithm in Python.

### DESCRIPTION
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.

### STEPS
1. **Database Scanning:** GSP scans the sequence database to determine the support of each item in the dataset.
2. **Candidate Generation:** It generates a set of candidate sequences using frequent items found in the previous step.
3. **Pattern Growth:** It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. **Repeat:** The process continues until no new sequences meet the minimum support threshold.

GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.

### PROCEDURE

1. Import the required libraries `defaultdict` and `combinations`.
2. Define the `generate_candidates(dataset, k)` function to generate candidate patterns of length k from the dataset.
3. Define the `gsp(dataset, min_support)` function to implement the GSP algorithm.
4. Define example datasets for Top Wear, Bottom Wear, and Party Wear.
5. Set the minimum support threshold to 2.
6. Apply the GSP algorithm to each category.
7. Display the frequent patterns along with their support counts.
8. Visualize the frequent patterns using Matplotlib.

### PROGRAM

```python
from collections import defaultdict
from itertools import combinations

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    candidates = defaultdict(int)

    for sequence in dataset:
        for candidate in set(combinations(sequence, k)):
            candidates[candidate] += 1

    return candidates


# Function to perform GSP algorithm
def gsp(dataset, min_support):
    k = 1
    frequent_patterns = {}

    while True:
        candidates = generate_candidates(dataset, k)

        frequent_k = {
            pattern: support
            for pattern, support in candidates.items()
            if support >= min_support
        }

        if not frequent_k:
            break

        frequent_patterns.update(frequent_k)
        k += 1

    return frequent_patterns


# Example dataset for each category
top_wear_data = [
    ["blouse", "t-shirt", "tank_top"],
    ["hoodie", "sweater", "top"],
    ["hoodie"],
    ["hoodie", "sweater"]
]

bottom_wear_data = [
    ["jeans", "trousers", "shorts"],
    ["leggings", "skirt", "chinos"]
]

party_wear_data = [
    ["cocktail_dress", "evening_gown", "blazer"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress"],
    ["party_dress"]
]


# Minimum support threshold
min_support = 2

# Perform GSP algorithm for each category
top_wear_result = gsp(top_wear_data, min_support)
bottom_wear_result = gsp(bottom_wear_data, min_support)
party_wear_result = gsp(party_wear_data, min_support)


# Output the frequent sequential patterns
print("Frequent Sequential Patterns - Top Wear:")
if top_wear_result:
    for pattern, support in top_wear_result.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found in Top Wear.")


print("\nFrequent Sequential Patterns - Bottom Wear:")
if bottom_wear_result:
    for pattern, support in bottom_wear_result.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found in Bottom Wear.")


print("\nFrequent Sequential Patterns - Party Wear:")
if party_wear_result:
    for pattern, support in party_wear_result.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found in Party Wear.")


# Visualization using Matplotlib
import matplotlib.pyplot as plt

def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot(
            [str(pattern) for pattern in patterns],
            support,
            marker='o',
            linestyle='-',
            color='blue'
        )

        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")


# Visualize frequent sequential patterns for each category
visualize_patterns_line(top_wear_result, 'Top Wear')
visualize_patterns_line(bottom_wear_result, 'Bottom Wear')
visualize_patterns_line(party_wear_result, 'Party Wear')
```

### OUTPUT

**Frequent Sequential Patterns – Top Wear:**
```text
Pattern: ('sweater',), Support: 2
Pattern: ('hoodie',), Support: 3
Pattern: ('hoodie', 'sweater'), Support: 2
```

**Frequent Sequential Patterns – Bottom Wear:**
```text
No frequent sequential patterns found in Bottom Wear.
```

**Frequent Sequential Patterns – Party Wear:**
```text
Pattern: ('suit',), Support: 4
Pattern: ('party_dress',), Support: 6
Pattern: ('formal_dress',), Support: 4
Pattern: ('party_dress', 'formal_dress'), Support: 4
Pattern: ('formal_dress', 'suit'), Support: 4
Pattern: ('party_dress', 'suit'), Support: 4
Pattern: ('party_dress', 'formal_dress', 'suit'), Support: 4
```

### VISUALIZATION

The frequent patterns are visualized using Matplotlib line plots.

1. **Top Wear:** Insert the screenshot of the Top Wear graph.
2. <img width="1272" height="882" alt="Screenshot 2026-10-31 233500" src="https://github.com/user-attachments/assets/c4f3fc2d-b057-476d-bf0c-c234c5f60aa4" />

3. **Party Wear:** Insert the screenshot of the Party Wear graph.
   <img width="1252" height="832" alt="Screenshot 2026-10-31 233538" src="https://github.com/user-attachments/assets/90fbd650-cdc9-40b4-928b-f380199cf41d" />


*Note: Bottom Wear has no frequent patterns, so no graph is displayed for this category.*

### RESULT

Thus, the GSP algorithm was successfully implemented in Python, and frequent patterns were identified for Top Wear, Bottom Wear, and Party Wear datasets. The frequent patterns were also visualized using Matplotlib.
