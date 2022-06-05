# Contingency table 
A contingency table shows all the classifications that have been done with the real value. In a contingency table you can see exactly how things were wrongly classified as what. 

# Example
Here is an example table in a result when classifying languages.

| Language | German | French | Dutch | Italian | English |
| -------- | ------ | ------ | ----- | ------- | ------- |
| German   | 4030.  | 1.     | 2.    | 4.      | 13.     | 
| French   | 3.     | 3385.  | 2.    | 11.     | 7.      |
| Dutch    | 20.    | 2.     | 1230. | 4.      | 24.     |
| Italian  | 0.     | 4.     | 2.    | 10682.  | 4.      |
| English  | 10.    | 20.    | 13.   | 43.     | 16559.  |

So what you can read from this table is that 4030 German words were classified as German 4030 times but also 3 French, 20 Dutch and 10 Italian words were classified as German. 

1 German word was also classified as French.
2 German words were also classified as Dutch.
4 German words were also classified as Italian.
13 German words were also classified as English. 

So that is how you read these tables. 

Here was my code to create the [Evaluating Classification models](Evaluating%20Classification%20models.md) scores.


```python
def precision(contingency_table, label):
    index = labels2ids[label]
    result = contingency_table.T[index]
    
    tp = result[index]
    
    mask = np.ones(len(result), bool)
    mask[index] = False
    
    fp = sum(result[mask])
    
    return tp / (tp + fp)


def recall(contingency_table, label):
    ct = contingency_table
    index = labels2ids[label]
    
    result = ct.T[index]
    
    tp = result[index]
    
    fn = sum(map(lambda x : x[[len(ct))](ct|True if i == index else False for i in range(len(ct|[len(ct|[len(ct|[len(ct))](ct))]])))]])), ct.T))
    
    return tp / (tp + fn)
    


def F_measure(contingency_table, label, Beta=1):
    P = precision(contingency_table, label)
    R = recall(contingency_table, label)
    return ((Beta**2 + 1) * P*R) / (Beta**2 * P + R)
```
