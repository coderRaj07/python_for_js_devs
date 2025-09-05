# 🐍 JavaScript to Python: A Complete Cheat Sheet for JSON, Functional Programming & Data Handling

If you're switching from JavaScript to Python or just exploring Pythonic ways to write better code — this guide will walk you through all major conversions from `JSON.stringify()` to `map()`, `filter()`, `reduce()`, and even secure data hashing.

---

## 📦 JSON Handling in Python vs JavaScript

### 🔸 `JSON.stringify()` → `json.dumps()`

Converts an object to a JSON string.

**JavaScript:**

```javascript
const obj = { name: "Rajendra", age: 25 };
const jsonString = JSON.stringify(obj);
console.log(jsonString); // '{"name":"Rajendra","age":25}'
```

**Python:**

```python
import json

obj = {"name": "Rajendra", "age": 25}
json_string = json.dumps(obj)
print(json_string)  # '{"name": "Rajendra", "age": 25}'
```

---

### 🔸 `JSON.parse()` → `json.loads()`

Parses a JSON string into an object or dict.

**JavaScript:**

```javascript
const jsonString = '{"name":"Rajendra","age":25}';
const obj = JSON.parse(jsonString);
console.log(obj.name); // Rajendra
```

**Python:**

```python
import json

json_string = '{"name": "Rajendra", "age": 25}'
obj = json.loads(json_string)
print(obj["name"])  # Rajendra
```

---

### 📁 JSON File Handling

#### 🔹 Writing JSON to a File

**JavaScript:**

```javascript
const fs = require('fs');
fs.writeFileSync('data.json', JSON.stringify(obj));
```

**Python:**

```python
with open("data.json", "w") as file:
    json.dump(obj, file)
```

---

#### 🔹 Reading JSON from a File

**JavaScript:**

```javascript
const fs = require('fs');
const obj = JSON.parse(fs.readFileSync('data.json', 'utf8'));
```

**Python:**

```python
with open("data.json", "r") as file:
    obj = json.load(file)
```

---

## 🤏 Ternary Operator

Shorthand conditional logic in one line.

**JavaScript:**

```javascript
let status = condition ? "success" : "failure";
```

**Python:**

```python
status = "success" if condition else "failure"
```

---

## 🧠 What is List Comprehension?

List comprehensions in Python are a concise way to build lists using a single line of code — combining a `for` loop and an optional `if` condition.

### 📌 Syntax:

```python
[expression for item in iterable if condition]
```

* **expression** → What to include in the list
* **item** → Variable representing each element
* **condition** (optional) → Filters which items are included

---

### 🔸 JavaScript Equivalent:

```javascript
const arr = [1, 2, 3, 4];
const evens = arr.filter(x => x % 2 === 0); // [2, 4]
```

### 🔸 Python Version:

```python
arr = [1, 2, 3, 4]
evens = [x for x in arr if x % 2 == 0]  # [2, 4]
```

✅ **List comprehensions are faster, cleaner, and more Pythonic.**

---

## 🔁 Functional Programming: `map()`, `filter()`, `reduce()`

### 🔹 `map()`

**JavaScript:**

```javascript
const doubled = [1, 2, 3].map(x => x * 2);
```

**Python:**

```python
doubled = list(map(lambda x: x * 2, [1, 2, 3]))
# or
doubled = [x * 2 for x in [1, 2, 3]]
```

---

### 🔹 `filter()`

**JavaScript:**

```javascript
const evens = [1, 2, 3, 4].filter(x => x % 2 === 0);
```

**Python:**

```python
evens = list(filter(lambda x: x % 2 == 0, [1, 2, 3, 4]))
# or
evens = [x for x in [1, 2, 3, 4] if x % 2 == 0]
```

---

### 🔹 `reduce()`

**JavaScript:**

```javascript
const sum = [1, 2, 3, 4].reduce((acc, val) => acc + val, 0);
```

**Python:**

```python
from functools import reduce
sum_result = reduce(lambda acc, val: acc + val, [1, 2, 3, 4], 0)
```

---

## 🚀 Performance Tip

List comprehensions are generally **faster** than `map()`/`filter()` with `lambda` due to internal optimizations:

```python
import timeit

arr = list(range(10000))
print(timeit.timeit(lambda: list(map(lambda x: x * 2, arr)), number=1000))
print(timeit.timeit(lambda: [x * 2 for x in arr], number=1000))
```

---

## 🧊 Using `frozenset` to Compare Dicts

Use `frozenset(dict.items())` to make dictionaries **hashable** for comparison or storing in sets:

```python
frozenset({"a": 1, "b": 2}.items())  # hashable
```

Useful for efficient uniqueness checks.

---

