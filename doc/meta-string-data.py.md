## String Meta-Data: [meta-string-data.py](https://gist.github.com/nomuus/b95ad1417d8d3ec68adc2b6a37efe999#file-meta-string-data-py)
Embeddable Python one-liner to output string metadata from stdin to JSON on stdout.

### Examples

#### Show the meta-data on password strings using Python-file containing embeddable one-line string

`printf "Password123@\nPassword_123\n" | python3 meta-string-data.py`

Result:
```
{"digit": 3, "upper": 1, "lower": 7, "punct": 1, "other": 0}
{"digit": 3, "upper": 1, "lower": 7, "punct": 1, "other": 0}
```

#### Show the meta-data on password strings using embeddable one-line string

`printf "Password123@\nPassword_123\n" | python3 -c "(lambda sys=__import__('sys'), json=__import__('json'): list(filter(lambda s: print(json.dumps((lambda _k=['digit','upper','lower','punct','other'], _v=[0,0,0,0,0]: dict(tuple(zip(_k, _v))) if all(map(lambda c: all((_v.__setitem__(0, _v[0].__add__(int(c.isdigit()))) or True, _v.__setitem__(1, _v[1].__add__(int(c.isupper()))) or True, _v.__setitem__(2, _v[2].__add__(int(c.islower()))) or True, _v.__setitem__(3, _v[3].__add__(int((ord(c) >= 33 and ord(c) <= 47) or (ord(c) >= 58 and ord(c) <= 64) or (ord(c) >= 91 and ord(c) <= 96) or (ord(c) >= 123 and ord(c) <= 126)))) or True, _v.__setitem__(4, _v[4].__add__(int((ord(c) >= 0 and ord(c) <= 32) or (ord(c) >= 127)))) or True)), s.rstrip('\r\n'))) else dict(tuple(zip(_k, _v))))())) is not None, iter(sys.stdin.readline, ''))) if not sys.stdin.isatty() else {})()"`

Result:
```
{"digit": 3, "upper": 1, "lower": 7, "punct": 1, "other": 0}
{"digit": 3, "upper": 1, "lower": 7, "punct": 1, "other": 0}
```

#### Show the meta-data on [best 15 common credentials](https://github.com/danielmiessler/SecLists/blob/master/Passwords/Common-Credentials/best15.txt) compiled by @danielmiessler

`cat best15.txt | python3 meta-string-data.py`

Result:
```
{"digit": 6, "upper": 0, "lower": 0, "punct": 0, "other": 0}
{"digit": 4, "upper": 0, "lower": 0, "punct": 0, "other": 0}
{"digit": 5, "upper": 0, "lower": 0, "punct": 0, "other": 0}
{"digit": 6, "upper": 0, "lower": 0, "punct": 0, "other": 0}
{"digit": 7, "upper": 0, "lower": 0, "punct": 0, "other": 0}
{"digit": 8, "upper": 0, "lower": 0, "punct": 0, "other": 0}
{"digit": 3, "upper": 0, "lower": 3, "punct": 0, "other": 0}
{"digit": 0, "upper": 0, "lower": 6, "punct": 0, "other": 0}
{"digit": 0, "upper": 0, "lower": 8, "punct": 0, "other": 0}
{"digit": 0, "upper": 0, "lower": 7, "punct": 0, "other": 0}
{"digit": 0, "upper": 0, "lower": 6, "punct": 0, "other": 0}
{"digit": 0, "upper": 0, "lower": 8, "punct": 0, "other": 0}
{"digit": 0, "upper": 0, "lower": 6, "punct": 0, "other": 0}
{"digit": 0, "upper": 0, "lower": 8, "punct": 0, "other": 0}
{"digit": 0, "upper": 0, "lower": 4, "punct": 0, "other": 0}
```

# Copyright
Copyright (C) 2023 nomuus

[https://github.com/nomuus](https://github.com/nomuus)
