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
Copyright (C) 2023 nomuus

[https://github.com/nomuus](https://github.com/nomuus)