## 🧪 Comprehensions Overview

### List Comprehension

```python
[x for x in arr if isinstance(x, int)]
```

### Set Comprehension

```python
{item for item in arr if item > 0}
```

### Dictionary Comprehension

```python
{k: v for k, v in pairs if isinstance(v, int)}
```

---

## 🔗 Merging Lists

### Spread Operator

**JavaScript:**

```javascript
const merged = [...arr1, ...arr2];
```

**Python:**

```python
merged = [*arr1, *arr2]
```

---

### `+=` In-place Merge

**JavaScript:**

```javascript
arr1.push(...arr2);
```

**Python:**

```python
arr1 += arr2
```

✅ `+=` is faster and uses less memory.

---

## 🔒 Secure Data Hashing Example

```python
def process_secured_data(contributions):
    processed = []
    for entry in contributions:
        sub_type = entry.get("taskSubType")
        secured_data = entry.get("securedSharedData")
        hashed_data = {
            k: (
                {ik: hash_value(iv) for ik, iv in v.items()} if isinstance(v, dict)
                else [hash_value(i) for i in v] if isinstance(v, list)
                else hash_value(v)
            )
            for k, v in secured_data.items()
        }
        processed.append({"subType": sub_type, "securedSharedData": hashed_data})
    return processed
```

---

## 📚 Python Built-ins to Know
let's break down `.values()` and `.items()` in Python, including **what they are**, **when you'd use them**, and **examples** that show **why** you'd choose one over the other.

---

## 🔍 `.items()` and `.values()` in Python Dictionaries

In Python, dictionaries store data in **key-value pairs**, like this:

```python
person = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}
```

---

### 🧠 1. `.items()` → Get Key-Value Pairs

`.items()` returns all key-value pairs in the dictionary as **tuples**.

#### ✅ When to Use:

* When you need **both** keys and values.
* When looping through a dictionary.
* In **dictionary comprehensions** where you want to filter or transform.

#### 🔸 Example:

```python
for key, value in person.items():
    print(f"{key}: {value}")
```

**Output:**

```
name: Alice
age: 30
city: New York
```

#### 🔸 Dictionary comprehension example:

```python
# Filter only items where value is int
filtered = {k: v for k, v in person.items() if isinstance(v, int)}
print(filtered)  # {'age': 30}
```

---

### 🧠 2. `.values()` → Get Only Values

`.values()` returns only the values from the dictionary — no keys.

#### ✅ When to Use:

* When you only care about the values.
* When you want to **check if a value exists** in the dict.
* When you want to extract all values for processing.

#### 🔸 Example:

```python
for value in person.values():
    print(value)
```

**Output:**

```
Alice
30
New York
```

#### 🔸 Example: Check if a value exists

```python
if "Alice" in person.values():
    print("Found!")
```

---

### 📘 Comparison Summary

| Use Case                                   | Use                              |
| ------------------------------------------ | -------------------------------- |
| You want to loop over both keys and values | `.items()`                       |
| You only want to access or check values    | `.values()`                      |
| You want to transform both keys and values | `.items()` in dict comprehension |
| You want to find or filter by value only   | `.values()`                      |

---

### 🧪 Bonus: `.keys()` (for completeness)

If you only need the keys:

```python
for key in person.keys():
    print(key)
```

**Output:**

```
name
age
city
```

---

### 📌 Real-World Use Case

Imagine you're checking if a user's email is already in a user database stored like this:

```python
users = {
    "john": "john@example.com",
    "alice": "alice@example.com"
}

# Check if email exists (without caring who owns it)
if "john@example.com" in users.values():
    print("Email already used!")
```

Or if you want to log each user and their email:

```python
for username, email in users.items():
    print(f"{username}: {email}")
```

---

| Concept        | Example                 | Use                          |
| -------------- | ----------------------- | ---------------------------- |
| `.items()`     | `for k,v in d.items()`  | Iterate key-value pairs      |
| `.values()`    | `v in d.values()`       | Check if value exists        |
| `isinstance()` | `isinstance(val, list)` | Type check before operations |

---

## ✅ Final Cheat Sheet

| JavaScript               | Python                     |
| ------------------------ | -------------------------- |
| `JSON.stringify()`       | `json.dumps()`             |
| `JSON.parse()`           | `json.loads()`             |
| `array.map(fn)`          | `[fn(x) for x in arr]`     |
| `array.filter(fn)`       | `[x for x in arr if cond]` |
| `array.reduce()`         | `reduce(fn, arr, init)`    |
| `[...]` spread           | `[*arr1, *arr2]`           |
| `array1.push(...array2)` | `array1 += array2`         |
| Dict comparison          | `frozenset(dict.items())`  |

---


