---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.13.6
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

```python
import pathlib

inputs_folder = pathlib.Path("./inputs")
```

# Day 1: Sonar Sweep
## Part 1

```python
with open(inputs_folder / "day 1" / "part 1.txt", "r", encoding="utf-8") as stream:
    data = [int(line.strip()) for line in stream]
data[:5]
```

```python
result = sum(1 for i, value in enumerate(data[1:], 1) if value > data[i-1])
print(result)
```

## Part 2

```python
rolling = [sum(data[i-2:i+1]) for i in range(2, len(data))]
result = sum(1 for i, value in enumerate(rolling[1:], 1) if value > rolling[i-1])
print(result)
```

# Day 2: Dive!
## Part 1

```python
with open(inputs_folder / "day 2" / "part 1.txt", "r", encoding="utf-8") as stream:
    data = []
    for line in stream:
        direction, value = line.strip().split(" ")
        value = int(value)
        data.append((direction, value))
```

```python
hor, dep = 0, 0
for direction, value in data:
    if direction == "forward":
        hor += value
    elif direction == "down":
        dep += value
    elif direction == "up":
        dep -= value
    else:
        raise ValueError(direction, value)
print(hor * dep)
```

## Part 2

```python
hor, dep, aim = 0, 0, 0
for direction, value in data:
    if direction == "forward":
        hor += value
        dep += aim * value
    elif direction == "down":
        aim += value
    elif direction == "up":
        aim -= value
    else:
        raise ValueError(direction, value)
print(hor * dep)
```

# Day 3: Binary Diagnostic
## Part 1

```python
with open(inputs_folder / "day 3" / "part 1.txt", "r", encoding="utf-8") as stream:
    data = list(map(lambda x: x.strip(), stream))
```

```python
size = len(data[0])
joined = "".join(data)

def find_most_common(string):
    return max(set(string), key=string.count)
```

```python
gamma_rate = int("".join([find_most_common(joined[i::size]) for i in range(size)]), 2)
epsilon_rate = (1 << size) - 1 - gamma_rate
print(gamma_rate * epsilon_rate)
```

## Part 2

```python
ogr = [*data]
for i in range(size):
    most_common = find_most_common("".join(ogr)[i::size])
    ogr = [value for value in ogr if value[i] == most_common]
    if len(ogr) == 1:
        break
ogr = ogr[0]
print(ogr)
```

```python
csr = [*data]
for i in range(size):
    most_common = find_most_common("".join(csr)[i::size])
    csr = [value for value in csr if value[i] != most_common]
    if len(csr) == 1:
        break
csr = csr[0]
print(csr)
```

```python
print(int(ogr, 2) * int(csr, 2))
```

```python

```
