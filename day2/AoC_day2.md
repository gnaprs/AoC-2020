# Day 2


```python
import pandas as pd
import numpy as np

# import from given input
df1 = pd.read_csv("input.txt", header=None)
arr=np.ndarray.flatten(df1.values)

df = pd.DataFrame(arr,columns=['password'])

# formatting strings
df[['num','letter','password']] = df['password'].str.split(' ',expand=True)
df[['num1','num2']] = df['num'].str.split('-',expand=True)
df['letter'] = df['letter'].map(lambda x: x.strip(':'))

# as an example, show top 3 formatted entries
df.head(3)
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
      <th>password</th>
      <th>num</th>
      <th>letter</th>
      <th>num1</th>
      <th>num2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>qllllqllklhlvtl</td>
      <td>8-11</td>
      <td>l</td>
      <td>8</td>
      <td>11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>wmmmmmttm</td>
      <td>1-3</td>
      <td>m</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>pgppp</td>
      <td>2-4</td>
      <td>p</td>
      <td>2</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



## Part 1


```python

def isValidPassword_p1(password, num1, num2, letter):
    # counting frequency of letter in password
    freq=password.count(letter)
    # check if letter in specified range
    return (freq >= int(num1) and freq <= int(num2))

df['valid_p1']=df.apply(lambda x: isValidPassword_p1(x['password'], x['num1'], x['num2'], x['letter']), axis=1)
df['valid_p1'].value_counts()
```




    False    584
    True     416
    Name: valid_p1, dtype: int64



## Part 2


```python
def isValidPassword_p2(password, num1, num2, letter):
    # function is essentially an XNOR gate!
    l1 = (password[int(num1)-1]==letter) # check if 1st character matches
    l2 = (password[int(num2)-1]==letter) # check if 2nd character matches
    return (l1^l2)

df['valid_p2']=df.apply(lambda x: isValidPassword_p2(x['password'], x['num1'], x['num2'], x['letter']), axis=1)
df['valid_p2'].value_counts()
```




    True     688
    False    312
    Name: valid_p2, dtype: int64


