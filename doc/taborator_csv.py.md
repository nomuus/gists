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

# Copyright
Copyright (C) 2023 nomuus

[https://github.com/nomuus](https://github.com/nomuus)
