Sure! Here's a Python script that demonstrates the use of Association Rules using the Apriori and FP-Growth algorithms.

```python
import pandas as pd
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori, association_rules
from mlxtend.frequent_patterns import fpgrowth

# Sample dataset
dataset = [['Milk', 'Onion', 'Nutmeg', 'Kidney Beans', 'Eggs', 'Yogurt'],
           ['Dill', 'Onion', 'Nutmeg', 'Kidney Beans', 'Eggs', 'Yogurt'],
           ['Milk', 'Apple', 'Kidney Beans', 'Eggs'],
           ['Milk', 'Unicorn', 'Corn', 'Kidney Beans', 'Yogurt'],
           ['Corn', 'Onion', 'Onion', 'Kidney Beans', 'Ice cream', 'Eggs']]

# Create one-hot encoded DataFrame
te = TransactionEncoder()
te_data = te.fit(dataset).transform(dataset)
df = pd.DataFrame(te_data, columns=te.columns_)

# Generate frequent itemsets using Apriori algorithm
frequent_itemsets_apriori = apriori(df, min_support=0.2, use_colnames=True)
print("Frequent Itemsets (Apriori):")
print(frequent_itemsets_apriori)

# Generate association rules from frequent itemsets using confidence threshold
rules_apriori = association_rules(frequent_itemsets_apriori, metric="confidence", min_threshold=0.7)
print("\nAssociation Rules (Apriori):")
print(rules_apriori)

# Generate frequent itemsets using FP-Growth algorithm
frequent_itemsets_fpgrowth = fpgrowth(df, min_support=0.2, use_colnames=True)
print("\nFrequent Itemsets (FP-Growth):")
print(frequent_itemsets_fpgrowth)

# Generate association rules from frequent itemsets using confidence threshold
rules_fpgrowth = association_rules(frequent_itemsets_fpgrowth, metric="confidence", min_threshold=0.7)
print("\nAssociation Rules (FP-Growth):")
print(rules_fpgrowth)
```

This script uses the `mlxtend` library, which provides implementations of the Apriori and FP-Growth algorithms. It first creates a one-hot encoded DataFrame from the given dataset. Then, it applies the Apriori algorithm to generate frequent itemsets and prints them. Next, it applies the association rules algorithm to derive association rules from the frequent itemsets and prints them.

Similarly, it applies the FP-Growth algorithm to generate frequent itemsets and prints them. Finally, it applies the association rules algorithm to derive association rules from the frequent itemsets generated by FP-Growth and prints them.

You can replace the `dataset` variable with your own dataset to observe the results for your data. Make sure to install the `mlxtend` library before running this script by using the command `pip install mlxtend`.