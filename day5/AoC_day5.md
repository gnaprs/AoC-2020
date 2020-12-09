# Day 5


```python
import pandas as pd 
import re

seats_bin = []
# import data
with open("input.txt", 'r') as file:
    for line in file:
        line=line.split('\n')[0]

        # recognize that the format of the string is binary in the format: row = [:7], col = [7:]
        current_seat = ""
        for i in line:
            current_seat+={'F': '0','B': '1', 'L': '0', 'R': '1'}.get(i)
        seats_bin.append(current_seat)
```

## Part 1


```python
seats_id = []

for i in seats_bin:
    # converting from binary to row and column no.
    row = int(i[:7],2)
    col = int(i[7:],2)

    # seat ID: multiply the row by 8, then add the column
    seats_id.append(row*8+col)
    
print('Ans:', max(seats_id))
```

    Ans: 953
    

## Part 2


```python
# sort all seats in numerical order
seats_id.sort()

for i, seat_id in enumerate(seats_id):
    # explicitly skip first seat
    if seat_id + 1 != seats_id[i + 1]:
        # my seat is the empty seat behind someone elses'!
        print('Ans:', seat_id + 1)
        break
```

    Ans: 615
    
