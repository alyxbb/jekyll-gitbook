# More on Lists

{% embed url="https://www.youtube.com/watch?index=8&list=PLKb_ndRMEWN9LzbKCy4R-5YtI4GoMzCgd&v=u6e7wKVbu8E" %}

## The `in` operator

The `in` operator seen for strings also works on lists.

```bash
>>> cheeses = ['Cheddar', 'Edam', 'Gouda'] 
>>> 'Edam' in cheeses
 True 
>>> 'Brie' in cheeses
 False 
>>>
```

## Traversing a list

The most common way to traverse the elements of a list is with a `for` loop. The syntax is the same as for strings:

{% code lineNumbers="true" %}
```python
for cheese in cheeses: 
    print(cheese)
```
{% endcode %}

This works well if you only need to read the elements of the list. But if you want to write or update the elements, you need the indices. A common way to do that is to combine the functions `range` and `len`:

{% code lineNumbers="true" %}
```python
for i in range(len(numbers)): 
    numbers[i] = numbers[i] * 2
```
{% endcode %}

This loop traverses the list and updates each element. `len` returns the number of elements in the list. `range` returns a list of indices from `0` to `n-1`, where `n` is the length of the list. Each time through the loop `i` gets the index of the next element. The assignment statement in the body uses `i` to read the old value of the element and to assign the new value.

A `for` loop over an empty list never executes the body:

{% code lineNumbers="true" %}
```python
for x in []: 
    print('This never happens.') 
```
{% endcode %}

Although a list can contain another list, the nested list still counts as a single element. The length of the list `['spam', 1, ['Brie', 'Roquefort', 'Pol le Veq'], [1, 2, 3]]` is four.

## List operations

The `+` operator concatenates lists:

```bash
>>> a = [1, 2, 3] 
>>> b = [4, 5, 6] 
>>> c = a + b 
>>> print(c)
 [1, 2, 3, 4, 5, 6] 
>>>
```

Similarly, the `*` operator repeats a list a given number of times:

```bash
>>> [0] * 4 
 [0, 0, 0, 0] 
>>> [1, 2, 3] * 3 
[1, 2, 3, 1, 2, 3, 1, 2, 3] 
>>>
```

The first example repeats `[0]` four times. The second example repeats the list `[1, 2, 3]` three times.

## List methods

Python provides methods that operate on lists. For example, `append` adds a new element to the end of a list:

```bash
>>> t = ['a', 'b', 'c'] 
>>> t.append('d')
>>> print(t)
 ['a', 'b', 'c', 'd'] 
>>>
```

`extend` takes a list as an argument and appends all of the elements:

```bash
>>> t1 = ['a', 'b', 'c']
>>> t2 = ['d', 'e']
>>> t1.extend(t2)
>>> print(t1)
 ['a', 'b', 'c', 'd', 'e']
>>>
```

This example leaves `t2` unmodified.

`sort` arranges the elements of the list from low to high:

```
>>> t = ['d', 'c', 'e', 'b', 'a']
>>> t.sort()
>>> print(t)
 ['a', 'b', 'c', 'd', 'e']
>>>
```

List methods are all void; they modify the list and return `None`. If you accidentally write\
`t = t.sort()`, you will be disappointed with the result.

## Map, filter and reduce

To add up all the numbers in a list, you can use a loop like this:

{% code lineNumbers="true" %}
```python
def add_all(a_list): 
    total = 0 
    for val in a_list: 
        total += val 
    return total
```
{% endcode %}

`total` is initialized to `0`. Each time through the loop, `x` gets one element from the list. The `+=` operator provides a short way to update a variable. This **augmented assignment statement**:

```python
total += val

```

is equivalent to:

```python
total = total + val
```

As the loop executes, `total` accumulates the sum of the elements; a variable used this way is sometimes called an **accumulator**. Adding up the elements of a list is such a common operation that Python provides it as a built-in function, `sum`:

```bash
>>> t = [1, 2, 3] 
>> sum(t)
 6
>>> 
```

An operation like this that combines a sequence of elements into a single value is sometimes called **reduce**. Sometimes you want to traverse one list while building another. For example, the following function takes a list of strings and returns a new list that contains capitalised strings:

{% code lineNumbers="true" %}
```python
def capitalise_all(word): 
    result = [] 
    for letter in word: 
        result.append(letter.capitalize()) 
    return result 
```
{% endcode %}

