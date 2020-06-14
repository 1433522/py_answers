# 16.在 list 类型 (class) 的各种方法 (method) 中,请列举你认为最常用的五个,并举例说明其用途、用法。
答：
1. 增加
- `list.append(x)`:Add an item to the end of the list.
```
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.append('watermelon')
>>> fruits
['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana', 'watermelon']
```

- `list.extend(iterable)`:Extend the list by appending all the items from the iterable. Equivalent to a[len(a):] = iterable.
```
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple']
>>> fruits.extend(('banana','watermelon'))
>>> fruits
['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana', 'watermelon']
```

- `list.insert(i, x)`:Insert an item at a given position. The first argument is the index of the element before which to insert, so a.insert(0, x) inserts at the front of the list, and a.insert(len(a), x) is equivalent to a.append(x).
```
>>> fruits
['orange', 'apple', 'banana', 'pear', 'banana', 'kiwi', 'apple']
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple']
>>> fruits.insert(2,'watermelon')
>>> fruits
['orange', 'apple', 'watermelon', 'pear', 'banana', 'kiwi', 'apple']
```

2. 删除
- `list.remove(x)`:Remove the first item from the list whose value is equal to x. It raises a ValueError if there is no such item.
```
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.remove('banana')
>>> fruits
['orange', 'apple', 'pear', 'kiwi', 'apple', 'banana']
```

- `list.pop([i])`:Remove the item at the given position in the list, and return it. If no index is specified, a.pop() removes and returns the last item in the list. (The square brackets around the i in the method signature denote that the parameter is optional, not that you should type square brackets at that position. You will see this notation frequently in the Python Library Reference.)
```
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.pop()
'banana'
>>> fruits
['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple']
>>> fruits.pop(2)
'pear'
>>> fruits
['orange', 'apple', 'banana', 'kiwi', 'apple']
```

- `list.clear()`:Remove all items from the list. Equivalent to del a[:].
```
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.clear()
>>> fruits
[]
```

