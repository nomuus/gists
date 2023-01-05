## CaddyServer Configuration for BishopFox Sliver C2: [caddyfile_sliver_c2_public.conf](https://gist.github.com/nomuus/d10bf42cd96e2d2b12e3458054ebe5bf)
This is a @CaddyServer [Caddyfile](https://caddyserver.com/docs/caddyfile) configuration for @BishopFox [Sliver](https://github.com/BishopFox/sliver) C2 (public version). It has been derived from a private caddyfile configuration and should require only minimal modification to get started.

This caddyfile configuration is intended to function as a reverse proxy server (a.k.a. redirector) to an upstream server, i.e. Sliver server.
The configuration presumes that `/var/log/caddy/caddy.log` is writable, either by caddy as a [static binary](https://caddyserver.com/docs/install#static-binaries) or as a [system service](https://caddyserver.com/docs/running#linux-service). Installation and usage are beyond the scope of this document.

The current configuration is hard-coded for 127.0.0.1 thru 127.0.0.4 on port 8080.
The `127.0.0.x:8080` value should be changed to the respective upstream server.

It contains "anti-analysis" in that any `User-Agent` not matching that defined by [default](https://gist.github.com/nomuus/d10bf42cd96e2d2b12e3458054ebe5bf#file-caddyfile_sliver_c2_public-conf-L137) or not matching a [subset of known browsers](https://gist.github.com/nomuus/d10bf42cd96e2d2b12e3458054ebe5bf#file-caddyfile_sliver_c2_public-conf-L84) will cause `500` errors. There's also an IOC handler that can be changed to better suit an engagement.

Additional modifications are up to the discretion of the operator.

### Examples

#### Validating the caddyfile

```
caddy_linux_amd64-2-6-3 validate --config ./caddyfile_sliver_c2_public.conf --adapter caddyfile
```

Result:
```
2022/12/24 04:56:33.950	INFO	using provided configuration	{"config_file": "./caddyfile_sliver_c2_public.conf", "config_adapter": "caddyfile"}
2022/12/24 04:56:33.952	WARN	caddyfile	Unnecessary header_up X-Forwarded-Host: the reverse proxy's default behavior is to pass headers to the upstream
2022/12/24 04:56:33.952	WARN	caddyfile	Unnecessary header_up X-Forwarded-Host: the reverse proxy's default behavior is to pass headers to the upstream
2022/12/24 04:56:33.952	WARN	caddyfile	Unnecessary header_up X-Forwarded-Host: the reverse proxy's default behavior is to pass headers to the upstream
2022/12/24 04:56:33.952	WARN	caddyfile	Unnecessary header_up X-Forwarded-Host: the reverse proxy's default behavior is to pass headers to the upstream
2022/12/24 04:56:33.953	WARN	Caddyfile input is not formatted; run the 'caddy fmt' command to fix inconsistencies	{"adapter": "caddyfile", "file": "./caddyfile_sliver_c2_public.conf", "line": 3}
2022/12/24 04:56:33.954	WARN	http	server is listening only on the HTTP port, so no automatic HTTPS will be applied to this server	{"server_name": "srv0", "http_port": 80}
2022/12/24 04:56:33.955	INFO	tls.cache.maintenance	started background certificate maintenance	{"cache": "0xc0004e32d0"}
2022/12/24 04:56:33.956	INFO	tls.cache.maintenance	stopped background certificate maintenance	{"cache": "0xc0004e32d0"}
Valid configuration
```

# Copyright
Copyright (C) 2023 nomuus

[https://github.com/nomuus](https://github.com/nomuus)