`result` is initialised with an empty list; each time through the loop, we append the next element. So `result` is another kind of accumulator. An operation like `capitalise_all` is sometimes called a **map** because it "maps" a function (in this case the method `capitalize`) onto each of the elements in a sequence.

Another common operation is to select some of the elements from a list and return a sublist. For example, the following function takes a list of strings and returns a list that contains only the uppercase strings:

{% code lineNumbers="true" %}
```python
def only_upper(word): 
    result = [] 
    for letter in word: 
        if letter.isupper(): 
            result.append(letter) 
    return result
```
{% endcode %}

`isupper` is a string method that returns `True` if the string contains only upper case letters. An operation like "only\_upper" is called a **filter** because it selects some of the elements and filters out the others.

Most common list operations can be expressed as a combination of map, filter and reduce. Because these operations are so common, Python provides language features to support them, including the built-in function `map` and an operator called a **comprehension**.

**Exercise:** Write a function `cumulative_sum` that takes a list of numbers and returns the cumulative sum; that is, a new list where the $$i^{th}$$ element is the sum of the first $$i+1$$ elements from the original list. For example, the cumulative sum of `[1, 2, 3]` is `[1, 3, 6]`.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def cumulative_sum(elements):
    if elements is []:
        return []
    cumulative = 0
    cumulative_list = []
    for elt in elements:
        cumulative += elt
        cumulative_list.append(cumulative)
    return cumulative_list
```
{% endcode %}

</details>

## Deleting elements

There are several ways to delete elements from a list. If you know the index of the element you want, you can use `pop`:

```bash
>>> t = ['a', 'b', 'c'] 
>>> x = t.pop(1) 
>>> print(t)
 ['a', 'c'] 
>>> print(x)
 b
>>> 
```

`pop` modifies the list and returns the element that was removed. If you don't provide an index, it deletes and returns the last element. If you don't need the removed value, you can use the `del` operator:

```bash
>>> t = ['a', 'b', 'c']
>>> del t[1] 
>>> print(t) 
 ['a', 'c']
>>>
```

If you know the element you want to remove (but not the index), you can use `remove`:

```bash
>>> t = ['a', 'b', 'c']
>>> t.remove('b')
>>> print(t)
 ['a', 'c'] 
>>>
```

The return value from `remove` is `None`. To remove more than one element, you can use del with a slice index:

```bash
>>> t = ['a', 'b', 'c', 'd', 'e', 'f']
>>> del t[1:5]
>>> print(t)
 ['a', 'f'] 
>>>
```

As usual, the slice selects all the elements up to, but not including, the second index.

## Sorting a list

The `sorted()` function in Python is a built-in function that sorts the elements of a given iterable in a specific order (ascending or descending) and returns it as a list. The `sorted()` function takes two optional parameters:

* `reverse`: A boolean value that specifies whether the list should be sorted in descending order (`True`) or ascending order (`False`). The default value is `False`.
* `key`: A function that takes a single element from the iterable as input and returns a value that will be used to sort the element. This allows you to sort the iterable based on a custom criteria.

The `sorted()` function can be used to sort any iterable object, such as lists, tuples, strings, and dictionaries. For example, the following code sorts a list of numbers in ascending order:

```bash
>>> numbers = [10, 5, 2, 3, 1]
>>> sorted_numbers = sorted(numbers)
>>> print(sorted_numbers)
 [1, 2, 3, 5, 10]
>>>
```

We can also sort a list in descending order using the key parameter `reverse`:

```bash
>>> numbers = [2, 10, 5, 3, 1]
>>> sorted_numbers = sorted(numbers, reverse=True)
>>> print(sorted_numbers)
 [10, 5, 3, 2, 1]
>>>
```

The `sorted()` function can also be used to sort a list of strings in alphabetical order:

```bash
>>> strings = ["hello", "world", "python", "programming"]
>>> sorted_strings = sorted(strings)
>>> print(sorted_strings)
 ['hello', 'python', 'programming', 'world']
>>>
```

The `sorted()` function is a powerful tool that can be used to sort any iterable object in a variety of ways. It is a versatile function that can be used in a variety of programming tasks. We will revisit the function later in the book when we have learned the concept of **lambda functions**.

## Lists and strings

A string is a sequence of characters and a list is a sequence of values, but a list of characters is not the same as a string. To convert from a string to a list of characters, you can use `list`:

```bash
>>> s = 'spam'
>>> letters = list(s)
>>> print(letters)
 ['s', 'p', 'a', 'm']
