# Day 4


```python
import pandas as pd 
import re

arr = []
# import data
with open("input.txt", 'r') as file:
    curDict = dict()
    for line in file:
        if line == "\n" or line == "":
            # new entry! add data to array and create empty dictionary
            arr.append(curDict)
            curDict = dict()
        else:
            # parse input into tuples and add into dictionary
            tuples=line.rstrip().split(' ')
            for i in tuples:
                i = i.split(':')
                curDict[i[0]]=i[1]

# Creates DataFrame. 
df = pd.DataFrame(arr) 
df.tail(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>eyr</th>
      <th>hgt</th>
      <th>pid</th>
      <th>ecl</th>
      <th>byr</th>
      <th>hcl</th>
      <th>iyr</th>
      <th>cid</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>284</th>
      <td>2039</td>
      <td>72cm</td>
      <td>#d80d30</td>
      <td>#cc4aff</td>
      <td>2025</td>
      <td>5307c9</td>
      <td>2025</td>
      <td>224</td>
    </tr>
    <tr>
      <th>285</th>
      <td>2027</td>
      <td>184</td>
      <td>58151347</td>
      <td>NaN</td>
      <td>2015</td>
      <td>98fb9d</td>
      <td>2029</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>286</th>
      <td>2021</td>
      <td>183cm</td>
      <td>164cm</td>
      <td>xry</td>
      <td>2019</td>
      <td>#18171d</td>
      <td>2013</td>
      <td>187</td>
    </tr>
  </tbody>
</table>
</div>



## Part 1


```python
df['valid_p1']=~(df.drop(['cid'], axis=1)).isnull().any(axis=1)
df['valid_p1'].value_counts()
```




    True     219
    False     68
    Name: valid_p1, dtype: int64



## Part 2


```python
def isPassportValid(eyr,hgt,pid,ecl,byr,hcl,iyr):
    validity = False

    if not(pd.isna(eyr) or pd.isna(hgt) or pd.isna(pid) or pd.isna(ecl) or pd.isna(byr) or pd.isna(hcl) or pd.isna(iyr)):
        passport_valid = []
        # byr (Birth Year) - four digits; at least 1920 and at most 2002.
        passport_valid.append(len(re.findall("(19[2-9][0-9]|200[0-2])", byr)) == 1)

        # iyr (Issue Year) - four digits; at least 2010 and at most 2020.
        passport_valid.append(len(re.findall("(201[0-9]|2020)", iyr)) == 1)

        # eyr (Expiration Year) - four digits; at least 2020 and at most 2030.
        passport_valid.append(len(re.findall("(202[0-9]|2030)", eyr)) == 1)

        # hgt (Height) - a number followed by either cm or in:
            # If cm, the number must be at least 150 and at most 193.
            # If in, the number must be at least 59 and at most 76.
        passport_valid.append(len(re.findall("(1[5-8][0-9]cm|19[0-3]cm|59in|6[0-9]in|7[0-6]in)", hgt)) == 1)

        # hcl (Hair Color) - a # followed by exactly six characters 0-9 or a-f.
        passport_valid.append(len(re.findall("^#[a-f0-9]{6}", hcl)) == 1)

        # ecl (Eye Color) - exactly one of: amb blu brn gry grn hzl oth.
        passport_valid.append(len(re.findall("(amb|blu|brn|gry|grn|hzl|oth)", ecl)) == 1)

        # pid (Passport ID) - a nine-digit number, including leading zeroes.
        passport_valid.append(len(re.findall("^\d{9}$", pid)) == 1)

        validity = not(False in passport_valid)

    return validity
```


```python
df['valid_p2']=df.apply(lambda x: isPassportValid(x['eyr'], x['hgt'], x['pid'], x['ecl'], x['byr'], x['hcl'], x['iyr']), axis=1)
df['valid_p2'].value_counts()
```




    False    160
    True     127
    Name: valid_p2, dtype: int64


