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

```python

```