>>> 
```

Because `list` is the name of a built-in function, you should avoid using it as a variable name. I also avoid `l` because it looks too much like `1` on some fonts. So that's why I use `letters` instead.

The `list` function breaks a string into individual letters. If you want to break a string into words, you can use the `split` method:

```bash
>>> s = 'pining for the fjords'
>>> t = s.split()
>>> print(t)
 ['pining', 'for', 'the', 'fjords']
>>>
```

An optional argument called a **delimiter** specifies which characters to use as word boundaries. The following example uses a hyphen as a delimiter:

```bash
>>> s = 'spam-spam-spam'
>>> delimiter = '-'
>>> s.split(delimiter)
 ['spam', 'spam', 'spam']
>>>
```

`join` is the inverse of `split`. It takes a list of strings and concatenates the elements. `join` is a string method, so you have to invoke it on the delimiter and pass the list as a parameter:

```bash
>>> t = ['pining', 'for', 'the', 'fjords']
>>> delimiter = '-'
>>> delimiter.join(t)
 'pining-for-the-fjords'
>>>
```

In this case the delimiter is a space character, so `join` puts a '-' between words. To concatenate strings without delimiters, you can use the empty string, `''`, as a delimiter.

## Objects and values

If we execute these assignment statements:

```bash
>>> a = 'banana'
>>> b = 'banana'
```

We know that `a` and `b` both refer to a string, but we don't know whether they refer to the **same** string. There are two possible states:

<figure><img src="../.gitbook/assets/list1.png" alt="" width="375"><figcaption><p>The two possible states for the variable <code>a</code> and <code>b</code>.</p></figcaption></figure>

In one case, `a` and `b` refer to two different objects that have the same value. In the second case, they refer to the same object. To check whether two variables refer to the same object, you can use the `is` operator.

```bash
>>> a = 'banana'
>>> b = 'banana'
>>> a is b
 True 
>>
```

In this example, Python only created one string object, and both `a` and `b` refer to it. But when you create two lists, you get two objects:

```bash
>>> a = [1, 2, 3]
>>> b = [1, 2, 3]
>>> a is b
 False 
>>>
```

So the state diagram looks like this:

<figure><img src="../.gitbook/assets/list2.png" alt="" width="152"><figcaption><p>State diagram for the variable <code>a</code> and <code>b</code>.</p></figcaption></figure>

In this case we would say that the two lists are **equivalent**, because they have the same elements, but not **identical**, because they are not the same object. If two objects are identical, they are also equivalent, but if they are equivalent, they are not necessarily identical.

Until now, we have been using "object and value" interchangeably, but it is more precise to say that an object has a value. If you execute `[1,2,3]`, you get a list object whose value is a sequence of integers. If another list has the same elements, we say it has the same value, but it is not the same object.

## Aliasing

If `a` refers to an object and you assign `b = a`, then both variables refer to the same object:

```bash
>>> a = [1, 2, 3]
>>> b = a
>>> b is a
 True 
>>>
```

The state diagram looks like this:

<figure><img src="../.gitbook/assets/list3.png" alt="" width="152"><figcaption><p>State diagram representing two references (<code>a</code> and <code>b</code>) <br>to the same object <code>[1,2,3]</code>. </p></figcaption></figure>

The association of a variable with an object is called a `reference`. In this example, there are two references to the same object. An object with more than one reference has more than one name, so we say that the object is **aliased**.

If the aliased object is mutable, changes made with one alias affect the other:

```bash
>>> b[0] = 17
>>> print(b)
[17, 2, 3]
>>> print(a) 
 [17, 2, 3]
