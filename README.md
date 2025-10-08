### EX3 Implementation of GSP Algorithm In Python
### DATE: 
### AIM:
To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>

### Program:

```python
from collections import defaultdict
from itertools import combinations

# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    c = defaultdict(int)
    for seq in dataset:
        # flatten into list of items (your version mixes strings/lists)
        flat_seq = []
        for itemset in seq:
            if isinstance(itemset, str):
                flat_seq.extend(itemset.split(','))   # split commas
            else:
                flat_seq.extend(itemset)
        # ensure uniqueness per sequence
        for comb in set(combinations(sorted(flat_seq), k)):
            c[comb] += 1
    # collect all frequent patterns
    res = {}
    for item, support in c.items():
        if support >= min_support:
            res[item] = support
    return res

# Function to perform GSP algorithm
def gsp(dataset, min_support):
    k = 1
    fp = defaultdict(int)
    seq=dataset
    while True:
        c = generate_candidates(seq, k)
        if not c:
            break
        fp.update(c)
        k += 1
    return fp

# Example dataset for each category
Dataset_1 = [
    [["a"],["b"],["c"],["b","e"],["c","f"],["g"],["a","b","e"]],
    [["a"],["d"],["b","c"],["c"],["f","g"],["c","h"]],
    [["b"],["c"],["a","d"],["e"],["b"],["f"],["c","d","f","g","h"]],
    [["c"],["e","c"],["e","h"]]
]
Dataset_2 = [
    [["b","d"],["c"],["b"],["a","c"]],
    [["b","f"],["c","e"],["b"],["f","g"]],
    [["a","h"],["b","f"],["a"],["b","f"]],
    [["b","e"],["c","e"],["d"]],
    [["a"],["b","d"],["b"],["c"],["b"],["a","d","e"]]
]
# Minimum support threshold
min_support = 3

# Perform GSP algorithm for each category
Dataset_1_result = gsp(Dataset_1, min_support)
Dataset_2_result = gsp(Dataset_2, min_support)

# Output the frequent sequential patterns for each category
print("Frequent Sequential Patterns - Dataset_1:")
if Dataset_1_result:
    for pattern, support in Dataset_1_result.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found in Dataset_1.")

print("\nFrequent Sequential Patterns - Dataset_2:")
if Dataset_2_result:
    for pattern, support in Dataset_2_result.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found in Dataset_2.")

```
### Output:
<img width="400" height="320" alt="image" src="https://github.com/user-attachments/assets/be3a1776-7e6c-4179-a075-cc12dd92283b" />
</br>
<img width="400" height="400" alt="image" src="https://github.com/user-attachments/assets/2b371945-1b97-4aa2-b46b-b9566b12b802" />
</br>
<img width="400" height="380" alt="image" src="https://github.com/user-attachments/assets/1c2f8e25-92bd-44c7-a00f-475ef1fb9c02" />

### Visualization:
```python
import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for each category using a line plot
visualize_patterns_line(Dataset_1_result, 'Dataset_1')
visualize_patterns_line(Dataset_2_result, 'Dataset_2')
```
### Output:
<img width="820" height="495" alt="image" src="https://github.com/user-attachments/assets/7579bf21-da44-4ef4-8a84-7f9a289edcab" />

<img width="820" height="495" alt="image" src="https://github.com/user-attachments/assets/f9718d78-7e35-48a8-8815-2a25839a15b1" />

### Result:
GSP Algorithm In Python has been implemented successfully.
