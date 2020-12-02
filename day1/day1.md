# Day 1


```python
import pandas as pd

df1 = pd.read_csv("input.txt", header=None)
arr=df1.values
```

## Part 1


```python
def getPairs(arr, sum): 
    n = len(arr)

    # Cycle through all pairs and check sum 
    for i in range(0, n): 
        for j in range(i + 1, n): 
            if arr[i] + arr[j] == sum: 
                ans1=arr[i]
                ans2=arr[j]
                print(arr[i],arr[j])

    return ans1,ans2

ans1,ans2=getPairs(arr,2020)
print(ans1*ans2)
```

    [1124] [896]
    [1007104]
    

## Part 2

Three entries


```python
import numpy as np

arr1=np.ndarray.flatten(arr)
arr1.sort()
arr1
```




    array([  24,  465,  539,  812,  896, 1124, 1149, 1207, 1215, 1217, 1222,
           1224, 1225, 1232, 1234, 1237, 1240, 1241, 1252, 1270, 1271, 1279,
           1280, 1284, 1299, 1301, 1304, 1317, 1329, 1330, 1331, 1338, 1343,
           1360, 1365, 1369, 1371, 1372, 1376, 1379, 1381, 1383, 1384, 1386,
           1388, 1389, 1394, 1395, 1397, 1400, 1410, 1417, 1419, 1422, 1427,
           1429, 1434, 1435, 1441, 1442, 1443, 1453, 1457, 1458, 1462, 1469,
           1470, 1473, 1484, 1487, 1490, 1494, 1502, 1505, 1510, 1515, 1524,
           1528, 1536, 1539, 1541, 1544, 1546, 1548, 1551, 1554, 1562, 1566,
           1572, 1582, 1585, 1586, 1589, 1592, 1593, 1597, 1602, 1610, 1615,
           1616, 1619, 1625, 1626, 1629, 1630, 1631, 1632, 1637, 1638, 1647,
           1652, 1658, 1675, 1676, 1688, 1691, 1692, 1697, 1700, 1705, 1707,
           1710, 1711, 1712, 1713, 1720, 1721, 1723, 1736, 1737, 1739, 1741,
           1744, 1745, 1748, 1751, 1752, 1753, 1754, 1758, 1769, 1778, 1780,
           1788, 1792, 1794, 1795, 1800, 1804, 1805, 1815, 1817, 1821, 1823,
           1825, 1829, 1836, 1856, 1857, 1868, 1883, 1884, 1885, 1888, 1892,
           1896, 1902, 1908, 1911, 1915, 1922, 1932, 1933, 1934, 1941, 1948,
           1950, 1955, 1956, 1958, 1963, 1966, 1968, 1974, 1975, 1976, 1977,
           1979, 1980, 1982, 1983, 1988, 1994, 2001, 2003, 2005, 2006, 2008,
           2009, 2010], dtype=int64)




```python
def getTriplet(arr, sum): 
    n = len(arr)
    
    arr.sort() # sort from lowest to highest, fix first element
    
    for i in range(0, n-2): 
        l = i + 1 # left is one after locked value
          
        r = n-1 # right is end of array
        while (l < r): 
            if( arr[i] + arr[l] + arr[r] == sum): 
                print(arr[i], arr[l], arr[r])
                return arr[i], arr[l], arr[r]

            # if less than sum, move to a larger number (left move)
            elif (arr[i] + arr[l] + arr[r] < sum): 
                l += 1
            # if more than sum, move to a smaller number (right move)
            else: # A[i] + A[l] + A[r] > sum 
                r -= 1
  
    # rip no triplet shrugs
    return 0,0,0

ans1,ans2,ans3=getTriplet(arr1,2020)
print(ans1*ans2*ans3)
```

    24 539 1457
    18847752
    