>>> 
```

Although this behaviour can be useful, it is error-prone. In general, it is safer to avoid aliasing when you are working with mutable objects.

For immutable objects like strings, aliasing is not as much of a problem. In this example:

```
>>> a = 'banana'
>>> b = 'banana' 
```

It almost never makes a difference whether `a` and `b` refer to the same string or not.

Certainly! Let's explore list comprehension in Python.

## **List Comprehension in Python**

List comprehension is a concise and powerful way to create lists in Python. It allows you to generate new lists by applying an expression to each item in an existing iterable (such as a list, tuple, or range) and optionally filtering the items based on a condition. The result is a new list that often requires fewer lines of code compared to traditional for loops.

Here's the basic syntax of a list comprehension:

```python
new_list = [expression for item in iterable if condition]
```

* `expression` is the operation to perform on each item.
* `item` represents the current item in the iterable.
* `iterable` is the source of data (e.g., a list or range).
* `condition` (optional) filters the items based on a specified condition.

### **Examples of List Comprehension**

1.  **Creating a List of Squares**:

    {% code lineNumbers="true" %}
    ```python
    numbers = [1, 2, 3, 4, 5]
    squares = [x**2 for x in numbers]
    # squares will be [1, 4, 9, 16, 25]
    ```
    {% endcode %}
2.  **Filtering Even Numbers**:

    {% code lineNumbers="true" %}
    ```python
    numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    evens = [x for x in numbers if x % 2 == 0]
    # evens will be [2, 4, 6, 8, 10]
    ```
    {% endcode %}
3.  **Creating a List of Combinations**:

    {% code lineNumbers="true" %}
    ```python
    colours = ['red', 'green', 'blue']
    combinations = [(a, b) for a in colours for b in colours if a != b]
    # combinations will be [('red', 'green'), ('red', 'blue'), ('green', 'red'), 
    # ('green', 'blue'), ('blue', 'red'), ('blue', 'green')]
    ```
    {% endcode %}
4.  **Working with Strings**:

    {% code lineNumbers="true" %}
    ```python
    words = ['Bonjour', 'le', 'monde']
    capitalised = [word.upper() for word in words]
    # capitalised will be ['BONJOUR', 'LE', 'MONDE']
    ```
    {% endcode %}

List comprehensions are not only concise but also efficient, making them a favourite among Python developers for tasks like data transformation and filtering. They improve code readability and help you write Pythonic, elegant code. However, for more complex operations, it's essential to strike a balance between brevity and clarity to maintain code maintainability.

## List arguments

When you pass a list to a function, the function gets a reference to the list. If the function modifies a list parameter, the caller sees the change. For example, `delete_head` removes the first element from a list:

{% code lineNumbers="true" %}
```python
def delete_head(lst): 
    del lst[0] 
```
{% endcode %}

Here's how it is used:

```bash
>>> letters = ['a', 'b', 'c']
>>> delete_head(letters)
>>> print (letters)
 ['b', 'c'] 
>>>
```

The parameter `lst` and the variable `letters` are aliases for the same object. The stack diagram looks like this:

<figure><img src="../.gitbook/assets/stack5.png" alt="" width="366"><figcaption><p>State diagram of a mutable object passed in the parameters of a function.</p></figcaption></figure>

Since the list is shared by two frames, I drew it between them.

It is important to distinguish between operations that modify lists and operations that create new lists. For example, the `append` method modifies a list, but the `+` operator creates a new list:

```bash
>>> t1 = [1, 2]
>>> t2 = t1.append(3)
>>> print(t1)
 [1, 2, 3]
>>> print(t2)
 None
>>> t1 = [1, 2]
>>> t3 = t1 + [3]
>>> print (t3)
 [1, 2, 3]
>>> t2 is t3
 False 
>>>
```

This difference is important when you write functions that are supposed to modify lists. For example, this function _does not_ delete the head of a list:

{% code lineNumbers="true" %}
```python
def bad_delete_head(t): 
    t = t[1:] # WRONG!
```
{% endcode %}

The slice operator creates a new list and the assignment makes `t` refer to it, but none of that has any effect on the list that was passed as an argument.

An alternative is to write a function that creates and returns a new list. For example, `tail` shown below returns all but the first element of a list:

{% code lineNumbers="true" %}
```python
def tail(t): 
    return t[1:]
```
{% endcode %}

This function leaves the original list unmodified. Here's how it is used:

```bash
>>> letters = ['a', 'b', 'c']
>>> rest = tail(letters)
>>> print(rest)
 ['b', 'c']
>>>
```

**Exercise:** Write a function called `chop` that takes a list as parameter and modifies it, removing the first and last elements, and returns `None`. Then write a function called `middle` that takes a list and returns a new list that contains all but the first and last elements.

<details>

<summary>Answer</summary>

{% code lineNumbers="true" %}
```python
def chop(elements):
    del elements[0]
    del elements[-1]

def middle(elements):
    return elements[1:-1]  
```
{% endcode %}

Alternatively, we could use the `pop` method from the list object:

{% code lineNumbers="true" %}
```python
def chop_with_pop(elements):
    elements.pop(0)
    elements.pop()
```
{% endcode %}

</details>
