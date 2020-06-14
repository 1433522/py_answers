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



# 17.在 dict 类型 (class) 的各种方法 (method) 中,请列举你认为最常用的五个,并举例说明其用途、用法。


# 18.在 set 类型 (class) 的各种方法 (method) 中,请列举你认为最常用的五个,并举例说明其用途、用法。


