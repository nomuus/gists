```
  n     o     m      
   \ '  |  ' /       
@   \ ' | ' /   #    //////////// https://github.com/nomuus/gists
 `.  \ .|, /  .`     
~. `. \ G / .` ,~     ..|'''.|  '||'  .|'''.|  |''||''|  .|'''.|  
  `'.`.\I/,`.'`      .|'     '   ||   ||..  '     ||     ||..  '  
*- - .`,S',`.- -*    ||    ....  ||    ''|||.     ||      ''|||.  
 , ' .`/T\`. ' ,     '|.    ||   ||  .     '||    ||    .     '|| 
"  .` / S \ `.  ^     ''|...'|  .||. |'....|'    .||.   |'....|'  
 .`  / `|` \  `.     
?   / ' | ' \   `!   ///////////// https://gist.github.com/nomuus
   / '  |  ' \       
  u     u     s      
```

# Gists

This repository provides a central reference point for @nomuus [gist created on Github](https://gist.github.com/nomuus):

- [Taborator to CSV](https://github.com/nomuus/gists#taborator-to-csv-taborator_csvpy)
- [Zoom Debian Install Helper](https://github.com/nomuus/gists#zoom-debian-install-helper-install_zoom_debiansh)
- [String Meta-Data](https://github.com/nomuus/gists#string-meta-data-meta-string-datapy)
- [HTTP Header to JSON](https://github.com/nomuus/gists#http-header-to-json-http-header-to-jsonpy)

See individual gist  and respective comments for further details or license if applicable.

---

## Taborator to CSV: [taborator_csv.py](https://gist.github.com/nomuus/e3e6dd7019b3b4a23c7f64600c3384e4#file-taborator_csv-py)
Converts exported data from @PortSwigger [Burp Suite Taborator extension](https://github.com/PortSwigger/taborator) by @hackvertor ([origin](https://github.com/hackvertor/taborator)) to CSV.

### Example

#### Convert and decode exported JSON data to UNIX-style CSV

`python3 taborator_csv.py --out-format=unix --decode export.json`
```
"id","client_ip","hostname","interaction_id","interaction_type","protocol","query_type","raw_query","request","response","time_stamp","type","comment"
"1","127.0.0.1","dbbcd142850bf4eb73af336f58234a.example.com","dbbcd142850bf4eb73af336f58234a","collaborator","","A","b'!\x10\x00\x00\x00\x01\x00\x00\x00\x00\x00\x00\x1edbbcd142850bf4eb73af336f58234a\x07example\x03com\x00\x00\x01\x00\x01'","","","2022-Aug-08 23:23:31 UTC","DNS","this is a comment"
"2","127.0.0.1","dbbcd142850bf4eb73af336f58234a.example.com","dbbcd142850bf4eb73af336f58234a","collaborator","","AAAA","b'\xd2-\x00\x00\x00\x01\x00\x00\x00\x00\x00\x00\x1edbbcd142850bf4eb73af336f58234a\x07example\x03com\x00\x00\x1c\x00\x01'","","","2022-Aug-08 23:23:31 UTC","DNS","this is a comment"
```

## Zoom Debian Install Helper: [install_zoom_debian.sh](https://gist.github.com/nomuus/777152e79f4a8bc176fcded05bd10d26#file-install_zoom_debian-sh)
Downloads and installs the latest @Zoom [Linux client and dependencies](https://support.zoom.us/hc/en-us/articles/204206269-Installing-or-updating-Zoom-on-Linux) on Debian-based Linux operating systems.

### Example

#### Download and install @Zoom client in a @QubesOS disposable VM

`[user@disp1234 ~]$` ```sudo bash install_zoom_debian.sh```

Result:
```
...
    [output of apt]
    [latest version saved as zoom_$LATEST_ZOOM_VERSION.deb]
...

```

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


## HTTP Header to JSON: [http-header-to-json.py](https://gist.github.com/nomuus/93b31dc3e790116c82e951e5e741a048#file-http-header-to-json-py)
Embeddable Python one-liner to convert HTTP Headers from stdin to JSON on stdout.

### Examples

##### Converting `wget` output from `example.com` to JSON string

```
wget -q --server-response --method HEAD https://www.example.com 2>&1 | python3 http-header-to-json.py
```

Result:
```
{"Content-Encoding": "gzip", "Accept-Ranges": "bytes", "Age": "595653", "Cache-Control": "max-age=604800", "Content-Type": "text/html; charset=UTF-8", "Date": "Fri, 22 Jul 2022 00:53:13 GMT", "Etag": "\"3147526947\"", "Expires": "Fri, 29 Jul 2022 00:53:13 GMT", "Last-Modified": "Thu, 17 Oct 2019 07:18:26 GMT", "Server": "ECS (agb/A445)", "X-Cache": "HIT", "Content-Length": "648"}
```

#### Getting latest version of @SlackHQ [Nebula](https://github.com/slackhq/nebula) using embeddable one-line string and parsing with [jq](https://github.com/stedolan/jq)

```
LATEST_NEBULA_VERSION=$(wget -q --server-response --method HEAD https://github.com/slackhq/nebula/releases/latest/  2>&1 | python3 -c "print((lambda sys=__import__('sys'), json=__import__('json'): json.dumps(dict(list(map(lambda t: (t[0], t[2]), filter(all, [line.strip('\r\n\t ').partition(': ') for line in iter(sys.stdin.readline, '')])))) if not sys.stdin.isatty() else {}))())" | jq -r '.Location' | sed 's/.*\///g'); [ ! -z $LATEST_NEBULA_VERSION ] &&  wget https://github.com/slackhq/nebula/releases/download/$LATEST_NEBULA_VERSION/nebula-linux-amd64.tar.gz -O nebula-$LATEST_NEBULA_VERSION.tar.gz
```


# Copyright
Copyright (C) 2022 nomuus

[https://github.com/nomuus](https://github.com/nomuus)