3. 其他(针对现有元素进行操作）
-  `list.index(x[, start[, end]])`:Return zero-based index in the list of the first item whose value is equal to x. Raises a ValueError if there is no such item.The optional arguments start and end are interpreted as in the slice notation and are used to limit the search to a particular subsequence of the list. The returned index is computed relative to the beginning of the full sequence rather than the start argument.
```
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.index('banana')
3
>>> fruits.index('banana',4)
6
```

- `list.count(x)`:Return the number of times x appears in the list.
```
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.count('banana')
2
```

- `list.sort(key=None, reverse=False)`:Sort the items of the list in place.
```
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.sort()
>>> fruits
['apple', 'apple', 'banana', 'banana', 'kiwi', 'orange', 'pear']
```

- `list.reverse()`:Reverse the elements of the list in place.
```
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits.reverse()
>>> fruits
['banana', 'apple', 'kiwi', 'banana', 'pear', 'apple', 'orange']
```

- `list.copy()`:Return a shallow copy of the list. Equivalent to a[:].
```
>>> fruits = ['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> fruits_copy = fruits.copy()
>>> fruits_copy
['orange', 'apple', 'pear', 'banana', 'kiwi', 'apple', 'banana']
>>> id(fruits)
140434694954752
>>> id(fruits_copy)
140434678939472
```

# 17.在 dict 类型 (class) 的各种方法 (method) 中,请列举你认为最常用的五个,并举例说明其用途、用法。
答：
1. 增加
- `setdefault(key[, default])`:If key is in the dictionary, return its value. If not, insert key with a value of default and return default. default defaults to None.
```
>>> tel = {'jack': 4098, 'sape': 4139,'guido': 4127}
>>> tel.setdefault('alex')
>>> tel
{'jack': 4098, 'sape': 4139, 'guido': 4127, 'alex': None}
>>> tel.setdefault('john',1111)
1111
>>> tel
{'jack': 4098, 'sape': 4139, 'guido': 4127, 'alex': None, 'john': 1111}
```

- `update([other])`:Update the dictionary with the key/value pairs from other, overwriting existing keys. Return None.
改
```
>>> tel = {'jack': 4098, 'sape': 4139,'guido': 4127}
>>> tel.update('jack'=4000,'alex'=1234,'john'=1111)
>>> tel.update(jack=4000,alex=1234,john=1111)
>>> tel
{'jack': 4000, 'sape': 4139, 'guido': 4127, 'alex': 1234, 'john': 1111}
```
2. 删除
- `pop(key[, default])`:If key is in the dictionary, remove it and return its value, else return default. If default is not given and key is not in the dictionary, a KeyError is raised.
```
>>> tel = {'jack': 4098, 'sape': 4139,'guido': 4127}
>>> tel.pop('jack')
4098
>>> tel
{'sape': 4139, 'guido': 4127}
```

- `popitem()`:Remove and return a (key, value) pair from the dictionary. Pairs are returned in LIFO order.
```
>>> tel = {'jack': 4098, 'sape': 4139,'guido': 4127}
>>> tel.popitem()
('guido', 4127)
>>> tel
{'jack': 4098, 'sape': 4139}
```

- `clear()`:Remove all items from the dictionary.
```
>>> tel = {'jack': 4098, 'sape': 4139,'guido': 4127}
>>> tel.clear()
>>> tel
{}
```

3. 其他
- `copy()`:Return a shallow copy of the dictionary.
```
>>> tel = {'jack': 4098, 'sape': 4139,'guido': 4127}
>>> tel_cp = tel.copy()
>>> id(tel)
140434677843200
>>> id(tel_cp)
140434677965120
```

- `get(key[, default])`:Return the value for key if key is in the dictionary, else default. If default is not given, it defaults to None, so that this method never raises a KeyError.
```
>>> tel = {'jack': 4098, 'sape': 4139,'guido': 4127}
>>> tel.get('jack')
4098
```

- `keys()`:Return a new view of the dictionary’s keys.
```
>>> tel = {'jack': 4098, 'sape': 4139,'guido': 4127}
>>> tel.keys()
dict_keys(['jack', 'sape', 'guido'])
```

- `values()`:Return a new view of the dictionary’s values. 
```
>>> tel = {'jack': 4098, 'sape': 4139,'guido': 4127}
>>> tel.values()
dict_values([4098, 4139, 4127])
```

- `items()`:Return a new view of the dictionary’s items ((key, value) pairs).
```
>>> tel = {'jack': 4098, 'sape': 4139,'guido': 4127}
>>> tel.items()
dict_items([('jack', 4098), ('sape', 4139), ('guido', 4127)])
```

# 18.在 set 类型 (class) 的各种方法 (method) 中,请列举你认为最常用的五个,并举例说明其用途、用法。
答：
1. 增加
- `add()`:Add an element to a set.
```
>>> a = set("hello")
>>> a
{'h', 'l', 'o', 'e'}
>>> a.add('x')
>>> a
{'h', 'x', 'o', 'e', 'l'}
```
2. 删除
- `clear()`:Remove all elements from this set.
```
>>> a = set("hello")
>>> a
{'h', 'l', 'o', 'e'}
>>> a.clear()
>>> a
set()
```

- `discard()`: Remove an element from a set if it is a member.If the element is not a member, do nothing.
```
>>> a = set("hello")
>>> a.discard('h')
>>> a
{'l', 'o', 'e'}
```

3. 集合操作
-  `difference()`: Return the difference of two or more sets as a new set.
```
>>> a = set("hello")
>>> b = set("world")
>>> a - b
{'h', 'e'}
>>> a.difference(b)
{'h', 'e'}
```

- `intersection()`:Return the intersection of two or more sets as a new set.
```
>>> a = set("hello")
>>> b = set("world")
>>> a.intersection(b)
{'o', 'l'}
>>> a & b
{'o', 'l'}
```

- `union()`:Return the union of sets as a new set.
```
>>> a = set("hello")
>>> b = set("world")
>>> a.union(b)
{'h', 'w', 'o', 'e', 'd', 'r', 'l'}
>>> a | b
{'h', 'w', 'o', 'e', 'd', 'r', 'l'}
```

- `symmetric_difference()`: Return the symmetric difference of two sets as a new set.
```
>>> a = set("hello")
>>> b = set("world")
>>> a.symmetric_difference(b)
{'h', 'd', 'w', 'r', 'e'}
>>> a ^ b
{'h', 'd', 'w', 'r', 'e'}
```

