### Method remove duplicates

Berasal dari salah satu kurikulum codeacademy

```
def remove_duplicates(numbers):
    single = []
    for n in numbers:
        if n not in single:
            single.append(n)
    return single
```
