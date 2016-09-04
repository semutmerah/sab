### Method Reverse String

Berasal dari salah satu kurikulum codeacademy

```
def reverse(text):
    part = []
    rvd = []
    for c in text:
        part.append(c)
    count = len(part) - 1
    while count >= 0:
        rvd.append(part[count])
        count -= 1
    return ''.join(rvd)
```
