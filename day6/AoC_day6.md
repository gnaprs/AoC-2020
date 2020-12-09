# Day 6

```python
import pandas as pd 
import re

groups = []
# import data
with open("input.txt", 'r') as file:
    curGroup = ""
    for line in file:
        if line == "\n" or line == " ":
            groups.append(curGroup)
            curGroup = ""
        else:
            # add current person's answer to group!
            curGroup+=line
```

## Part 1


```python
count_p1 = 0

# add number of unique answers to current count
for i in groups:
    count_p1 += len(set(i.replace('\n','')))

print('Ans:', count_p1)
```

    Ans: 6310
    

## Part 2


```python
count_p2 = 0

for i in groups:
    # count group members and number of unique questions
    group_mem = i.count('\n')
    qns = set(i.replace('\n',''))

    # check if number of answers matches number of group members
    for char in qns:
        if i.count(char) == group_mem:
            count_p2+=1

print('Ans:', count_p2)
```

    Ans: 3193
    
