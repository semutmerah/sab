### Method Mengecek Bilangan Prima

Berasal dari salah satu kurikulum codeacademy

```
def is_prime(x):
    if x <= 1:
        return False
    elif x == 2:
        return True
    else:
        divider = range(2, x)
        result = []
        for i in divider:
            result.append(x % i)
        if 0 in result:
            return False
        else:
            return True
```
