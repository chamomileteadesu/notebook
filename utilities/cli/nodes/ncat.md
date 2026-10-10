# ncat

> Read, write, redirect, and encrypt data across a network.
> An alternative implementation of a similar utility called `netcat`/`nc`.
> More information: <https://nmap.org/ncat/guide/index.html>.

- listen a port(as server):

  `ncat -l port`

- connect a port(as client):

  `ncat 主机 port`

- File transfer(as sender):

  `ncat -l port > 文件名`

- Fill transfer(as receiver):

  `ncat < 文件名 主机 port`

- Keep listening:

  `ncat -kl port`

- Accept multiple incoming connections on an encrypted channel evading detection of traffic content:

  `ncat --ssl [-k|--keep-open] [-l|--listen] port`

- Connect to an open `ncat` connection over SSL:

  `ncat --ssl host port`

- Check connectivity to a remote host on a particular port with timeout:

  `ncat [-w|--wait] seconds [-vz|--verbose -z] host port`
