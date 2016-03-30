# pyscan
A simple multi-threaded TCP port scanner written in python.

UDP support may or may not be comming in the future. This program was
written just for fun. If you want a good port scanner use
nmap <https://nmap.org/>.

The code is released under the GPLv3 (see LICENSE).

## Examples

```bash
$ ./pyscan -p 1-5,8080 localhost www.nmap.org
```
will scan ports 1, 2, 3, 4, 5 and 8080 on localhost and www.nmap.org.

```bash
$ ./pyscan -p '*' localhost
```
will scan all ports on localhost.

Adjusting the number of used threads:
```bash
$ ./pyscan -T 20 -p '*' localhost
```
will scan all ports on localhost using 20 threads.

Changing the connect timeout:
```bash
$ ./pyscan -t 20 localhost
```
will scan localhost waiting 20 seconds for an answer.

## Example output
By now only open ports are shown:

```bash
$ ./pyscan localhost
Scan report for localhost:
PORT      STATE    SERVICE
22/tcp    open     ssh
139/tcp   open     netbios-ssn
445/tcp   open     microsoft-ds
631/tcp   open     ipp
```

## Scan details
pyscan executes a full connect() on the target port, so this is no
SYN-scanning like it can be used by nmap. This makes pyscan much
slower, since the full TCP 3-way-handshake is run. Even worse: By
now the implementation even run close() on the open ports, which
causes additional traffic.

## Installation
Simply clone the repository. You'll need to run pyscan from
the same directory, since it uses the stopthread.py module (or
add the directory to your PYTHONPATH).

If for some reason pyscan is not marked executeable, do so
with 'chmod +x pyscan' or your file-manager.
