# Tool: httpver_scan
This is a tool (written in Python) to perform quick scan on HTTP server.

It's features include:
 - scan spcific URL
 - scan a list of sites from an input file
 - allow to follow [301] redirection
 - always make async connections

# Usage
```bash
$ ./httpver_scan.py -h
usage: httpver_scan.py [-h] [-u <url> [<url> ...]] [-f <sites.url>] [-r] [-v]

options:
  -h, --help            show this help message and exit
  -u <url> [<url> ...]  Specifying URL
  -f <sites.url>        Specifying input site file
  -r                    Follow HTTP 301 redirection.
  -v                    verbose output
```

## Samples
Below is the sample output where [301] redirection is not followed:

```console
 [*] Scanning [7] sites...

           URLs                            Protocols           Server                    Time / Total      Content
==================================================================================================================
     [  1] https://requestbin.com/         r_0 [307] HTTP/2    s:CloudFront              [0.1506]/[0.1510] ~0.0kb
     [  2] https://nghttp2.org/            r_0 [200] HTTP/2    s:nghttpx                 [0.3011]/[0.3014] ~6.2kb
     [  3] http://www.isc2.org/            r_0 [301] HTTP/1.0  s:                        [0.0905]/[0.0908] ~0.0kb
     [  4] https://www.isc2.org/           r_0 [200] HTTP/1.1  s:                        [1.9348]/[1.9355] ~114.7kb
     [  5] https://facebook.com/           r_0 [301] HTTP/2    s:                        [0.3001]/[0.3006] ~0.0kb
     [  6] https://www.facebook.com/       r_0 [200] HTTP/2    s:                        [0.5904]/[0.5906] ~61.2kb
     [  7] https://httpbin.org/                        < Timeout               > [6.0867]

 [*] Completed 7/7 sites with 7 connections for 9.456673 sec. [ real: 6.10 sec].
```

Below is the sample output where [301] redirection is followed:

```console
 [*] Scanning [7] sites...

           URLs                            Protocols           Server                    Time / Total      Content
==================================================================================================================
     [  1] https://requestbin.com/         r_1 [200] HTTP/2    s:                        [1.3965]/[1.6643] ~522.1kb
     [  2] https://nghttp2.org/            r_0 [200] HTTP/2    s:nghttpx                 [0.3163]/[0.3168] ~6.2kb
     [  3] http://www.isc2.org/            r_1 [200] HTTP/1.1  s:                        [2.0711]/[2.1660] ~114.7kb
     [  4] https://www.isc2.org/           r_0 [200] HTTP/1.1  s:                        [1.9245]/[1.9249] ~114.7kb
     [  5] https://facebook.com/           r_1 [200] HTTP/2    s:                        [0.3767]/[0.6940] ~61.2kb
     [  6] https://www.facebook.com/       r_0 [200] HTTP/2    s:                        [0.6108]/[0.6110] ~61.2kb
     [  7] https://httpbin.org/                        < Timeout               > [6.0383]

 [*] Completed 7/7 sites with 10 connections for 13.415142 sec. [ real: 6.05 sec].
```


