# Day 3


```python
# import data
with open("input.txt", 'r') as file:
    arr = file.read().splitlines()

arr[0:3] # print first 3 lines
```




    ['...#.....#.......##......#.....',
     '...#..................#........',
     '....##....#.......#............']



## Part 1


```python
position = 0
count = 0

for line in arr:
    if line[position] == "#":
        count += 1
    
    # wrap around if we hit the end of the line
    position = (position + 3)%len(line)
    
print(count) 
```

    220
    

## Part 2


```python
def checkSlope(right, down):
    arr_selected=arr[::down]
    position = 0
    count = 0

    for line in arr_selected:
        if line[position] == "#":
            count += 1
        # wrap around if we hit the end of the line
        position = (position + right)%len(line)
    return count
```


```python
slopes=[[3,1],[1,1],[5,1],[7,1],[1,2]]

prod = 1
for slope in slopes:
    treeNum = checkSlope(slope[0],slope[1])
    print("Right: ", slope[0],"Down: ", slope[1], "Trees: ", treeNum)
    prod *=treeNum   

print("Ans:", prod)
```

    Right:  3 Down:  1 Trees:  220
    Right:  1 Down:  1 Trees:  70
    Right:  5 Down:  1 Trees:  63
    Right:  7 Down:  1 Trees:  76
    Right:  1 Down:  2 Trees:  29
    Ans: 2138320800
    
